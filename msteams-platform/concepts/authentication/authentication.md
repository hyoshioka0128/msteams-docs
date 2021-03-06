---
title: Authenticate a user in Teams
description: Describes authentication in Teams and how to use it in your apps
keywords: teams authentication OAuth SSO AAD
---
# Authentication in Teams

> [!Note]
> Authentication on mobile clients requires version 1.4.1 or later of the Teams JavaScript SDK.

In order for your app to access user information stored in Azure Active Directory, as well as access data from other services like Facebook and Twitter, your app will have to establish a trusted connection with those providers. The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) supports this in a way that allows your apps to work both in the web and desktop versions of Teams. (Currently, app authentication from iOS and Android is somewhat different, but much of what's described here does, or soon will, work on mobile devices as well.)

## Use the OAuthCard for easier authentication

The Azure Bot Service’s OAuthCard has been recently introduced to make authentication easier for apps using bots. For more information on using the OAuthCard See:

* [Using the OAuthCard](~/concepts/authentication/auth-oauth-card.md)

The other topics in this section describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.

## General authentication information

Authentication flow as it applies to any authentication provider:

* [Authentication flow in tabs](~/concepts/authentication/auth-flow-tab.md) describes how tab authentication works in Teams. This shows a typical web based authentication flow used for tabs.
* [Authentication flow in bots](~/concepts/authentication/auth-flow-bot.md) describes how authentication works within a bot in your app in Teams. This shows a non-web based authentication flow used for bots on all versions of Teams (web, desktop app, and mobile apps)

## Authentication in Azure Active Directory

Detailed implementation walkthroughs for authentication using Azure Active Directory (Azure AD):

* [Azure AD authentication in tabs](~/concepts/authentication/auth-tab-AAD.md) describes how to connect to Azure Active Directory from within a tab in your app in Teams.
* [Azure AD authentication in bots](~/concepts/authentication/auth-bot-AAD.md) describes how to connect to Azure Active Directory from within a bot in your app in Teams.
* [Silent authentication (Azure AD)](~/concepts/authentication/auth-silent-AAD.md) describes how to implement single sign on (SSO) in your app using Azure Active Directory. Currently SSO only works for tabs.

## Samples

Sample code showing bot authentication in Node:

* [Microsoft Teams bot authentication sample](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

Sample code showing tab authentication for C# and Node:

* [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Microsoft Teams tab authentication sample (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)
