# Testability
---
Testability of software obviously relates very closely to the concept of software testing. Software testing is the process of scrutinizing and evaluating a piece of software to see that it performs the job that it was written to do. In that same vein means writing testable software means designing and developing software in a way that facilitates this process. Testing ideally happens at every stage throughout the software development lifecycle, from design to release, and involves a multitude of departments, from Design to Development to QA.

## Glossary
--
When discussing principles of testability, the following terms are useful:

### Software Management

**Project --** A deployable unit of software, either as a full-on end user application or auxiliary service

**Feature --** An atomic unit of functionality contained within a software project

**Bug --** An erroneous behavior exhibited by a software feature

### Testing Goals

**Verification --** Does the application work correctly?

**Validation --** Does the application meet the end users' needs?

### Testing Methods

**Black Box Testing --** Testing a piece of software primarily through its UI/UX with no knowledge of its inner workings.

**White Box Testing --** Testing a piece of software with full access and knowledge of its inner workings.

**Gray Box Testing --** Testing a piece of software with partial access and knowledge of its inner workings.

### Testing Levels

**Unit Testing --** Testing an individual unit or module of software in isolation

**Integration Testing --** Testing the interaction of multiple modules of software in combination

**End-to-End (or System) Testing** **--** Testing the whole application in an environment that closely mimics the type employed in a production setting

**Functional/Feature Testing --** Testing a new individual feature

**Regression Testing --** Testing an application to determine that new features or fixes introduced haven't re-introduced bugs elsewhere

**Acceptance Testing --** Final testing performed on an application that ultimately decides whether the new feature or change will be released to the customer

### Testing Metrics

**Code Coverage --** A percentage total of the lines of code executed during a feature's automated test sweep

## Testability Resources
---
Some resources across the web to better understand the scope of Testability:

- [Software Testing Overview](https://www.w3schools.in/software-testing/overview/)
- [A Decent Medium Post on Front-End Testing](https://medium.com/@giltayar/testing-your-frontend-code-part-i-introduction-7e307eac4446)
- [MSDN's Article on Unit Testing Best Practices (for .NET Core, but Still Generally Useful)](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)

## Testability Evaluation
---
The following areas and consideration questions should be used to evaluate our software for testability:

**Clear Requirements** -- It's difficult to test software when you don't even know how it should behave to begin with. A given feature request should thus have well-documented requirements. These requirements should exist in a single location easily referenced by all involved in the development process and should serve as a single source of truth for that feature. Each requirement section should have a clearly delineated owner (i.e. a designer, developer or QA person) that is responsible for preparing and maintaining it. Requirements should be detailed, and include, among other things, how the user accesses this feature, what the feature should look like (e.g. with a mock-up), and what the feature should and should not do. As requirements update in response to feedback, a section's owner must make sure documentation reflects those changes as soon as possible and notify any other interested parties (i.e. developers and/or QA). We have opted to use Azure DevOps as its primary work-tracking platform, and the specific processes its developers follow are listed below:

**Does a feature proposal have a concrete epic/feature/backlog item created for it?** -- Each planned feature should have a corresponding epic, feature, or backlog item in Azure DevOps, according to the item's scope. This should originate from a combination of project management, development, and design

**Does the feature have a detailed description of what it should do?** -- Each feature should have a complete description of its expected behavior so that developers can know what to code for, and QA can know what to test for. This should likely be authored by a combination of designers and developers during the design phase.

**Does the bug have a list of replication steps? --** Each bug should have a list of steps to reproduce the cited issue, for use by development in diagnosing the issue, and by QA in ensuring the bug has been fixed

**Does the feature have a mock-up? --** Each visual addition or change to a product should have a corresponding mock-up, either embedded directly or linked, to reference both for development and testing purposes. This should be managed primarily by a designer. This mock-up should contain complete information about how the feature will look under a variety of circumstances (e.g. different screen/element sizes, when certain elements hover over/clicked on, when certain elements are opened or closed, etc.). Designers will ideally update mock-ups as requirements change, but should that prove impractical, the feature's written description should be updated and ultimately referenced over the mock-up.

**Does the feature have a list of acceptance criteria?** -- Each feature should contain a list of acceptance criteria, which will serve as a checklist of properties/behaviors to verify during the QA process for the purposes of acceptance testing. This should primarily be compiled by design and development during the design phase, and then maintained by development thereafter.

**Writing Testable Code --** Not all code is equally testable. Code that lends itself most easily to automated development testing tends to have several features in common. The following are good guidelines to abide by when adding to a codebase, though you shouldn't necessarily keep to them mindlessly. You can only abstract away so much, and at some point, your code will need to do work that doesn't fit with these properties.

**Is my code modular? --** Code that runs in self-contained, easily spun-up units (e.g. functions or classes) without relying on global side effects or settings is often more easily tested than code that doesn't fit this pattern. Dependency inversion

**Is my code repeatable?** -- Testable code should be able to run randomly and repeatedly at any given time. Cases where this may fail include code that incorporates a component of time (e.g. checking whether a given data point is before or after today), or code that makes use of randomly generated values (e.g. guids and other ids). Such code can still be tested, but perhaps not as robustly

**Does my code set up good data contracts and abstractions? -** Code that interacts with well-defined, implementation-agnostic interfaces tends to be easier to test, since those interfaces can be faked/mocked within a test environment.

**Does my code make good use of dependency inversion? -** It's often easier to test code that receives its dependencies as arguments in function or constructor parameters, rather than creating them or importing them directly. This again allows those dependencies to be mocked in test environments and easily handed off to your code where appropriate

**Does my code receive or call into code from elsewhere in the app?** -- Even with good abstractions and dependency inversion, the more dependencies from other parts of the app your code has (whether through direct imports or dependency inversion), the likelier it is you'll need to mock something in order to properly run a unit test, or spin something up to run an integration or end-to-end test.

**Does my code depend on platform-specific­ functionality? ­­--** If your code makes use of something provided by its host framework/platform, you'll need to emulate that through mocks or a testing utility (like JSDom for front-end code) in whatever test environment you set up. Examples in TypeScript/JavaScript include calling directly into the DOM or making use of JSOM in the case of the SharePoint product. Backend examples include directly referencing the properties on an HTTP request in an ASP.NET MVC controller action

**Does my code call into a network service/run an IO/database operation? --** Making a network, I/O, database, etc. request from your codenot only dramatically slows your tests down, but also greatly raises the chances that your tests will fail unpredictably. Like with dependencies elsewhere in the code base, you'll need to mock calls into these services in some way in order to test them quickly and reliably

**Thorough Development Tests --** A feature or service should have a thorough, repeatable suite of tests with reasonable coverage that can be run periodically throughout development to track that the feature is matching with its expected behavior, and at later dates to ensure that subsequent changes haven't introduced any regression bugs. The ideal combination of unit, integration and end-to-end tests depends heavily on the feature being written and the environment where the code will live (i.e. client-side vs. server-side).

**Does my code have tests that verify a variety of inputs? --** Tests should verify that a piece of code returns expected values for both valid and invalid inputs. These tests should also check for malicious input in cases where that may be a risk

**Does my code test itself for a variety of different states?** --For stateful pieces of code, tests should verify all the different changes of outward state that it can undergo, and ensure that it never enters anything invalid

**Does my code have tests with descriptive names?** -- A piece of code's corresponding tests should succinctly describe what the test does and what it expects to happen

**Does my app have tests that verify its most common pathways? --** It is useful for many apps to have a few integrations and/or end-to-end tests that spin up an entire environment and verify that it doesn't error through the app's most common actions

**Does my service have a set of tests to verify that it's maintaining its data contract?** -- An auxiliary web API should in some way test that it accepts and returns data in a backward-compatible way as it changes. Should any changes be introduced that need to break this compatibility, this will signal to the developer the need to either update the client or deploy a **new** major version of the service

**Does my code test do basic performance testing? -** Common actions taken by your code should have their performance measured in some way and either integrated into the project's test suite or sent on to some analytics service (like Azure Application Insights) in a production environment

**If necessary, does my service/feature perform load tests? --** It may be useful to set up automated tests to ensure that the feature/service can handle expected workloads (i.e. from normal data input sizes or a normal number of simultaneous user requests). This is especially vital to test in features or services that are critical for the product to be used

**If necessary, does my service/feature perform stress tests? --** It may be useful to set up automated tests that identify at what data input sizes and request workloads the service/feature begin to break down, and if such cases can lead to disaster scenarios like crashes or data loss. This is especially vital to test in features or services that are critical for the product to be used

**Code and Project Documentation --** Good project documentation can help to ease code testability, especially in cases where new developers/testers are brought onto a project.

**Does my project have a detailed README file? -** A good README file (or project wiki) can aid in testability for new developers brought onto a project, since it can serve not only as a place to describe what the project is supposed to do, but also describe what testing technologies the project uses, and what approaches the original developer(s) have taken in writing their tests

**Does my code have good documentation? -** Standard class/function documentation formats (like JSDoc in JavaScript and XML documentation in C#) can aid discovery by automated testing tools. They also serve as good foundations to start writing/editing tests from when they provide detail about how the unit of code should behave, what inputs it should take, what it should return, and when it should error

**Integration with Automated Build Pipelines --** Development tests written for a product, service or feature should be integrated into that project's automated build pipeline (i.e. CI/CD), such that they will run whenever a new change is introduced and prevent any erroneous changes from propagating through the deployment chain.

**Does the project include a task/set of tasks to run its associated tests during a build? --** A project must be sure to run its tests during any triggered build event, and automatically fail the build in its entirety should any of its tests not pass

**Is the project set up to notify relevant developers when a build fails? --** Should a build fail to complete, a developer must be notified so someone may step in and restore the master branch to a buildable state as soon as possible

**Integration with QA Automated Test Processes --** Where applicable, code should be written in a way that dovetails as nicely as possible with any automated test platforms that QA has set up. This includes things like making HTML elements easily selectable by test platforms such as Selenium.

**Testability Metrics --** The overall testability of the code produced should possibly be evaluated regularly. This section may also recommendations for evaluating QA's execution on its own testing systems, though that probably won't fall under our purview until we get a local QA person.

**How many bugs per step in the testing process (up to release)**

**Consistent code coverage**

**Consistent performance timers**

**Number of failed unit tests per check-in**

**Number of items under development column without requirements**

**Number of items under testing column without acceptance criteria**