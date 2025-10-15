---
conversation_id: "95e0bda4-262b-4b05-a285-bb035a406366"
title: "Blazor WebAssembly Common Processes"
create_time: 1705331255.251031
update_time: 1705331295.866404
language_guess: "en"
num_messages: 11
part_index: 1
part_count: 1
---

### system — 2024-01-15T15:07:35.251031+00:00

_(empty)_

### user — 2024-01-15T15:07:35.252367+00:00

Brazor webassemblyで共通処理とすべきことがらとさんぷるをしめせ

### assistant — 2024-01-15T15:08:13.291206+00:00

search("Blazor WebAssembly common processes and examples")

### tool — 2024-01-15T15:08:13.293551+00:00

_(empty)_

### assistant — 2024-01-15T15:08:13.299298+00:00

mclick(["0", "1", "4", "5", "6", "7"])

### tool — 2024-01-15T15:08:13.305021+00:00

{ headers: { 'content-type': contentType } });
              })();
            }
          }
        }
      });
    </script>

Standalone Blazor WebAssembly:

    <script type="module">
      import { BrotliDecode } from './decode.min.js';
      Blazor.start({
        loadBootResource: function (type, name, defaultUri, integrity) {
          if (type !== 'dotnetjs' && location.hostname !== 'localhost' && type !== 'configuration') {
            return (async function () {
              const response = await fetch(defaultUri + '.br', { cache: 'no-cache' });
              if (!response.ok) {
                throw new Error(response.statusText);
              }
              const originalResponseBuffer = await response.arrayBuffer();
              const originalResponseArray = new Int8Array(originalResponseBuffer);
              const decompressedResponseArray = BrotliDecode(originalResponseArray);
              const contentType = type === 
                'dotnetwasm' ? 'application/wasm' : 'application/octet-stream';
              return new Response(decompressedResponseArray, 
                { headers: { 'content-type': contentType } });
            })();
          }
        }
      });
    </script>

For more information on loading boot resources, see 【21†ASP.NET Core Blazor startup】.

To disable compression, add the `CompressionEnabled` MSBuild property to the app's project file and set the value to `false`:

    <PropertyGroup>
      <CompressionEnabled>false</CompressionEnabled>
    </PropertyGroup>

The `CompressionEnabled` property can be passed to the 【27†dotnet publish】 command with the following syntax in a command shell:

    dotnet publish -p:CompressionEnabled=false

To disable compression, add the `BlazorEnableCompression` MSBuild property to the app's project file and set the value to `false`:

    <PropertyGroup>
      <BlazorEnableCompression>false</BlazorEnableCompression>
    </PropertyGroup>

The `BlazorEnableCompression` property can be passed to the 【27†dotnet publish】 command with the following syntax in a command shell:

    dotnet publish -p:BlazorEnableCompression=false

## Rewrite URLs for correct routing

Routing requests for page components in a Blazor WebAssembly app isn't as straightforward as routing requests in a Blazor Server app. Consider a Blazor WebAssembly app with two components:

  * `Main.razor`: Loads at the root of the app and contains a link to the `About` component (`href="About"`).
  * `About.razor`: `About` component.

When the app's default document is requested using the browser's address bar (for example, `https://www.contoso.com/`):

  1. The browser makes a request.
  2. The default page is returned, which is usually `index.html`.
  3. `index.html` bootstraps the app.
  4. 【28†Router】 component loads, and the Razor `Main` component is rendered.

In the Main page, selecting the link to the `About` component works on the client because the Blazor router stops the browser from making a request on the Internet to `www.contoso.com` for `About` and serves the rendered `About` component itself. All of the requests for internal endpoints within the Blazor WebAssembly app work the same way: Requests don't trigger browser-based requests to server-hosted resources on the Internet. The router handles the requests internally.

If a request is made using the browser's address bar for `www.contoso.com/About`, the request fails. No such resource exists on the app's Internet host, so a 404 - Not Found response is returned.

Because browsers make requests to Internet-based hosts for client-side pages, web servers and hosting services must rewrite all requests for resources not physically on the server to the `index.html` page. When `index.html` is returned, the app's Blazor router takes over and responds with the correct resource.

When deploying to an IIS server, you can use the URL Rewrite Module with the app's published `web.config` file. For more information, see the 【29†IIS】 section.

## Hosted deployment with ASP.NET Core

A hosted deployment serves the Blazor WebAssembly app to browsers from an 【30†ASP.NET Core app】 that runs on a web server.

The client Blazor WebAssembly app is published into the `/bin/Release/{TARGET FRAMEWORK}/publish/wwwroot` folder of the server app, along with any other static web assets of the server app. The two apps are deployed together. A web server that is capable of hosting an ASP.NET Core app is required. For a hosted deployment, Visual Studio includes the Blazor WebAssembly App project template (`blazorwasm` template when using the 【31†dotnet new】 command) with the `Hosted` option selected (`-ho|--h

### tool — 2024-01-15T15:08:13.313831+00:00

URL: https://learn.microsoft.com/en-us/samples/dotnet/blazor-samples/blazor-samples/
【0†Skip to main content】

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

【1† Download Microsoft Edge †go.microsoft.com】 【2† More info about Internet Explorer and Microsoft Edge 】

【3† †www.microsoft.com】

Table of contents  Exit focus mode

  Read in English Save 【4† †github.com】 

 Read in English Save 【4† Edit †github.com】

Twitter LinkedIn Facebook Email

Table of contents

# Blazor sample applications

  * Code Sample 
  * 01/12/2024
  * 13 contributors 

【5†Browse code†github.com】 

Samples in this repository accompany the 【6†official Microsoft Blazor documentation】.

To obtain a local copy of the sample apps in this repository, use either of the following approaches:

  * 【7†Fork this repository†docs.github.com】 and 【8†clone it†docs.github.com】 to your local system.
  * Select the Code button. Select Download ZIP to save the repository locally. Extract the saved Zip archive (`.zip`) to access the sample apps.

## Sample app article links

  * Blazor Server with EF Core: 【9†ASP.NET Core Blazor Server with Entity Framework Core (EFCore)】
  * Blazor with SignalR: 【10†Use ASP.NET Core SignalR with Blazor】
  * Blazor WebAssembly scopes-enabled logging: 【11†ASP.NET Core Blazor logging: Client-side log scopes】
  * Blazor WebAssembly with ASP.NET Core Identity: 【12†Blazor WebAssembly with ASP.NET Core Identity】

## Snippet sample apps for article code examples

WARNING: Always follow an article's security guidance when implementing sample code.

Prior to the release of .NET 8, snippet sample apps for Blazor Server and Blazor WebAssembly provide the code examples that appear in Blazor articles. Many of the components in the snippet sample apps compile and run if copied to a local test app. However, the entire snippet sample apps aren't meant to be runnable demonstration sample apps, and not all of the components are completely functional. The purpose of the snippet sample apps prior to .NET 8's release is merely to supply code examples to documentation.

For the release of .NET 8 (and later releases), the sample apps for Blazor Web App and Blazor WebAssembly both supply snippets to articles and are fully working demonstration sample apps. All of the components in these apps function normally.

Blazor snippet sample apps

  * Blazor Web App (.NET 8 or later)
  * Blazor Server (.NET 7.0 or earlier)
  * Blazor WebAssembly

## Community help and support

For more information, see the Support requests section in the 【13†Blazor Fundamentals overview article】.

【14† California Consumer Privacy Act (CCPA) Opt-Out Icon Your Privacy Choices †aka.ms】

Theme

  * Light 
  * Dark 
  * High contrast 

  *   * 【15†Previous Versions】
  * 【16†Blog†techcommunity.microsoft.com】
  * 【17†Contribute】
  * 【18†Privacy†go.microsoft.com】
  * 【19†Terms of Use】
  * 【20†Trademarks†www.microsoft.com】
  * © Microsoft 2023

【14† California Consumer Privacy Act (CCPA) Opt-Out Icon Your Privacy Choices †aka.ms】

Theme

  * Light 
  * Dark 
  * High contrast 

  *   * 【15†Previous Versions】
  * 【16†Blog†techcommunity.microsoft.com】
  * 【17†Contribute】
  * 【18†Privacy†go.microsoft.com】
  * 【19†Terms of Use】
  * 【20†Trademarks†www.microsoft.com】
  * © Microsoft 2023

### tool — 2024-01-15T15:08:13.322137+00:00

* 【8† Code review Manage code changes 】
    * 【9† Issues Plan and track work 】
    * 【10† Discussions Collaborate outside of code 】

Explore
    * 【11† All features 】
    * 【12† Documentation †docs.github.com】
    * 【13† GitHub Skills †skills.github.com】
    * 【14† Blog †github.blog】

  * Solutions 

For
    * 【15† Enterprise 】
    * 【16† Teams 】
    * 【17† Startups 】
    * 【18† Education †education.github.com】

By Solution
    * 【19† CI/CD & Automation 】
    * 【20† DevOps †resources.github.com】
    * 【21† DevSecOps †resources.github.com】

Resources
    * 【22† Learning Pathways †resources.github.com】
    * 【23† White papers, Ebooks, Webinars †resources.github.com】
    * 【24† Customer Stories 】
    * 【25† Partners †partner.github.com】

  * Open Source 

    * 【26† GitHub Sponsors Fund open source developers 】

    * 【27† The ReadME Project GitHub community articles 】

Repositories
    * 【28† Topics 】
    * 【29† Trending 】
    * 【30† Collections 】

  * 【31†Pricing】 

Search or jump to...

# Search code, repositories, users, issues, pull requests...

 Search 

Clear  

【32† Search syntax tips †docs.github.com】 

#  Provide feedback 

We read every piece of feedback, and take your input very seriously.

  Include my email address so I can be contacted

Cancel  Submit feedback 

#  Saved searches 

## Use saved searches to filter your results more quickly

Name 

Query 

To see all available qualifiers, see our 【32†documentation†docs.github.com】. 

Cancel  Create saved search 

【2† Sign in 】 

【33† Sign up 】 

You signed in with another tab or window. 【34†Reload】 to refresh your session. You signed out in another tab or window. 【34†Reload】 to refresh your session. You switched accounts on another tab or window. 【34†Reload】 to refresh your session.   Dismiss alert

{{ message }}

【35† PacktPublishing 】  / 【34†Blazor-WebAssembly-by-Example】  Public

  * 【36† Notifications 】 
  * 【36† Fork 47 】 
  * 【36† Star 71 】 

  * 

Blazor WebAssembly by Example, published by Packt 

### License

【37† MIT license 】 

【38† 71 stars 】 【39† 47 forks 】 【40† Branches 】 【41† Tags 】 【42† Activity 】 

【36† Star 】 

【36† Notifications 】 

  * 【34† Code  】
  * 【43† Issues 0 】
  * 【44† Pull requests 0 】
  * 【45† Actions  】
  * 【46† Security 】
  * 【47† Insights  】

  Additional navigation options  

  * 【34† Code 】 
  * 【43† Issues 】 
  * 【44† Pull requests 】 
  * 【45† Actions 】 
  * 【46† Security 】 
  * 【47† Insights 】 

# PacktPublishing/Blazor-WebAssembly-by-Example

This commit does not belong to any branch on this repository, and may belong to a fork outside of the repository.

## About

Blazor WebAssembly by Example, published by Packt 

### Resources

Readme 

### License

MIT license 

【42† Activity 】 

【48† Custom properties 】 

### Stars

【38† 71 stars 】 

### Watchers

【49† 5 watching 】 

### Forks

【39† 47 forks 】 

【50† Report repository 】 

##  【51† Releases 】

No releases published

##  【52† Packages 0 】

No packages published   

##  【53† Contributors 5 】

  * 【54† 】 
  * 【55† 】 
  * 【56† 】 
  * 【57† 】 
  * 【58† 】 

## Languages

  * 【59† C# 70.7% 】 
  * 【60† HTML 17.3% 】 
  * 【61† CSS 11.1% 】 
  * 【62† JavaScript 0.9% 】 

## Foot

### tool — 2024-01-15T15:08:13.330541+00:00

5. In the Additional information window, select .NET 8.0 (Long Term Support) in the Framework drop-down if not already selected and click the Create button.

When creating a Blazor Web App you can select from various options, like whether to enable authentication, what interactive render modes to enable, and how much of the app you want to be interactive. For this app, make sure the defaults are selected as follows: 

    * Authentication type: None
    * Interactive render mode: Server
    * Interactivity location: Per page/component

[Image 3: Visual Studio additional information dialog showing .NET 8.0 in the Framework drop-down.]

Your project is created and loaded in Visual Studio. Take a look at the contents of your project using Solution Explorer.

[Image 4: Solution Explorer contains a list of folders and files created for your project]

Several files were created to give you a simple Blazor app that is ready to run.

  * `Program.cs` is the entry point for the app that starts the server and where you configure the app services and middleware.
  * `App.razor` is the root component for the app.
  * `Routes.razor` configures the Blazor router.
  * The `Components/Pages` directory contains some example web pages for the app.
  * `BlazorApp.csproj` defines the app project and its dependencies and can be viewed by double-clicking the BlazorApp project node in the Solution Explorer.
  * The `launchSettings.json` file inside the `Properties` directory defines different profile settings for the local development environment. A port number is automatically assigned at project creation and saved on this file.

If everything looks good, select the Continue button below to go to the next step.

In your terminal, run the following command to create your app:

Command prompt Copy 

    dotnet new blazor -o BlazorApp

This command creates your new Blazor Web App project and places it in a new directory called `BlazorApp` inside your current location.

Navigate to the new `BlazorApp` directory created by the previous command:

Command prompt Copy 

    cd BlazorApp

Take a quick look at the contents of the `BlazorApp` directory.

Command prompt Copy 

    ls

Several files were created in the `BlazorApp` directory, to give you a simple Blazor app that is ready to run.

  * `Program.cs` is the entry point for the app that starts the server and where you configure the app services and middleware.
  * `App.razor` is the root component for the app.
  * `Routes.razor` configures the Blazor router.
  * The `Components/Pages` directory contains some example web pages for the app.
  * `BlazorApp.csproj` defines the app project and its dependencies.
  * The `launchSettings.json` file inside the `Properties` directory defines different profile settings for the local development environment. A port number is automatically assigned at project creation and saved on this file.

Take note of the `BlazorApp` directory path as you will use it later in the tutorial.

If everything looks good, select the Continue button below to go to the next step.

## Run your app

Click on the Start Debugging button (green arrow) in the Debug Toolbar in Visual Studio to run your app.

[Image 5: The toolbar contains a shortcut button to the same command available through the menu Debug | Start Debugging (F5)]

Once the app is running, you can apply code changes to the running app by clicking the Hot Reload button.

[Image 6: The toolbar contains a shortcut button to the same command available through the menu Debug | Hot Reload (Alt + F10)]

You can stop the app at any time by clicking on the Stop button in the top toolbar.

[Image 7: The toolbar contains a shortcut button to the same command available through the menu Debug | Stop Debugging (Shift + F5)]

The first time you run a web app in Visual Studio, it will set up a development certificate for hosting the app over HTTPS and then prompt you to trust the certificate. We recommend agreeing to trust the certificate. The certificate will only be used for local development, and without it most browsers will complain about the security of the website.

Wait for the app to launch in the browser. Once you get to the following page, you have successfully run your first Blazor app!

In your terminal, run the following command:

Command prompt Copy 

    dotnet watch

The `dotnet watch` command will build and start the app, and then update the app whenever you make code changes. You can stop the app at any time by selecting `Ctrl`+`C`.

Wait for the app to display that it's listening on http://localhost:<port number> and for the browser to launch at that address.

Wait for the app to display tha

### assistant — 2024-01-15T15:08:13.343700+00:00

Blazor WebAssembly is a web framework that allows you to build interactive web applications using C# and .NET, with the application running directly in the browser via WebAssembly. When working with Blazor WebAssembly, there are several common processes and aspects you should be aware of, along with examples that can help guide your development process.

### Common Processes and Aspects

1. **Handling Boot Resources**: In a standalone Blazor WebAssembly app, you often need to manage boot resources. For example, you might need to load resources dynamically based on the type (like 'dotnetwasm' for WebAssembly) and handle decompression (like using BrotliDecode for compressed resources)【6†source】.

2. **Routing and URL Rewriting**: Blazor WebAssembly handles routing differently compared to server-side apps. For instance, you need to ensure that requests for client-side pages are correctly rewritten to `index.html` so that the Blazor router can then take over and serve the correct resource【6†source】.

3. **Hosted Deployment with ASP.NET Core**: When deploying a Blazor WebAssembly app, you can opt for a hosted deployment where the Blazor app is served from an ASP.NET Core app. This requires setting up the client app within the `/bin/Release/{TARGET FRAMEWORK}/publish/wwwroot` folder of the server app, and both apps are deployed together【6†source】.

### Sample Applications and Examples

1. **Microsoft's Official Samples**: Microsoft provides a repository of Blazor sample applications that are aligned with their official documentation. These samples can be accessed by cloning the repository or downloading it as a ZIP file. They include examples like Blazor Server with EF Core, Blazor with SignalR, and Blazor WebAssembly scopes-enabled logging【7†source】.

2. **Blazor WebAssembly by Example (GitHub)**: A GitHub repository titled "Blazor WebAssembly by Example" published by Packt includes practical projects that can help you start building web applications using Blazor WebAssembly and .NET. This resource is particularly useful for hands-on learning through practical examples【8†source】.

3. **Creating a Simple Blazor App**: For a basic start, you can create a simple Blazor Web App using Visual Studio. The process involves selecting options like authentication type, interactive render mode, and interactivity location. The project includes essential components like `Program.cs` for the entry point, `App.razor` as the root component, `Routes.razor` for configuring the router, and a `Components/Pages` directory for web pages【9†source】.

These examples and guidelines can serve as a starting point for developing your Blazor WebAssembly applications. As you progress, you may find more specific examples and templates that match the particular needs of your project.
