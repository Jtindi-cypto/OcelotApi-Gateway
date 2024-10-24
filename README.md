# OcelotApi-Gateway

**#Prerequisists**
.NET core SDK 
Visual studio code.

**STEPS**
STEP 1:
Create a new ASP .NET core web API project using the code below by typing it on your terminal:
dotnet new web API -n OcelotWebApiGetaway
cd OcelotWebApiGetaway

STEP 2:
Install the Ocelot NuGet package using the following codes:
dotnet add package Ocelot.
dotnet add package Microsoft.Extensions.Configurations.Json

Step 3:
Modify the programs.cs file to configure Ocelot. open the programs.cs file add Ocelot to the service pipeline, and add the following modifications:
using Ocelot.DependencyInjection;
using Ocelot.Middleware;

var builder = WebApplication.CreateBuilder(args);

// Add Ocelot
builder.Services.AddOcelot();

// Load the configuration from appsettings.json
builder.Configuration.AddJsonFile("ocelot.json");

var app = builder.Build();

// Use Ocelot middleware
await app.UseOcelot();

app.Run();

STEP 4:
Create the Ocelot Configuration(ocelot.json):
Create a new file named ocelot.json in the root directory of your project. This file defines the routing and configuration for the API gateway.

{ 
  "Routes" :[{
     "DownstreamPathTemplate": "/api/service1/{everything}",
     "DownstreamScheme": "http",
     "DownstreamHostAndPorts":[{
     "Host" : "localhost",
      "Port" : 5001
     }],

     "UpstreamPathTemplate": "/service1/{everything}",
     "upstreamHttpMethod":["GET","POST"],
     "GlobalConfiguration": {
      "BaseUrl":"http://localhost:5000"
     }

}]  
}
STEP 5:





