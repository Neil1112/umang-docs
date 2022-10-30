# Branch Description Guide

---

This document lists the description of the git branches of the project. It lists the purpose of the branch, along with its environment, other configurations like database attached and the various checks one must do when commiting their work. By understanding the branches, we will understand the workflow of the development process.

## Important branches

There are five important branches in the project. These branches are listed down in the table below:

|Branch name|
|------------------|
|master|
|dev|
|e2e|
|alpha|
|rc|

## Branch Workflow

![branches](./../img/branch-description/branches.jpg)

There are 5 major branches that participate in the development cycle.
There are several resources which are shared by `dev`, `e2e`, `alpha` and `rc` branches. These are listed as follow:

|Resource|Description|
|------------------|--------------|
|JWT_SECRET_OR_KEY|NSDevelopers|
|TWILIO_SMS_ACCOUNT_SID|_not written due to security reasons_|
|TWILIO_SMS_AUTH_TOKEN|_not written due to security reasons_|
|GOOGLEAUTH_CLIENT_ID|92783308442-uts2q3bmagdfbj7br6g7igg48e9qqgk5.apps.googleusercontent.com|
|GOOGLEAUTH_CLIENT_SECRET|cRoE7ULcMyd63LfqhJve7sds|
|GOOGLEMAIL_TYPE|service_account|
|GOOGLEMAIL_PROJECT_ID|umangwellness-286808|
|GOOGLEMAIL_PRIVATE_KEY_ID|a53e5cd430b418b9e6b280c4e6211d16187373a2|
|GOOGLEMAIL_CLIENT_EMAIL|support-umagwellness@umangwellness-286808.iam.gserviceaccount.com|
|GOOGLEMAIL_CLIENT_ID|101789851039019824166|
|GOOGLEMAIL_AUTH_URI|https://accounts.google.com/o/oauth2/auth|
|GOOGLEMAIL_TOKEN_URI|https://oauth2.googleapis.com/token|
|GOOGLEMAIL_AUTH_PROVIDER_X509_CERT_URL|https://www.googleapis.com/oauth2/v1/certs|
|GOOGLEMAIL_CLIENT_X509_CERT_URL|https://www.googleapis.com/robot/v1/metadata/x509/support-umagwellness%40umangwellness-286808.iam.gserviceaccount.com|
|CHAT_ACCOUNT_SID|AC6b8a7f251d357fee94f2e9b203b411fd|
|CHAT_AUTH_TOKEN|efbbf0f42e469bcd62f5f87a821f0c60|
|CHAT_API_KEY|SK8f823dd68f2def2cd0fbcb0633034e7a|
|CHAT_API_SECRET|X2lfYrfpFCuWbmkWRLyz7msNN0KLmcWL|
|CHAT_SERVICE_SID|IS373c6b6939ef48fcaf602fc738af62d1|


Let's look at these branches one at a time.

### dev branch

The `dev` branch is responsible for all the new development code in either backend or frontend. It's purpose is to track the new code being developed for the next version.

|Resource|Description|
|------------------|--------------|
|Enviornment| `development` |
|Database|Dev - mongodb+srv://neil:developer@cluster0-xf1az.gcp.mongodb.net/umangwellness-dev-new?retryWrites=true&w=majority|
|server port|5000|
|Azure web-service instance|umang-dev|
|Hosted at|https://umang-dev.azurewebsites.net|
|Version example|1.2.2|

List of things that the `dev` branch is responsible for:

- Any new development in either backend or frontend.
- Developing new code for next version.
- Serving `umang-dev` instance at _**https://umang-dev.azurewebsites.net**_, which reflects the latest commited developments in the code.
- The first step for any MAJOR, MINOR or PATCH release.
- In case of quick fix required in the production the website is put into maintainence mode, and the fix is first applied in `rc` branch to quickly merge the changes in the `master` branch. Once the changes are pushed to `master`, they must be reflected then in the `dev` branch.
- Test Driven Development (TDD) is followed in the development process. Hence all the integration testing is being done in the `dev` branch only.

![testing-workflow](./../img/branch-description/testing-workflow.jpg)

### alpha branch

The `alpha` branch is responsible for all the testing on the newly developed code in the `dev` branch. Once the code is developed for any version in the `dev` branch, it is then merged into the `alpha` branch for testing. There are 3 types of testing - integration, e2e and manual. Integration testing is being done in the `dev` branch, and the e2e and manual testing are then done in the `alpha` branch.

If the code is updated in the `alpha` branch, then apply the suffix in the versioning properly as shown in the table below:

|Resource|Description|
|------------------|--------------|
|Enviornment| `alpha` |
|Database|Alpha - mongodb+srv://alpha@cluster0-xf1az.gcp.mongodb.net/umangwellness-dev-new?retryWrites=true&w=majority|
|server port|5000|
|Azure web-service instance|umang-test|
|Hosted at|https://umang-test.azurewebsites.net|
|Version example|1.2.2-a.1|


List of things that the `dev` branch is responsible for:

- For creating the base for e2e testing. e2e testing is done in the `e2e` branch, which gets all the code from the `alpha` branch.
- For doing the manual testing once the e2e tests passes.
- If there is any error/bug found in any of the testing phase, then they must be fixed in the `dev` branch, and then the fixes should be merged into the `alpha` branch. Hence there is a cycle between dev-alpha-testing.
- Once we feel confident about the code in the `alpha` branch, we merge it into the `rc` (release candidate) branch.
- Serving `umang-test` instance at _**https://umang-test.azurewebsites.net**_, which reflects the latest commited developments in the code. On this hosted-instance, the manual testing should be done.



### e2e branch

The `e2e` branch is solely responsible for the End to End testing of the frontend code for the next version. It gets its code from the `alpha` branch. If there is any bug found, then it must be fixed in the `dev` branch and then merge it to the `alpha` branch.

|Resource|Description|
|------------------|--------------|
|Enviornment| `e2e-test` |
|Database|created on the fly|
|server port|5000|




### rc branch

Once we are confident about the stability of the code after running the tests in the `alpha` branch, we merge the code in the `rc` branch to make it ready to release. The purpose of the `rc` branch is to keep the base ready at all time that is exactly identical to the production (i.e - `master` branch). The idea is, if there is any quick fix required in the production, then it is immediately addressed in the `rc` branch and the fix is merged in the `master` branch for quick release.

The `rc` branch is almost identical to the master branch, but have few configuration changes. If the code is updated in the `rc` branch, then apply the suffix in the versioning properly as shown in the table below:


|Resource|Description|
|------------------|--------------|
|Enviornment| `release-candidate` |
|Database|Prod-Clone - mongodb+srv://prod-clone@cluster0-xf1az.gcp.mongodb.net/umangwellness-dev-new?retryWrites=true&w=majority|
|server port|80|
|Version example|1.2.2-rc.2|

All other services and APIs are same as the `master` branch.

> Note - some of the features may be turned off in the `rc` branch to avoid unneccesary constraints.

### master branch

The `master` branch is responsible to host the `production` version. No changes should directly be done in the `master` branch. In case of small bug fix, turn the site into maintenance mode, apply the changes in the `rc` branch and then deploy the changes in the `master` branch. The bug should then be addressed in the `dev` branch and tested fully and then a new version with an incremented patch must be deployed.


|Resource|Description|
|------------------|--------------|
|Enviornment| `production` |
|Database|Prod - _link not written for security reasons_|
|server port|80|
|Azure web-service instance|umangprod|
|Hosted at|www.umangwellness.com|
