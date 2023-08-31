# No Launch Paths Found Error



## Cause of error:
You will get this error when you try to perform actions on Control Tower (creating/enrolling/updating an account) with the wrong principal such as:
+ Root user (this will always fail)
+ A role/user that has not been added to the ‘Access’ tab of the ‘AWS Control Tower Account Factory Portfolio’ in Service Catalog. It may also be missing the servicecatalog:ListLaunchPaths permission.

Also, when:
+ The SSO user of the account has not been added to the ‘AWSAccountFactory’ or ‘AWSServiceCatalogAdmins’ Groups in IAM Identity Center
