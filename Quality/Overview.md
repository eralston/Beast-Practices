Article to explain not only QA, but key focus areas for top quality coding

# Quality Principles
---
The STAUP framework (Security, Testability, Accessibility, Usability, and Performance) was originally developed by the US Products team at LiveTiles as a way to provide the qualitative aspects of good design and development. It was intended to guide review of designs and provide a means of giving feedback during PR Reviews beyond syntax and design patterns.
- Security
- Testability
- Accessibility
- Usability
- Performance

# Quality & Deployment Process
---
Quality starts with developers and ends with the customers. Here are the key steps involved with creating quality software.

## Environments
Multiple deployment areas for builds of the product. Each may have its own Appsettings JSON in the project codebase and each one ties to its own set of resources in Azure.
- Feature flags in the Appsettings JSON can control what features are toggled on and off in the system. As of this writing, they are all currently focused on the front-end code, but could affect the back-end in the future.

### Development (lcl)
A developer's machine is one environment. Ideally, this is able to run the app w/o a connection to the internet - if you're not ready to code on a plane, you're not ready to run a global software company.
- All automated tests should pass locally before committing. Because we use "rebase and fast forward", it incentivizes us to attempt to prevent even a single commit from having a bad build.
- The only known exception right now is that the unit tests for Storage are not able to run vs Azurite
- Database migrations are manual at the moment

### Test (tst)
The Test Environment is the first deployment location once a PR completes to the trunk branch and its deployment happens automatically. It provides hands-on testing for new features and should be manually tested before releases graduate to Beta. This is in the West US Region.

### Beta (bet)
The "preview" environment with early adopter users. These are NOT paid customers, but we should dedicate ourselves to providing them a good experience. This is also in the West US region.

### Staging (stg)
The staging environment is a pre-prod environment that uses a deployment slot on the production web app.

### Production (prd)
The forthcoming production environment(s) will be located in regions relevant to customer locations. This is the only environment that will have any kind of Service Level Agreement (SLA) and even then it's currently estimated around 99.3% availability at best.

## Automated Testing
Code testing code - but who tests the test???

### Test-Driven Development
It is recommended developers make unit tests first when developing the application. While the author does not necessarily do this on the front-end very often, I always do it on the back-end since it's always purely transactional.

### Test on Commit
Thanks to the Husky NPM package, there is always a pre-commit hook to format, unit test, and build the front and back end components on check-in.

### Build Validation
In the Pipeline in ADO, the project(s) should use build validation via branch policy such that the PR has to pass pipeline validation before being allowed to complete.

### Test on Deploy
In the Pipeline in ADO, the project(s) should also run the unit tests on deployment. At some point, this will include [end-to-end tests](https://www.browserstack.com/guide/end-to-end-testing) to thoroughly exercise the application.

## Manual Testing
Manual testing is the process of a human clicking on things to make sure the software works as intended. Before approving the graduation of a build through the sequence of Test -> Demo -> Beta -> Staging -> Production, there should be an increasing amount of hands-on manual testing by the team.

### Feature Testing
For each new feature in the product, it should receive a thorough exercising in Test before moving to beyond. This should be done by the developer and at least one other person.
- This is unique to each feature, but should include "Happy Paths"
- This should include negative paths (EG, empty and error states).

### Regression Testing
A thorough click through all currently known features before releasing the software in earnest. While this may be only one person to go from test to Demo, Demo to Beta is the key step where regression should have been done aggressively.
- This would benefit most from turning on the "Test" features in ADO to track real scenarios at a low level

### Smoke Testing
Moving from Beta to Demo and beyon, there should be an efficient hands-on test at each stage, but it can focus on "happy paths" and simplistic, yet comprehensive testing of features. In the very least, it should touch a transaction on each kind of system, such as:
- Performing all interactions with the dev console open in the browser to look for errors
- Logging in to make sure auth works
- Looking at Teams and Users to ensure Graph works
- Creating an entity (EG, Team, Session, or Series) to make sure the database works
- Creating and listening to a Clip to make sure Azure Storage works
- Checking the log to make sure App Insights works