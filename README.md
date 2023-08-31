# No Launch Paths Found Error



## Cause of error:
You will get this error when you try to perform actions on Control Tower (creating/enrolling/updating an account) with the wrong principal such as:
+ Root user (this will always fail)
+ A role/user that has not been added to the ‘Access’ tab of the ‘AWS Control Tower Account Factory Portfolio’ in Service Catalog. It may also be missing the servicecatalog:ListLaunchPaths permission.

Also, when:
+ The SSO user of the account has not been added to the ‘AWSAccountFactory’ or ‘AWSServiceCatalogAdmins’ Groups in IAM Identity Center

## Example:
Trying to create an account when you are logged in as root access will give you this red bar preventing you from doing so.

![NoLaunch](https://github.com/Luchiap/Control-tower_No-Launch-Paths-Found-Error/assets/83933068/808ebc46-fc1d-40e3-b831-16483063799c)


## How to troubleshoot and how to fix

Go to CloudTrail [1] --> event history --> Lookup attributes --> Event name --> type down 'ListLaunchPaths'

![ListLaunch1](https://github.com/Luchiap/Control-tower_No-Launch-Paths-Found-Error/assets/83933068/9b26351e-5626-43c7-94d0-417f635b33b1)

Check the most recent API record, open it and check the principal that performed the action. 

### Case1, logged in as root
Go to CloudTrail [1] --> event history --> Lookup attributes --> Event name --> type down 'ListLaunchPaths'

Logout as root and login as a user or role that has the necessary permissions of using Control Tower




References:
[1] https://us-east-1.console.aws.amazon.com/cloudtrail/home?region=us-east-1#/events?EventName=ListLaunchPaths
