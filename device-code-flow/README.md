---
# Metadata required by https://docs.microsoft.com/samples/browse/
# Metadata properties: https://review.docs.microsoft.com/help/contribute/samples/process/onboarding?branch=main#add-metadata-to-readme
languages:
- PowerShell
page_type: sample
name: PowerShell console application that makes a request to the Graph API via the Device Code flow
description: This PowerShell console application uses the device code flow for authentication and then makes a request to Microsoft Graph for the user's profile data.
products:
- azure
- azure-active-directory
- ms-graph
urlFragment: ms-identity-docs-code-app-device-code-powershell
---

<!-- SAMPLE ID: DOCS-CODE-031 -->
# PowerShell | console | user sign-in, protected web API access (Microsoft Graph) | Microsoft identity platform

<!-- Build badges here
![Build passing.](https://img.shields.io/badge/build-passing-brightgreen.svg) ![Code coverage.](https://img.shields.io/badge/coverage-100%25-brightgreen.svg) ![License.](https://img.shields.io/badge/license-MIT-green.svg)
-->

This PowerShell console application authenticates a user via the device code flow, and then makes a request to the Graph API as the authenticated user. The response to the request is printed to the terminal.

```console
.\app.ps1
Checking cache for existing accounts.
No cached accounts found.
Initiating a Device Code Flow.
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code XXXXXXXXX to authenticate.

{
  @odata.context    : https://graph.microsoft.com/v1.0/$metadata#users/$entity
  businessPhones    : {+1 (999) 5551001}
  displayName       : Contoso Employee
  givenName         : Contoso
  jobTitle          : Worker
  mail              : cemployee@contoso.com
  mobilePhone       : 1 999-555-1001
  officeLocation    : Contoso Plaza/F30
  preferredLanguage :
  surname           : Employee
  userPrincipalName : contoso_employee@contoso.com
  id                : 5a55a5dd-1a60-3989-413b-116087b0b941
}
```

## Prerequisites

- Azure Active Directory (Azure AD) tenant and the permissions or role required for managing app registrations in the tenant.
- PowerShell 7+

## Setup

### 1. Register the app

First, complete the steps in [Register an application with the Microsoft identity platform](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app) to register the application.

Use these settings in your app registration.

| App registration <br/> setting    | Value for this sample app                                                    | Notes                                                                                              |
|---------------------------------:|:-----------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------|
| **Name**                          | `PowerShell Device Code Flow App`                                            | Suggested value for this sample. <br/> You can change the app name at any time.                    |
| **Supported account types**       | **Accounts in this organizational directory only (Single tenant)**           | Suggested value for this sample.                                                                   |
| **Platform type**                 | _None_                                                                       | No redirect URI required; don't select a platform.                                                 |
| **Allow public client flows**     | **Yes**                                                                      | Required value for this sample.                                                                    |

> :information_source: **Bold text** in the table above matches (or is similar to) a UI element in the Azure portal, while `code formatting` indicates a value you enter into a text box in the Azure portal.

### 2. Update code sample with app registration values

```powershell
# 'Application (client) ID' of app registration in Azure portal - this value is a GUID
$ClientId = ""

# 'Directory (tenant) ID' of app registration in Azure portal - this value is a GUID
$TenantId = ""
```

### 3. Install package(s)

Install the MSAL.NET libraries in PowerShell:

```console
Install-Package Microsoft.Identity.Client
```

## Run the application

```console
.\app.ps1
```

Follow the device code flow instructions that are presented. If everything worked, you should receive a response similar to this:

```console
{
  @odata.context    : https://graph.microsoft.com/v1.0/$metadata#users/$entity
  businessPhones    : {+1 (999) 5551001}
  displayName       : Contoso Employee
  givenName         : Contoso
  jobTitle          : Worker
  mail              : cemployee@contoso.com
  mobilePhone       : 1 999-555-1001
  officeLocation    : Contoso Plaza/F30
  preferredLanguage :
  surname           : Employee
  userPrincipalName : contoso_employee@contoso.com
  id                : 5a55a5dd-1a60-3989-413b-116087b0b941
}
```

## About the code

This PowerShell console application prompts the user to sign in via their device using a code provided by Microsoft Authentication Library (MSAL).  Upon running the script, DeviceCodeHelper will poll the server to check for a successful authentication with the provided code.  Upon successful authentication, the script then makes an HTTP GET request to the Microsoft Graph /me endpoint with the user's access token in the HTTP header.  The response from the GET request is then displayed to the console.

## Reporting problems

### Sample app not working?

If you can't get the sample working, you've checked [Stack Overflow](http://stackoverflow.com/questions/tagged/msal), and you've already searched the issues in this sample's repository, open an issue report the problem.

1. Search the [GitHub issues](../../issues) in the repository - your problem might already have been reported or have an answer.
1. Nothing similar? [Open an issue](../../issues/new) that clearly explains the problem you're having running the sample app.

### All other issues

> :warning: WARNING: Any issue in this repository _not_ limited to running one of its sample apps will be closed without being addressed.

For all other requests, see [Support and help options for developers | Microsoft identity platform](https://docs.microsoft.com/azure/active-directory/develop/developer-support-help-options).

## Contributing

If you'd like to contribute to this sample, see [CONTRIBUTING.MD](/CONTRIBUTING.md).

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information, see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
