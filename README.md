## Document your RESTful APIs using swashbuckle ##

Recently I was asked to provide WADL (Web Application Definition Language), for a fairly large scale ASP.Net Web API project, by another development team. The request/response payloads are differnt large and complicated objects. My research led me to the widely popular, language-agnostic, easy to use and implement solution - [Swagger](http://Swagger.io). This not only documents your Web API endpoints but also allows the consumers to play around with the Web API calls. 

### Swashbuckle ###

**Swashbuckle** is a nuget package that provides your development team or end consumers an interactive way to visualize your API's. Swashbuckle uses the **Swagger** framework for describing, consuming, and visualizing RESTful APIs. Swagger is not dependent on MVC, it uses css, javascript and html for generating the UI.

### About the project ###

What we have here is a ASP.Net Web API project setup. There are two Nuget packages Swashbuckle.Core and a Swashbuckle package that provides a convenient interactive UI for your WebApi consumers.

### Getting started with a IIS hosted ASP.NET Web API ###

Assuming we have a Web API Project setup. We would use the following steps to add swashbuckle to your project.


#### Step 1 - Add Nuget packages ####

##### Using package manager console
If you prefer using package manager console, then type the following in the console to install Swashbuckle pacakge.

`Install-Package Swashbuckle -Version 5.5.3`
##### In Visual Studio
If you prefer using Visual Studio to install your pacakge, then right click your project in Solution Explorer and choose Manage NuGet Packages option.
Search **Swashbuckle** in the search box and select the package and install it.

![alt text](/images/ManageNuget.png "Manage Nuget Packages")

The following dependencies will be installed for package **Swashbuckle 5.5.3**

![alt text](/images/Packages.png "Dependencies")

##### Swagger Config 

A Swagger configuration file is added to the App Start folder. Although the default documentation is very detailed and may not require any additional work. There are times when you want to exercise control over what consumers see. There are several options to customize and control the way you want to render your documentation. We will explore some of the options in the next sections.

 ![alt text](/images/config.png "SwaggerConfig File")

##### Swagger UI

Once you have the package installed. You can run your project and browse to 
`<your-root-url>/swagger/ui/index` to view the documentation generated by Swashbuckle. Consumers can discover and experiment the calls in this UI by using the Try it Out option too.

![alt text](/images/swaggerUI.png "Swagger UI")

Details of each controller action's request and response and sample types are available to the consumers. 

![alt text](/images/details.png "Swagger UI")

Consumers can also experiment by trying out the calls to get a better understanding of the results.

![alt text](/images/tryitout.png "Swagger UI")

Json generated by swagger can be accessed by browsing to `<your-root-url>/swagger/docs/v1`.

 ![alt text](/images/json.png "Swagger Json")

#### Step 2 - Avoid Schema Id Conflicts

By default, Swashbuckle does not use full type names. If you have multiple objects with same names, like I did, you will have to use full type names. You can do this by adding the following to the SwaggerConfig file in App Start.

`c.UseFullTypeNameInSchemaIds();`

#### Step 3 - Disable Validator

Swagger UI is setup to use an online validator online.swagger.io out of the box. If it cannot access your swagger url then you will see an error message in your swagger UI. To prevent this, you can disable validation by adding the following to your SwaggerConfig file.

`c.DisableValidator()`
