# SwaggerConfigurationExtension

This project was created with the intention of versioning and configure a webapi in aspnet core v2.1 using the swagger (Swashbuckle.AspNetCore)

-- =============================================
-- Author: Pedro Henrique Vasconcellos
-- Create date: 01/08/2018
-- Description: This project was created with the intention of versioning and configure a webapi in aspnet core using the swagger (Swashbuckle.AspNetCore)
-- Site: https://vasconcellos.solutions/
-- =============================================

//Use in Controllers you do want to version
[ApiVersion("1.0")]
[Route("v{version:apiVersion}/[controller]")]

//Use in Controllers you do not want to version
//Obs: You can use this tag for the Token Generation Controller
[ApiVersionNeutral]
[Route("[controller]")]

//Referencing the project
using VasconcellosSolutions.SwaggerConfigurationExtension;

//Using => Class: Startup Method: ConfigureServices(IServiceCollection services)
using SwaggerConfigurationExtension;
public void ConfigureServices(IServiceCollection services)
{
    string typeToken = "Bearer";
    var apiKeyScheme = new ApiKeyScheme { In = "header", Description = "Please enter JWT with Bearer into field", Name = "Authorization", Type = "apiKey" };
    string name = "Vasconcellos WebAPI"
    string description = "This project has the purpose of performing an exemplification";

    var swaggerConfigurationExtension = new SwaggerStartupConfigureServices(services, typeToken, apiKeyScheme)
        .SetNameAndDescriptionProject(name, description);
}

//Using => Class: Startup Method: Configure(IApplicationBuilder app, IHostingEnvironment env)
public void Configure(IApplicationBuilder app, Microsoft.AspNetCore.Hosting.IHostingEnvironment env)
{
    //If you set "withInjectStyleSheet" to true, in "wwwroot" create a folder named "swagger" and put a custom css file "swaggercustom.css"
    bool withInjectStyleSheet = false;
    string swaggerDocumentationRoute = "Swagger";
    var swaggerStartupConfigure = new SwaggerStartupConfigure(app, withInjectStyleSheet, swaggerDocumentationRoute);
}