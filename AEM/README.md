### Deploying Umbrella roaming client with Autotask Endpoint Manager (AEM)
<div>
<table style="height: 50px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p> This guide is meant to be a basic overview of deploying the Cisco Umbrella roaming client using your RMM tool. We are not able to provide comprehensive support for AEM, but there is  <a href="http://help.aem.autotask.net/en/Content/4FEATURESPORTAL/Components/Scripting.htm">further documentation</a> available related to Components in AEM.</p>
			</td>
		</tr>
	</tbody>
</table>
</div>
<div>
<table style="height: 100px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p><strong>NOTE:</strong> This document is specific to deploying the Umbrella roaming client on Windows client operating systems, such as Windows 8 or 10. We do not support the installation of the Umbrella roaming client on Windows Server operating systems. A list of prerequisites is available <a href="https://docs.umbrella.com/product/msp/prerequisites/">here</a>. This document assumes you've read these prerequisites and have opened the appropriate firewall ports</p>
			</td>
		</tr>
	</tbody>
</table>
</div>
AEM provides the ability to use ```Components``` to deploy software or perform tasks. Components are essentially scripts in various languages (sometimes with environment variables) used in ```Jobs``` to run on the endpoints. The component available for download <a href="https://github.com/opendns/Deploy-Scripts/raw/master/AEM/DeployUmbrellaRoamingClient.cpt">here</a> is a PowerShell script with environment variables.

<div>
<table style="align:center"><colgroup><col width="624" /></colgroup>
	<tbody>
		<tr>
			<td bgcolor="#ccffff">You must enter all customer internal domains before deploying the Umbrella roaming client. Failure to do so will cause problems with accessing internal resources. To do this, in the Umbrella dashboard, navigate to Settings > Internal Domains and enter domains as required. For details about what needs to be in this list, please see please see <a href="https://docs.umbrella.com/product/msp/appendix-d-internal-domains/">this support article</a>.
			</td>
		</tr>
	</tbody>
</table>
</div>

Once logged into your AEM Portal, you will see the top navigation menu where you will select the devices you wish to deploy the roaming client to. __Note that you are only able to deploy to a single customer at a time__. 

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Devices.png" border="0" alt="Sites > Site Name > Devices">
			</td>
		</tr>
	</tbody>
</table>

Once you have selected the appropriate devices, schedule a Job to run: 

<table>
	<tbody>
		<tr>
			<td>
				<img src="docs/ScheduleJob.png" border="0" alt="Schedule Job">
			</td>
		</tr>
	</tbody>
</table>

You will then be prompted for a Job name, Component to add and any alerting options you want to configure. First, choose the name for the Job and when you want to schedule the Job to run. Then, click ```Add a Component```.

<table>
	<tbody>
		<tr>
			<td>
				<img src="docs/AddComponent.png" border="0" alt="Add Component">
			</td>
		</tr>
	</tbody>
</table>

Now, select the ```Deploy Umbrella roaming client``` component and click ```Add```.

<table style="align:center"><colgroup><col width="624" /></colgroup>
	<tbody>
		<tr>
			<td>
				<img src="docs/SelectComponent.png" border="0" alt="Deployment Parameters">
			</td>
		</tr>
  </tbody>
</table>


Now that you've added the Component, you will see a section for Variables. This is what associates the roaming client with the correct customer organization. In the MSP Console, you can find the  ```User_ID```, ```Org_ID``` and ```Org_Fingerprint``` parameters by navigating to Customer Management and expanding a customer.

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

Copy the appropriate variables into the fields as shown below.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Variables.png" border="0" alt="Component Variables">
			</td>
		</tr>
	</tbody>
</table>


The rest of the Job page is optional, but if you want alerts with logs emailed to you, you can use the Alerts + Job Recipients section to do so:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/AlertOptions.png" border="0" alt="Alert Options" style="vertical-align:middle">
			</td>
		</tr>
	</tbody>
</table>



To review results, click on the Job name and view the status as shown below. 

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/SuccessResult.png" border="0" alt="Job Results" style="vertical-align:middle">
			</td>
		</tr>
	</tbody>
</table>

A successful install will show the following ```Stdout``` output:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Successful.png" border="0" alt="Script Parameters">
			</td>
		</tr>
	</tbody>
</table>




In this example, we see a failed job and the logs from the script are in the ```Stdout``` output.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Results.png" border="0" alt="Job Results" style="vertical-align:middle">
			</td>
		</tr>
	</tbody>
</table>

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/ErrorMessage.png" border="0" alt="Stdout logs">
			</td>
		</tr>
	</tbody>
</table>

Another example:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Error2.png" border="0" alt="Stdout logs">
			</td>
		</tr>
	</tbody>
</table>





To confirm the roaming client is checking in, log into your Umbrella Dashboard and choose the customer where you ran the deployment script. Navigate to Identities > Roaming Computers, and search for the individual host names where the script should have been run.  If the computer is checking in properly, you’ll notice a green status icon as shown below:  

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/PolicyStatus.png" border="0" alt="Roaming Client in Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Computers without a green status icon are not checking in properly with Umbrella.  Please check [this support article](https://docs.umbrella.com/product/msp/appendix-a-status-and-functionality/) for more information on the status icons and troubleshooting.
