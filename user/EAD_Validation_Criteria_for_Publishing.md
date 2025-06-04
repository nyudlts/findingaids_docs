## EAD Validation Criteria for Publishing Finding Aids:
NYU Digital Library Technology Services 2025-06-04

1. EADs must be valid XML.  
2. EADs must pass validation against the [EAD 2002 schema](https://www.loc.gov/ead/ead.xsd). 
3. The EAD file must be smaller than 100 MB in size.
4. The EAD ID field will be used for generating finding aid and filename identifiers. 
This data is recorded in the collection-level ArchivesSpace record in the `Finding Aid Data > EAD ID` field.   
   EAD IDs must consist of:
   * a minimum of 2 groups of characters separated by an underscore (`_`)  
   * lower-case alphanumeric, `a` through `z` and `0` through `9`, characters 
   * EAD IDs containing other characters e.g.,  `" "`, `","`, `"|"`, `"&"`, `"-"`, `"."`, or any Upper-Case letter, will be rejected with a message stating the unauthorized characters.  
   * The maximum number of characters allowed in an EAD ID, including the underscores, is 251.  
  Examples of valid EAD IDs: `mss_417`, `photos_220`, `rg_2_2_7`, `rg_38_0_1_2`  
5. The Repository Name field will be used for branding and grouping finding aids. This data is recorded in the `System > Manage Repositories > Repository Name` field in ArchivesSpace. Access to this field is restricted to users with repository management permissions.   
The `<did><repository><corpname>` must be in the following set:  
   * Akkasah: Photography Archive (NYU Abu Dhabi)
   * al Mawrid Arab Art Archive, NYU Abu Dhabi
   * Brooklyn Collection
   * Brooklyn Historical Society
   * Center for Brooklyn History
   * Fales Library and Special Collections
   * NYU Abu Dhabi, Archives and Special Collections
   * New York University Archives
   * New-York Historical Society
   * Poly Archives at Bern Dibner Library of Science and Technology
   * Tamiment Library and Robert F. Wagner Labor Archives
   * Villa La Pietra
6. The EAD top level element must be `<archdesc level="collection">` in order to be indexed by the discovery tool. This data is recorded in the `Basic Information > Level of Description` field in the collection level ArchivesSpace record.  
7. The EAD does not contain any elements with attribute audience="internal". When downloading an EAD file, ensure `Export > Download EAD > Include unpublished` is **not** checked in the collection level ArchivesSpace record.
