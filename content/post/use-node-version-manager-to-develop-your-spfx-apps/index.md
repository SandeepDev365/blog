---
title: "Use Node Version Manager to develop your SPFx apps"
date: 2021-02-14T08:40:00-04:00
author: "Toni Pohl"
githubname: tonipohl
categories: ["Community post"]
tags: []
type: "regular"
images: 
- images/p6.png
summary: "To develop applications for SharePoint or Microsoft Teams with the SPFx framework, a few requirements must be met on your development computer. Learn how to install the supported Node.js v10.x version and how you can use other Node.js versions additionally with Node Version Manager"
---

To develop applications for SharePoint or Microsoft Teams with the [SPFx
framework](https://docs.microsoft.com/sharepoint/dev/spfx/sharepoint-framework-overview "Overview of the SharePoint Framework"),
a few requirements must be met on your development computer. Learn how
to install the supported Node.js v10.x version and how you can use other
Node.js versions additionally with Node Version
Manager!

## Why? 

As developer, it often makes sense to have multiple versions of a
framework installed on a single computer. For developing an app for
SharePoint Server 2019 or SharePoint Online with the SPFx framework, you
need to have **Node.js LTS v10.x.x** installed (LTS stands for Long Time
Support). You can find all the requirements at [Set up your SharePoint
Framework development
environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment). For
developing other web applications, e.g. when using frameworks such
as Angular, you might need other versions of Node.js installed.

The solutions for operation with several different versions of Node.js
are supplied with the **Node Version Manager (NVM)**. Here is a
step-by-step guide on how to remove old versions of Node.js, how to
install NVM and desired Node.js versions, and how to switch between the
Node.js versions. After the installation process, learn how to develop
your custom SharePoint app using the provided tools.

## Install nvm and Node.js 

First, follow the steps here to install the Node.js frameworks on your
machine. Alternatively, there´s a good description at [Set up your
Node.js development environment directly on
Windows](https://docs.microsoft.com/windows/nodejs/setup-on-windows "https://docs.microsoft.com/windows/nodejs/setup-on-windows").

If you already have installed other Node.js versions, it´s a good idea
to remove existing versions in the Windows Apps & Features settings.
When you have a later version, such as 14.5, already installed, it´s
usually not required to uninstall this version. nvm finds that version
and allows to use it with nvm.

{{< image alt="p1.png" src="images/p1.png" >}}

Alternatively, when you have [chocolatey](https://chocolatey.org/)
installed, you can run

```bash
choco uninstall nodejs -y
```

(as I did on my machine to cleanup.)

{{< image alt="p2.png" src="images/p2.png" >}}

You can install nvm from [Node Version Manager (nvm) for
Windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows "https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows")
by Corey Butler. The latest version is [nvm
v1.1.7](https://github.com/coreybutler/nvm-windows/releases/tag/1.1.7 "https://github.com/coreybutler/nvm-windows/releases/tag/1.1.7").
Download
[nvm-setup.zip](https://github.com/coreybutler/nvm-windows/releases/download/1.1.7/nvm-setup.zip "https://github.com/coreybutler/nvm-windows/releases/download/1.1.7/nvm-setup.zip")
and run it. Or, you can use choco (if installed on your computer):\
*choco install nvm -y*

Let´s check if nvm is working:

```bash
nvm ls
```

should find no Node.js versions.


{{< image alt="p3.png" src="images/p3.png" >}}

To see the latest Node.js versions check <https://nodejs.org/en/>, or
simply run

```bash
nvm ls available
```

{{< image alt="List available Node.js versions" src="images/p4.png" >}}

Now, install the desired Node.js versions:

```bash
nvm install 10.23.0
```

{{< image alt="p5.png" src="images/p5.png" >}}

```bash
nvm install 14.15.4
```

{{< image alt="p6.png" src="images/p6.png" >}}

Etc. For the latest Node.js version, simply run

```bash
nvm install latest
```

Now check the installed versions: 

```bash
nvm ls
```

{{< image alt="p7.png" src="images/p7.png" >}}

You can now switch between versions with nvm. Use \<nvm version>, e.g.

```bash
nvm use 10.23.0
```

or

```bash
nvm use 14.15.4
```

That´s the basic installation of Node.js and
[npm](https://www.npmjs.com/get-npm).

## Install the SPFx development tools once 

To install the required tools
[yo](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment#install-yeoman)
*with the sharepoint generator* and
[gulp](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment#install-gulp)
and for SharePoint development, we follow the steps at [Set up your
SharePoint Framework development
environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).
Here are the commands to run in a PowerShell console: First, switch to
Node.js v10, confirm, (check the current version), and install the tools
with npm.

```bash
nvm use 10.23.0
npm install gulp yo @microsoft/generator-sharepoint --global
```

{{< image alt="npm install" src="images/p8.png" >}}

## Create a new SPFx web part 

To create a new SPFx app, follow the steps described at [Build your
first SharePoint client-side web part (Hello World part
1)](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part "https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part").
In a new directory, run

```bash
yo @microsoft/sharepoint
```

{{< image alt="Run yo" src="images/p9.png" >}}

You need to trust the development self-signed SSL certificate as
described at [Trusting the self-signed developer
certificate](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment#trusting-the-self-signed-developer-certificate)
here. Then, you can open the workbench with SSL.

```bash
gulp trust-dev-cert
```


{{< image alt="gulp trust-dev-cert" src="images/p10.png" >}}

You can open Visual Studio Code now to modify the solution: *code .*

## Run the SPFx web part 

The generated solution includes the sample app that can now be modified.

{{< image alt="Coding\..." src="images/p11.png" >}}
When done, let´s open the default browser with the gulp webserver:

```bash
gulp serve
```

This opens the SPFx workbench, in our sample at
`https://localhost:4321/temp/workbench.html`. Here, you can add the
web part to the workbench page and test it.


{{< image alt="Use the workbench to run the web part" src="images/p12.png" >}}

**Tip:** When gulp serve is running, you can open your M365 tenant´s SPO
site and use the custom web part with the data from SharePoint, too:
[https://\<tenant>.sharepoint.com/sites/\<sitename>/\_layouts/15/workbench.aspx](https://%3ctenant%3e.sharepoint.com/sites/%3Csitename%3E/_layouts/15/workbench.aspx)

## Deploy the SPFx solution 

To build the ready-to-use solution, run

```bash
gulp bundle --ship
```

to build the package for the correct folder and

```bash
gulp package-solution --ship
```

to create the `\sharepoint\solution\<project>.sppkg` file that can
be uploaded to the [SharePoint App
catalog](https://docs.microsoft.com/sharepoint/use-app-catalog?redirectSourcePath=%252farticle%252fuse-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-0b6ab336-8b83-423f-a06b-bcc52861cba0).

## Develop the solution 

You can follow the next steps to develop the app described here:

-   [Build your first SharePoint client-side web part (Hello World part
    1)](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part "https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part")

-   [Connect your client-side web part to SharePoint (Hello World part
    2)](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/connect-to-sharepoint "https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/connect-to-sharepoint")

-   [Deploy your client-side web part to a SharePoint page (Hello World
    part
    3)](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/connect-to-sharepoint "https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/connect-to-sharepoint")

-   [Host your client-side web part from Microsoft 365 CDN (Hello World
    part
    4)](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/hosting-webpart-from-office-365-cdn "https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/hosting-webpart-from-office-365-cdn")

## Switch as required with nvm

The Node Version Manager helps to work with multiple versions of Node.js
for different purposes on the same machine. I hope this tip helps
developers for a productive development environment!
Happy
developing!

[This blog article is a repost from
blog.atwork.at.](https://blog.atwork.at/post/Use-nvm-for-multiple-nodejs-versions "blog.atwork.at")
 