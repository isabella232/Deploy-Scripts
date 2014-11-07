Download
---------------------
Get the latest script [here](https://raw.github.com/opendns/Deploy-Scripts/master/Labtech/OpenDNS%20Umbrella%20Roaming%20Agent.xml).

Notes
-----

This script deploys the roaming client for **Windows only**.
There is currently no support for any other operating system. 
The script will simply exit if run on OS X or Linux.

When the script is run, or scheduled, it will prompt for these variables:
  * `ORGID_FROM_CONFIG_FILE`
  * `FINGERPRINT_FROM_CONFIG_FILE`
  * `USERID_FROM_CONFIG_FILE`

Their values can be retrieved from the [MSP Console->Roaming Agent->Deploy](https://dashboard2.opendns.com/msp#roamingclient/deploy) page.

More information on these variables can be found [here](https://support.opendns.com/entries/55881150-Roaming-Client-Deployment-Parameters-for-mass-deployment-MSP-).



What the script does
--------------------

1. Make the `%windir%\ltsvc\packages\umbrella` folder
2. Download the [Roaming Client msi](http://shared.opendns.com/roaming/enterprise/release/win/production/Setup.msi) to the above folder
3. If the file is unable to be download, open a ticket
4. Use `msiexec` to install the downloaded MSI file silently, with no UI and remove the Add/Remove Programs entry.

