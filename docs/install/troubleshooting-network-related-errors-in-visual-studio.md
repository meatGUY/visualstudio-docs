---
title: "Troubleshoot network or proxy errors"
description: "Find solutions for network- or proxy-related errors that you might encounter when you install or use Visual Studio behind a firewall or a proxy server."
ms.date: 05/22/2019
ms.topic: troubleshooting
helpviewer_keywords:
  - "network installation, Visual Studio"
  - "administrator guide, Visual Studio"
  - "installing Visual Studio, administrator guide"
  - "list of domains, locations, URLs, Visual Studio"
  - "proxy errors, Visual Studio"
ms.assetid:
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
  - "multiple"
ms.prod: visual-studio-windows
ms.technology: vs-installation
---
# Troubleshooting network-related errors when you install or use Visual Studio

We've got solutions for the most typical network- or proxy-related errors that you might encounter when you install or use Visual Studio behind a firewall or a proxy server.

## Error: “Proxy authorization required”

This error generally occurs when users are connected to the internet through a proxy server, and the proxy server blocks the calls that Visual Studio makes to some network resources.

### To fix this proxy error

- Restart Visual Studio. A proxy authentication dialog box should appear. Enter your credentials when prompted in the dialog.

- If restarting Visual Studio does not solve the problem, it might be that your proxy server does not prompt for credentials for http:&#47;&#47;go.microsoft.com addresses but does so for &#42;.visualStudio.microsoft.com addresses. For these servers, consider adding the following URLs to an allow list to unblock all sign-in scenarios in Visual Studio:

  - &#42;.windows.net

  - &#42;.microsoftonline.com

  - &#42;.visualstudio.microsoft.com

  - &#42;.microsoft.com

  - &#42;.live.com

- You can otherwise remove the http:&#47;&#47;go.microsoft.com address from the allow list so that the proxy authentication dialog shows up for both the http:&#47;&#47;go.microsoft.com address and the server endpoints when Visual Studio is restarted.

  -OR-

- If you want to use your default credentials with your proxy, you can perform the following actions:

::: moniker range="vs-2017"

  1. Find **devenv.exe.config** (the devenv.exe configuration file) in: **%ProgramFiles%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE** or **%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE**.

  2. In the configuration file, find the `<system.net>` block, and then add this code:

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      You must insert the correct proxy address for your network in `proxyaddress="<http://<yourproxy:port#>`.

     > [!NOTE]
     > For more information, see the [&lt;defaultProxy&gt; Element (Network Settings)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/) and [&lt;proxy&gt; Element (Network Settings)](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings) pages.

::: moniker-end

::: moniker range="vs-2019"

  1. Find **devenv.exe.config** (the devenv.exe configuration file) in: **%ProgramFiles%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE** or **%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE**.

  2. In the configuration file, find the `<system.net>` block, and then add this code:

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      You must insert the correct proxy address for your network in `proxyaddress="<http://<yourproxy:port#>`.

     > [!NOTE]
     > For more information, see the [&lt;defaultProxy&gt; Element (Network Settings)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/) and [&lt;proxy&gt; Element (Network Settings)](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings) pages.

::: moniker-end

## Error: “The underlying connection was closed”

If you are using Visual Studio in a private network that has a firewall, Visual Studio might not be able to connect to some network resources. These resources can include Azure DevOps Services for sign-in and licensing, NuGet, and Azure services. If Visual Studio fails to connect to one of these resources, you might see the following error message:

  **The underlying connection was closed: An unexpected error occurred on send**

Visual Studio uses Transport Layer Security (TLS) 1.2 protocol to connect to network resources. Security appliances on some private networks block certain server connections when Visual Studio uses TLS 1.2.

### To fix this connection error

Enable connections for the following URLs:

- https:&#47;&#47;management.core.windows.net

- https:&#47;&#47;app.vssps.visualstudio.com

- https:&#47;&#47;login.microsoftonline.com

- https:&#47;&#47;login.live.com

- https:&#47;&#47;go.microsoft.com

- https:&#47;&#47;graph.windows.net

- https:&#47;&#47;app.vsspsext.visualstudio.com

- &#42;.azurewebsites.net (for Azure connections)

- &#42;.visualstudio.microsoft.com

- cdn.vsassets.io (hosts content delivery network, or CDN, content)

- &#42;.gallerycdn.vsassets.io (hosts Azure DevOps Services extensions)

- static2.sharepointonline.com (hosts resources that Visual Studio uses in the Office UI Fabric kit, such as fonts)

- &#42;.nuget.org (for NuGet connections)

  > [!NOTE]
  > Privately owned NuGet server URLs may not be included in this list. You can check for the NuGet servers that you are using in %APPData%\Nuget\NuGet.Config.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## See also

* [Install and use Visual Studio behind a firewall or proxy server](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Visual Studio administrator guide](visual-studio-administrator-guide.md)
* [Install Visual Studio](install-visual-studio.md)
