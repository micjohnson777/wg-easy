---
title: "Installing WG Easy in TrueNAS SCALE"
---

{{< toc >}}

TrueNAS SCALE is an open source storage platform based on Debian Linux that is free to download and use. 
For information on TrueNAS SCALE click [here](https://www.truenas.com/truenas-scale/).

To download the latest public release of SCALE, click [here](https://www.truenas.com/download-truenas-scale/). 
For information on installing and using SCALE, see [Getting Started](https://www.truenas.com/docs/scale/gettingstarted/).  

TrueNAS SCALE deploys the WG Easy app in a Kubernetes container (pod). 
When updates become available, SCALE displays an update badge on the app on the **Installed Application** screen. 
To update to the latest release, click **Update** or **Update All** and SCALE takes care of the update process. 

WG Easy is the easiest way to install and manage WireGuard on any Linux host.
It provides a pre-configured environment with all the necessary components and a web-based user interface to manage VPN connections.
The application is included in the TrueNAS SCALE community catalog of applications.

## First Steps
WG Easy does not require advance preparation to install the application in SCALE. 

If customizing the application, have the DNS server configured and the list of any IP addresses ready to add to the application. See [Network Configuration](#networking-settings) below for details on network configuration setting options.

Allow the WG Easy application to create the storage volumes during the installation, or create the dataset(s) you want to use before beginning the app installation.

## Installing the WG Easy App

To install**WG Easy**, log into SCALE, go to **Apps**, and click **Discover Apps**.
Either begin typing WG Easy into the search field or scroll down to locate the **WG Easy** application widget.

![SCALE WG Easy Application Widget](/docs/images/SCALEWGEasyAppWidget.png)

Click on the widget to open the **WG Easy** application information screen.

![SCALE WG Easy App Information Screen](/docs/images/SCALEWGEasyAppInfoScreen.png)

Click **Install** to open the WG Easy application configuration screen.

The **Install WG Easy** screen groups settings by type. The sections below provide details on each.
To find specific fields click in the **Search Input Fields** search field and scroll down to it. 
To move to a particular section, click on the section heading on the navigation area in the upper-right corner.

![SCALE Install WG Easy Application Screen](/docs/images/SCALEWGEasyAppInfoScreen.png)

Enter the public host name or IP of your VPN server in **Hostname or IP**.

You can install the app using the default settings or enter new values to customize to suit your use case. 
See the sections below for information on customizing application settings. You can edit the application settings at any time after installation.

Click **Install**. 
The system opens the **Installed Applications** screen with the Prometheus app in the **Deploying** state.
When the installation completes it changes to **Running**. 

Click **Web Portal** on the **Application Info** widget to open the WG Easy web interface where you can add a new client.

![WG Easy Web Portal](/docs/images/SCALEWGEasyWebPortal.png)

### Application Name Settings

Accept the default value or enter a name in **Application Name**. 
Use the default name but if adding a second deployment of the application you must change this name.

Accept the default version number in **Version**. 
When a new version becomes available, the application has an update badge. 
The **Installed Applications** screen shows the option to update applications.

### Configuration Settings

You can accept the defaults in the **Configuration** settings customize to suit your use case.

![SCALE WG Easy Configuration Settings](/docs/images/SCALEWGEasyAppConfigSettings.png)

If you use or want to protect access to the WG Easy web UI, enter a password in **Password for WebUI**.

Accept the default values in **Persistent Keep Alive** or change the value to the number of seconds you want to keep the session alive.
When set to zero, connections are not kept alive. An alternate value to use  is 25.

Accept the default setting for WireGuard (1420) in **Clients MTU** or enter a new value.

Accept the default IPs in **Clients IP Address Range** and **Clients DNS Server** or enter the IP addresses the client uses. 
If not provided, the app uses the default value 1.1.1.1.

To specify allowed IP addresses, click **Add** to the right of **Allowed IPs** for each IP address to enter.
If not specifying allowed IPs, the application uses 0.0.0.0/0.

To specify environment variables, click **Add** to the right of **WG Easy Environment** for each environment variable to add.

{{< expand "Environment Variables" "v" >}}
| Variable | Description |
|----------|-------------|
| WD_DEVICE | Enter the interface name or ID for the ethernet device WireGuard traffic should forward through. |
| WG_PRE_UP | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
| WG_POST_UP | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
| WG_PRE_DOWN | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
| WG_POST_DOWN | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
{{< /expand >}}

### Storage Settings
Install WG Easy using the default storage settings or enter datasets on the system to use for storage settings.

Select **Enable Custom Host Path for WG-Easy Configuration Volume** to add the **Host Path for WG-Easy Configuration Volume** field.
Enter or browse to select a preconfigured dataset mount path for the host path.

![SCALE WG Easy Add Custom Host Path](/docs/images/SCALEWGEasyInstallStorageAddExtraHostPaths.png)

To add additional host path volumes, click **Add** to the right of **Extra Host Path Volumes**.

![SCALE WG Easy Add Extra Host Path Volumes](/docs/images/SCALE/WGEasyInstallAppStorageAddExtraHostPaths.png) 

Enter or browse to the host path for dataset in **Mount Path in Pod** where you want to mount the volume inside the pod.

### Networking Settings

Accept the default port numbers in **WireGuard UDP Node Port for WG-Easy** and **WebUI Node Port for WG-Easy**.
WireGuard always listens on 51820 inside the container.

Refer to the TrueNAS [default port list](https://www.truenas.com/docs/references/defaultports/) for a list of assigned port numbers.
To change the port numbers, enter a number within the range 9000-65535.

![SCALE WG Easy Install Networking](/docs/images/SCALEWGEasyInstallAppNetworking.png)

### Advanced DNS Settings
WG Easy does not require configuring advanced DNS options.
Accept the default settings or click **Add** to the right of **DNS Options** to show the fields for option name and value.

![SCALE WG Easy Add DNS Options](/docs/images/SCALEWGEasyInstallAddDNSOptions.png)

### Resource Configuration Settings

Accept the default values in **Resources Configuration** or customize to suit the use case. 
By default, the application limits resources to no more than four CPU cores and eight Gigabytes available memory but the application might use considerably less system resources. 

Select **Enable Pod resource limits** to show the fields to enter new CPU and memory values for the destination system.

![SCALE WG Easy Enable Resource Limits](/docs/images/SCALEWGEasyInstallAddResourceLimits.png)

To customize the CPU and memory allocated to the container (pod) WG Easy uses, enter new CPU values as a plain integer value followed by the suffix m (milli). Default is 4000m.

Accept the default value 8Gi allocated memory or enter a new limit in bytes. 
Enter a plain integer followed by the measurement suffix, for example 129M or 123Mi.
