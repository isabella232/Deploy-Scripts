###Deploying OpenDNS Umbrella Roaming Client with LabTech
<div>
<table style="height: 100px; width: 100%">
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p><strong>NOTE:</strong> This document is specific to deploying the OpenDNS Roaming Client on Windows client operating systems,  such as Windows 8 or 10. OpenDNS does not support the installation of the Roaming Client on Windows Server operating systems.</p>
			</td>
		</tr>
	</tbody>
</table>
</div>


The OpenDNS Roaming Client can be deployed using RMM tools, such as LabTech, by applying the <a href="https://docs.opendns.com/product/msp/automated-deployment/#section-deployment-parameters">correct parameters</a> as part of the install string.  

The script outlined in this readme is more advanced than our <a href="https://github.com/opendns/Deploy-Scripts/tree/master/Labtech">basic script</a> and provides a more robust integration where you can automate deployment of the Roaming Client to managed workstations.

<div>
<table style="align:center"><colgroup><col width="624" /></colgroup>
	<tbody>
		<tr>
			<td bgcolor="#ccffff">This document assumes that you have read the prerequisites for the Roaming Client and all necessary firewall ports have been opened as documented in <a href="https://docs.opendns.com/product/msp/prerequisites/">this support article.</a>  Please note that all customer Internal Domains must be entered first before deploying the Roaming Client.  Failure to do so will cause problems with accessing internal resources. This is done in the Dashboard by navigating to Configuration > System Settings > Internal Domains. For details about what needs to be in this list, please see <a href="https://docs.opendns.com/product/msp/appendix-d-internal-domains/">this support article</a>.
			</td>
		</tr>
	</tbody>
</table>
</div>
To download the script, you can find the [full script here](https://github.com/opendns/Deploy-Scripts/blob/master/Labtech/advanced/Deploy_OpenDNS_Umbrella_Client-advanced.xml).
If you aren't familiar with GitHub, we recommend importing the script properly by clicking on the ‘Raw’ button as shown below:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/GitHub_Raw.png" border="0" alt="Scripts -> Raw">
			</td>
		</tr>
	</tbody>
</table>

This will open the script into raw XML (see below) that you can copy/paste into your favorite text editor and save as an XML file.

<table>
	<tbody>
		<tr>
			<td>
				<img src="docs/GitHub_Raw2.png" border="0" alt="Raw XML"">
			</td>
		</tr>
	</tbody>
</table>

Once you have the file saved, now we can import into LabTech.  To do that, open the LabTech Control Center, and click on Tools > Import > LT XML Expansion.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Import_XML.png" border="0" alt="Parameters from OpenDNS Dashboard">
			</td>
		</tr>
	</tbody>
</table>

You will be warned that importing items that already exist will result in them being updated, not new items created.  You can click ‘Yes’ on this warning.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/Import_XML_Warning.png" border="0" alt="Import Script">
			</td>
		</tr>
	</tbody>
</table>

Now you should see the newly imported script in the root script folder, and you can move it to your preferred location.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<center><img src="docs/Script_Imported.png" border="0" alt="Script successfully imported!" style="vertical-align:middle"></center>
			</td>
		</tr>
	</tbody>
</table>


At the Client and Computer level, the new fields appear for you to fill in with the appropriate OpenDNS values.  At the Client level, in order to allow the script to run, the “OpenDNS_EnabledClient” checkbox must be checked:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<center><img src="docs/Client_Checkbox.png" border="0" alt="Computer Settings"></center>
			</td>
		</tr>
	</tbody>
</table>

The OpenDNS ```User_ID```, ```Org_ID``` and ```Org_Fingerprint``` are found in the MSP Console under the Customer Management card in the _Deployment Parameters_ section. 

<table>
	<tbody>
		<tr>
			<td>
				<img src="docs/CustomerManagement.png" border="0" alt="Click the Caret">
			</td>
		</tr>
	</tbody>
</table>

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/RoamingParameters.png" border="0" alt="Script Parameters">
			</td>
		</tr>
	</tbody>
</table>

At the computer level, for scenarios which require a single workstation, or a small group, to be excluded from having the Roaming Client installed, simply check the "OpenDNS\_No_URC" box shown below for the appropriate computers, and the Roaming Client Deployment script will exit without installing.

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<center><img src="docs/LabTech-ComputerAddlInfo.png" border="0" alt="Deploy to workstations only!"></center>
			</td>
		</tr>
	</tbody>
</table>


To confirm the Roaming Client is checking in, log into your OpenDNS Dashboard and choose the customer where you ran the deployment script.  Then navigate to Configuration -> Identities -> Roaming Computers.  If the computer is checking in properly, you’ll notice a green status icon as shown below.  

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="docs/PolicyStatus.png" border="0" alt="Roaming Client in Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Computers without a green status icon are not checking in properly with OpenDNS.  Please check [this support article](https://docs.opendns.com/product/msp/appendix-a-status-and-functionality/) for more information on the status icons and troubleshooting.
