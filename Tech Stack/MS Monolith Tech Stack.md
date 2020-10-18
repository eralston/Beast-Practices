This is a summary of the technologies that make for an efficient monolithic, Microsoft-centric web SPA + API application.

## Learning Resources

-   Microsoft Learn - <https://docs.microsoft.com/en-us/learn/>
-   For an overview of architecture used at LiveTiles, read this: <https://medium.com/@ErikRalston/my-cloud-cookbook-15cbb5bfde40> We're going to start Monolithic then move to Elastic

## Tools & Process

-   Visual Studio Community 2019 - <https://visualstudio.microsoft.com/vs/community/>
-   Azure DevOps (ADO) -  Work Items, Git, CI/CD - <https://azure.microsoft.com/en-us/services/devops/>
-   Product Management, Creative Process, and SCRUM process: <https://medium.com/@ErikRalston/the-team-america-playbook-f7cb33f72473>

## Front-End

-   Typescript - <https://www.typescriptlang.org/>
-   React 16 - <https://reactjs.org/>
-   React Router -  <https://github.com/ReactTraining/react-router#readme>
-   Mobx - <https://mobx.js.org/README.html>
-   Bootstrap 4 & Reactstrap - <https://reactstrap.github.io/>
-   Font Awesome 5
-   Argon Dashboard v1.1.2 - <https://demos.creative-tim.com/argon-dashboard-react/#/admin/index>
-   Jest - <https://jestjs.io/>
-   Axios - <https://github.com/axios/axios>

## Back-End

-   C#
-   .Net Core 3.1
-   LINQ
-   Entity Framework Core
-   ASP.Net Core WebAPI - <https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-3.1&tabs=visual-studio>
-   With consideration for potential re-platforming to [Azure Functions](https://azure.microsoft.com/en-us/services/functions/) in the future
-   Swashbuckle - <https://github.com/domaindrivendev/Swashbuckle.AspNetCore>
-   Azure - <https://azure.microsoft.com/en-us/>
-   Sendgrid (email) - <https://sendgrid.com/>
-   Twilio (SMS) - <https://www.twilio.com/>

## Azure Resources
-   PaaS and FaaS only; No IaaS, no containers

| Name | Resources |
|--|--|
|App Service Plan (Azure Web App) |<https://azure.microsoft.com/en-us/pricing/details/app-service/windows/> |
|SQL Database |<https://azure.microsoft.com/en-us/pricing/details/sql-database/single/> |
|Storage (Blobs & Tables) |<https://azure.microsoft.com/en-us/pricing/details/storage/blobs/> |
|Azure Active Directory (also B2C flavor) |<https://azure.microsoft.com/en-us/pricing/details/active-directory/> |
|CDN |<https://azure.microsoft.com/en-us/pricing/details/cdn/> |
|Redis Cache |<https://azure.microsoft.com/en-us/pricing/details/cache/> |
|Key Vault |<https://azure.microsoft.com/en-us/services/key-vault/> |
| Cognitive Services | <https://azure.microsoft.com/en-us/services/cognitive-services/>|