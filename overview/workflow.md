# Finding Aids Workflow and System Overview

![](./fa-workflow-v0_2_1.png)

#### Sequence
* the Archivist...
  * exports an EAD from ArchivesSpace
  * logs into the EAD Publisher (EP) application
    * https://ead-publisher.dlib.nyu.edu/findingaids/publish
  * selects the archival repository
  * selects whether or not the EAD contains new or updated digital images
  * uploads the EAD...

* then the EP...
  * stores the uploaded EAD on the Isilon storage system
  * validates the EAD
    * if the EAD fails validation, the EP...
      * provides an error report to the Archivist and deletes the uploaded EAD
    * if the EAD passes validation, the EP...
      * names the uploaded EAD file `<eadid>.xml`, e.g., `mss_208.xml`
      * calls the `FASB` to generate the `JSON` files required by `Hugo`
      * calls `Hugo`to generate the finding aid
      * returns links to the EAD and the preview finding aid to the Archivist

* the Archivist...
  * reviews the preview finding aid and/or EAD
  * decides whether or not to publish the finding aid or remove it
    * if the Archivist decides to remove the finding aid...
      * then the EP...
        * deletes the preview finding aid files
        * deletes the preview EAD file
        * returns to the EP home screen
    * if the Archivist decides to publish the finding aid...
      * then the EP calls the `deploy` script that...
        * removes the outdated finding aid from the AWS S3 bucket
        * copies the new finding aid to the AWS S3 bucket
        * invalidates the URLs for the finding aid in the AWS CloudFront CDN
        * enqueues a Git Transactor (GT) `add` task for the EAD
        * returns to the EP home screen

* the GT wakes up and...
  * if there is an `add` task in the queue...
    * pulls the latest version of the EADs Git repository to local storage
    * copies the just-published EAD to the local EADs Git repository
    * commits the just-published EAD to the local EADs Git repository
    * pushes the local EADs Git repository to GitHub

* the Finding Aids Bridge (FAB) discovery application then...
  * receives a message that the EADs Git repository has been updated in GitHub
  * pulls the latest version of the EADs Git repository
  * adds/updates the search index with data from the just-published EAD

* the Patron...
  * visits the FAB discovery application...
    * https://specialcollections.library.nyu.edu
  * and searches the EAD index
  * the FAB provides search results with links to the published finding aid(s) 
  * the Patron visits the links of interest
    * e.g., https://findingaids.library.nyu.edu/fales/mss_208/



