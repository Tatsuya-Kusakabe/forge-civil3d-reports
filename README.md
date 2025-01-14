# Extract alignment names and export report - Civil 3D

![Platforms](https://img.shields.io/badge/Webapp-Windows|MacOS|Linux-lightgray.svg)
![.NET Core](https://img.shields.io/badge/.NET%20Core-3.0-blue.svg)
[![ASP.NET Core](https://img.shields.io/badge/ASP.NET%20Core-3.0-blue.svg)](https://asp.net/)

[![oAuth2](https://img.shields.io/badge/oAuth2-v1-green.svg)](http://developer.autodesk.com/)
[![Data-Management](https://img.shields.io/badge/Data%20Management-v1-green.svg)](http://developer.autodesk.com/)
[![Design-Automation](https://img.shields.io/badge/Design%20Automation-v3-green.svg)](http://developer.autodesk.com/)
[![Viewer](https://img.shields.io/badge/Viewer-v7-green.svg)](http://developer.autodesk.com/)

![Platforms](https://img.shields.io/badge/Plugins-Windows-lightgray.svg)
![.NET](https://img.shields.io/badge/.NET%20Framework-4.7.2-blue.svg)
[![Civil 3D](https://img.shields.io/badge/Civil%203D-2021-lightblue.svg)](http://developer.autodesk.com/)

![Intermediate](https://img.shields.io/badge/Level-Intermediate-green.svg)
[![License](http://img.shields.io/:license-MIT-blue.svg)](http://opensource.org/licenses/MIT)

# Description

This sample demonstrates using Design Automation with Civil 3D support included in the AutoCAD engine. User can select a DWG file hosted on BIM 360 Document Manager (or A360) and view using the Forge Viewer.

Once the file is loaded, in the background, a Design Automation workitem will run a .NET plugin to extract alignment names from the file. When ready, the information will be visible on the property panel.

When one of alignment names is selected, in the background, , a Design Automation workitem will run again to export alignment report. When ready, the excel sheet is automatically downloaded. 

This sample is based on the [Learn Forge](http://learnforge.autodesk.io) tutorials (`View hubs` section).

This sample is forked from [Extract style information - Civil 3D](https://github.com/Autodesk-Forge/forge-civil3d-properties) samples.

# Thumbnail

![thumbnail](/thumbnail.gif)

# Setup

## Prerequisites

1. **Forge Account**: Learn how to create a Forge Account, activate subscription and create an app at [this tutorial](http://learnforge.autodesk.io/#/account/). 
2. **Visual Studio**: Either Community (Windows) or Code (Windows, MacOS). 
3. **.NET Core** basic knowledge with C#
4. **ngrok**: Routing tool, [download here](https://ngrok.com/)
7. **Civil 3D** 2021: required to compile changes into the plugin. Windows only.

For using this sample, you need an Autodesk developer credentials. Visit the [Forge Developer Portal](https://developer.autodesk.com), sign up for an account, then [create an app](https://developer.autodesk.com/myapps/create) that uses Data Management and Model Derivative APIs. For this new app, use `http://localhost:3000/api/forge/callback/oauth` as Callback URL, although is not used on 2-legged flow. Finally take note of the **Client ID** and **Client Secret**.

## Running locally

Clone this project or download it. It's recommended to install [GitHub desktop](https://desktop.github.com/). To clone it via command line, use the following (**Terminal** on MacOSX/Linux, **Git Shell** on Windows):

    git clone https://github.com/Tatsuya-Kusakabe/forge-civil3d-reports


**Visual Studio** (Windows):

Right-click on the project, then go to **Debug**. Adjust the settings as shown below. 

`FORGE_CALLBACK_URL` also has to be written as described in **Environment variables** section.

![](readme/visual_studio_settings.png)

**Visual Studio Code** (Windows, MacOS):

Open the folder, at the bottom-right, select **Yes** and **Restore**. This restores the packages (e.g. Autodesk.Forge) and creates the launch.json file. See *Tips & Tricks* for .NET Core on MacOS.

![](readme/visual_code_restore.png)

**7-Zip**

The **Post-build** event in Visual Studio uses 7-Zip to automatically build and copy AppBundle. 7-Zip has to be installed under the %PROGRAMFILES% folder.

**IIS**

IIS (Internet Information Services) has to be activated from Windows Control Panel.

**ngrok**

Run `ngrok http 3000 -host-header="localhost:3000"` to create a tunnel to your local machine, then copy the address into the `FORGE_WEBHOOK_URL` environment variable.

**Environment variables**

At the `.vscode\launch.json`, find the env vars and add your Forge Client ID, Secret and callback URL. Also define the `ASPNETCORE_URLS` variable. The end result should be as shown below:

```json
"env": {
    "ASPNETCORE_ENVIRONMENT": "Development",
    "ASPNETCORE_URLS" : "http://localhost:3000",
    "FORGE_CLIENT_ID": "your id here",
    "FORGE_CLIENT_SECRET": "your secret here",
    "FORGE_CALLBACK_URL": "http://localhost:3000/api/forge/callback/oauth",
    "FORGE_WEBHOOK_URL": "your ngrok address here: e.g. http://abcd1234.ngrok.io"
},
```

**Civil 3D plugin**

A compiled version of the `Civil 3D` plugin (.bundles) is included on the `webapp` module, under `wwwroot/bundles` folder. Any changes on these plugins will require to create a new .bundle, the **Post-build** event should create it.

Start the app.

Open `http://localhost:3000` to start the app, select a DWG file. The demo thumbnail shows you how to navigate.

## Deployment

To deploy this application to Heroku, the **Callback URL** for Forge must use your `.herokuapp.com` address. After clicking on the button below, at the Heroku Create New App page, set your Client ID, Secret and Callback URL for Forge.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

# Further Reading

Documentation:

- [BIM 360 API](https://developer.autodesk.com/en/docs/bim360/v1/overview/) and [App Provisioning](https://forge.autodesk.com/blog/bim-360-docs-provisioning-forge-apps)
- [Data Management API](https://developer.autodesk.com/en/docs/data/v2/overview/)
- [Viewer](https://developer.autodesk.com/en/docs/viewer/v7) 
- [Design Automation](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/overview/)

### Troubleshooting

1. **Cannot see my BIM 360 projects**: Make sure to provision the Forge App Client ID within the BIM 360 Account, [learn more here](https://forge.autodesk.com/blog/bim-360-docs-provisioning-forge-apps). This requires the Account Admin permission.

2. **error setting certificate verify locations** error: may happen on Windows, use the following: `git config --global http.sslverify "false"`

## License

This sample is licensed under the terms of the [MIT License](http://opensource.org/licenses/MIT). Please see the [LICENSE](LICENSE) file for full details.

## Written by

Augusto Goncalves [@augustomaia](https://twitter.com/augustomaia), [Forge Partner Development](http://forge.autodesk.com)
