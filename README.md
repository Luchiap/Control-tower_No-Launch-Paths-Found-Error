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

Go to CloudTrail [1](https://us-east-1.console.aws.amazon.com/cloudtrail/home?region=us-east-1#/events?EventName=ListLaunchPaths) --> event history --> Lookup attributes --> Event name --> type down 'ListLaunchPaths'

![ListLaunch1](https://github.com/Luchiap/Control-tower_No-Launch-Paths-Found-Error/assets/83933068/9b26351e-5626-43c7-94d0-417f635b33b1)

Check the most recent API record, open it and check the principal that performed the action. 

### Case 1, logged in as root

If you were logged in as root, you will need to logout and login as a user or role that has the necessary permissions of using Control Tower.

### Case 2, logged in as user/role

If you were logged in as user/role and still got the same error, 

Go to Service Catalog --> Portfolios --> AWS Control Tower Account Factory Portfolio --> Access.

Check if your user/role is listed here. If it's not then you will need to add it. Click on Grant Access and follow the steps.

In my case, I am logged in as adminuser, this user has to be appear in this list.

![Service](https://github.com/Luchiap/Control-tower_No-Launch-Paths-Found-Error/assets/83933068/0601bc18-5ffe-4251-a205-643c3e6a3b81)

### Case 3, logged in as user/role with access to portfolio

If you were logged in as user/role and checked that you had access to the portfolio, you will need to check if the SSO user of your management account is part of group AWSAccountFactory or AWSServiceCatalogAdmins in IAM Identity Center. It must be part of one of them at minimum. 
See below.

![AccountFactory](https://github.com/Luchiap/Control-tower_No-Launch-Paths-Found-Error/assets/83933068/566dd886-ea54-4976-99a2-d1cfc7dad2d2)






## References:

[1] https://us-east-1.console.aws.amazon.com/cloudtrail/home?region=us-east-1#/events?EventName=ListLaunchPaths
