# Fly Manager

Reference implementaion of Portable Fly Manager for managing <a href="https://fly.io">fly.io</a> machines to run in servers, desktops and mobile.

Demo Hosted version is in <a href="https://guiapp.fly.dev">https://guiapp.fly.dev</a> (Will be periodically reinstalled)

Docker Image is <a href="https://hub.docker.com/r/arshucs/guiapp">arshucs/guiapp</a>

Source of the Web UI is in the current repository under wwwroot folder of linux64_musl folder.

![Manage Fly Machines](Screenshot.png) "Portable Fly Manager for Managing Fly Machines".

## Configure with Own Admin User

    1. Configure the appconfig.json as below to stop loading the cached Embedded AppSites

    {
      "AssetTypeName": "AppWeb.Web.AssetRegister",
      "AssetDll": "AppWeb.Web.dll",
      "IsEnabled": false
    }

    2. Remove the Members.dat/Roles.dat from wwwroot\App_Data Folder

    3. Once the above action are done packaging the runtime in docker will on launch will prompt for the initial admin user id and password.
