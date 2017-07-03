### Deploying Umbrella roaming client with N-able
<div>
<table style="height: 100px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p><strong>NOTE:</strong> This document is specific to deploying the Cisco Umbrella roaming client on Windows client operating systems, such as Windows 8 or 10. We do not support the installation of the Umbrella roaming client on Windows Server operating systems. A list of prerequisites is available <a href="https://docs.umbrella.com/product/msp/prerequisites/">here</a>. This document assumes you've read these prerequisites and have opened the appropriate firewall ports.</p>
			</td>
		</tr>
	</tbody>
</table>
</div>


The Umbrella roaming client can be deployed using RMM tools, such as N-able, by applying the <a href="https://docs.umbrella.com/product/msp/automated-deployment/#section-deployment-parameters">correct parameters</a> as part of the install string.  


<div>
<table style="align:center"><colgroup><col width="624" /></colgroup>
	<tbody>
		<tr>
			<td bgcolor="#ccffff">You must enter all customer internal domains before deploying the Umbrella roaming client. Failure to do so will cause problems with accessing internal resources. To do this, in the Umbrella dashboard navigate to Settings > Internal Domains and enter domains as required. For details about what needs to be in this list, please see <a href="https://docs.umbrella.com/product/msp/appendix-d-internal-domains/">this support article</a>.
			</td>
		</tr>
	</tbody>
</table>
</div>

To download the script, you can find the [full script here](https://github.com/opendns/Deploy-Scripts/blob/master/N-able/UmbrellaRoamingClient-install.amp).
If you aren't familiar with GitHub, we recommend importing the script properly by clicking <strong>Raw</strong>.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/GitHub_Raw.png" border="0" alt="Scripts -> Raw">
			</td>
		</tr>
	</tbody>
</table>

This will open the script into raw XML (see below) that you can copy/paste into your favorite text editor and save as a .AMP file.

<table>
	<tbody>
		<tr>
			<td>
				<img src="docs/GitHub_Raw2.png" border="0" alt="Raw XML"">
			</td>
		</tr>
	</tbody>
</table>

Once you have the file saved, now we can import into N-able.  To do that, at the Service Organization (SO) level, navigate to Configuration > Scheduled Tasks > Script/Software Repository. Here you can add a new automation policy:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/NCentral-Add-AP.png" border="0" alt="Parameters from Umbrella Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Choose the file to upload, and then click "OK."

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/NCentral-Browse.png" border="0" alt="Parameters from Umbrella Dashboard">
			</td>
		</tr>
	</tbody>
</table>

To schedule the Automation Policy, navigate to the appropriate customer and click on Actions > Run an Automation Policy. Select "OpenDNS Umbrella RoamingClient"  and you will see the screen below. You will be need to enter the <a href="https://docs.umbrella.com/product/msp/automated-deployment/#section-deployment-parameters">parameters</a> found in the MSP Console.  

<div>
<table style="height: 10px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p><strong>NOTE:</strong> Cisco recommends using the LocalSystem credentials as shown below.</p>
			</td>
		</tr>
	</tbody>
</table>
</div>

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/SetParams.png" border="0" alt="Prompt for parameters">
			</td>
		</tr>
	</tbody>
</table>

<div>
<table style="height: 10px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ccffff">
				<p><strong>Support Operating Systems:</strong><br>This script will exit if a Windows Server operating system is detected, as it is not supported.</p>
			</td>
		</tr>
	</tbody>
</table>
</div>

By default, this install will hide the Add/Remove Programs entry, as well as the Windows system tray icon.

In Umbrella for MSPs, you can find the ```User_ID```, ```Org_ID``` and ```Org_Fingerprint``` parameters by navigating to Customer Management and expanding a customer. 
<table>
	<tbody>
		<tr>
			<td>
				<img src="docs/CustomerManagement.png" border="0" alt="Click the Caret">
			</td>
		</tr>
	</tbody>
</table>

Parameters are located in the _Deployment Parameters_ area.  
<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/RoamingParameters.png" border="0" alt="Script Parameters">
			</td>
		</tr>
	</tbody>
</table>

Next, select the target workstations to install the roaming client on:

<div>
<table style="height: 100px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p><strong>NOTE:</strong> The Umbrella roaming client is only supported on Windows client operating systems,  such as Windows 8 or 10. Cisco does not support the installation of the roaming client on Windows Server operating systems.</p>
			</td>
		</tr>
	</tbody>
</table>
</div>

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/SelectWorkstations.png" border="0" alt="Script Parameters">
			</td>
		</tr>
	</tbody>
</table>

After you've selected your workstations to deploy the roaming client to, you will need to set the schedule. You can use a one-time schedule since the roaming client will auto-update. In N-able, you have the option to run the task later on offline workstations.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Schedule.png" border="0" alt="Script Parameters">
			</td>
		</tr>
	</tbody>
</table>

After running the automation policy, you can confirm the roaming client is checking in by logging into your Umbrella Dashboard and choose the customer where you ran the deployment script.  Then navigate to Identities -> Roaming Computers.  If the computer is checking in properly, you’ll notice a green status icon as shown below.  

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/PolicyStatus.png" border="0" alt="roaming client in Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Computers without a green status icon are not checking in properly with Umbrella.  Please check [this support article](https://docs.umbrella.com/product/msp/appendix-a-status-and-functionality/) for more information on the status icons and troubleshooting.
