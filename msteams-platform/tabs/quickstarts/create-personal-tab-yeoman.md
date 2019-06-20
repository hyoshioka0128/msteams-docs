---
title: "Quickstart: Create a Personal Tab with the Teams Yeoman Generator"
author: laujan 
description: A quickstart guide to creating a personal tab with the Teams Yeoman Generator. 
ms.topic: quickstart 
ms.author: laujan
---
# Quickstart: Use the Teams Yeoman Generator to create a Node.js custom personal tab

>[!NOTE]
>This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.

Teams custom tabs enable you to embed web-based content directly into Microsoft Teams via your [Teams App Package](/msteams-platform/_old/concepts/apps/apps-package.md) (see [What are custom tabs in Microsoft Teams?](/msteams-platform/tabs/what-are-custom-tabs.md)). There are two types of tabs available in Teams - channel/group and personal. Custom tabs can be scoped for either channel/group use, serving dynamic content, or personal use, serving static content. An app can have one channel/group tab and up to sixteen personal tabs.

In this quickstart we will walk-through creating a custom personal tab using the [Microsoft Teams App Project Generator](/OfficeDev/generator-teams). For more information, see the Microsoft Teams App [Project Structure](/OfficeDev/generator-teams/wiki/Project-Structure) documentation.

[!INCLUDE [create-custom-tab-node-js-common](../../includes/create-custom-tab-node-js-common.md)]

## Create your personal tab

Adding a personal tab to your app project requires creating a content page and adding few lines of code to the existing project files:

> 1.&emsp; In your code editor, create a new HTML file named, `static.html` .  Add the following code:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>
            <!-- Todo: add your a title here -->
        </title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- inject:css -->
        <!-- endinject -->
    </head>
        <body>
            <h1>Static Tab</h1>
            <p><img src="/assets/icon.png"></p>
            <p>This is your personal tab!</p>
        </body>
</html>

```

> 2.&emsp;Save the `static.html` file in your app's `web` folder. The relative file path should be: <br>&emsp;`./src/app/web/<yourDefaultTabNameTab>/static.html`<br>

> 3.&emsp; In your code editor, navigate to your app's `manifest.json` file: `./src/manifest/manifest.json/` . Scroll down to the empty staticTabs array ( `"staticTabs":[]` ) and add the following JSON object:

```json
{
    "entityId": "staticTab",
    "name": "Static Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/static.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

> [!TIP]
> Remember to update the `"contentURL"` path component in the the staticTabs JSON object with `<yourDefaultTabNameTab>` using your *DefaultTabName* + *Tab*.

> 4.&emsp; Save the updated `manifest.json` file.

> 5.&emsp; Your content page must be served in an iFrame. Open your app's `Tab.ts` TypeScript file in your code editor: `./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts` and add the following to the list of iFrame decorators:

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/static.html")
```

> 6.&emsp; *Save* the updated `Tab.ts` file and *Save all* for good measure.

> [!NOTE]
> Open a command prompt in your app's project folder to complete the project's gulp tasks.

## Create a Teams App manifest

Now that your tab code is complete, you can build your project:
>The [Teams Manifest](foo.md) will be part of your app package zip file (along with your two app icons) and will be uploaded into Microsoft Teams. This is achieved through a gulp task that validates the manifest and creates the zip file in the `./package` folder. In the command prompt, type the following:

```bash
gulp manifest
```

## Build your app

>The build command compiles your solution into the `./dist` folder. In the command prompt, type the following:

```bash
gulp build
```

## Run your app in localhost

>To build and start a local web server, in the command prompt, type the following:

```bash
gulp serve
```

>Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your app's home page.

>To view your personal tab, remain in the current browser and add `static.html` to the app's file path: `http://localhost:3007/<yourDefaultAppNameTab>/static.html` Press Enter.<br>

>>![personal tab screenshot](/microsoftteams/platform/assets/personalTab.PNG)

## Package your app for Microsoft Teams

Microsoft Teams is an entirely cloud-based product, and thus requires your app to be available from the cloud using HTTPS endpoints. Teams does not allow apps to be hosted on localhost. Therefore, you need to either publish your app to a public URL or use a proxy which will expose your local port to an internet-facing URL.

To test your tab extension we will use [ngrok](https://ngrok.com/docs), which is built into this project. Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints. Your server's web endpoints will be available during the current session on your local machine. When the machine is shut down or goes to sleep the service will no longer be available.

>In your command prompt, enter the following:

```bash
gulp ngrok-serve
```

## Upload your app in Microsoft Teams

- Open Microsoft Teams. In the **YourTeams** panel click (**&#8943;**) *More options* next to the team that you are using to test your app's tabs and Select *Manage team*. 
- In the main panel click on *Apps* from the tab bar and click on *Upload a custom app* located in the lower right-hand corner of the page. 
- Open your project folder, browse to the `./package` folder, select the zip file in the `./package` folder, right-click, and choose open. 
- Your app will upload into Microsoft Teams.

## View your personal tabs

- In the navbar located at the far-left of the Teams App, click (**&#8943;**) *More added apps*. You will be presented with a list of personal view apps.
- Select your app's personal tab from the list to view.

### Nice work! You just extended Microsoft Teams with custom tabs.