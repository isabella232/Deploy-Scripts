###Deploying OpenDNS Umbrella Roaming Client with Kaseya
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


The OpenDNS Roaming Client can be deployed using RMM tools, such as Kaseya, by applying the <a href="https://docs.opendns.com/product/msp/automated-deployment/#section-deployment-parameters">correct parameters</a> as part of the install string.  


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

To download the script, you can find the [full script here](https://github.com/opendns/Deploy-Scripts/blob/master/Kaseya/Umbrella_Roaming_Client.xml).
If you aren't familiar with GitHub, we recommend importing the script properly by clicking on the ‘Raw’ button as shown below:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="images/GitHub_Raw.png" border="0" alt="Scripts -> Raw">
			</td>
		</tr>
	</tbody>
</table>

This will open the script into raw XML (see below) that you can copy/paste into your favorite text editor and save as an XML file.

<table>
	<tbody>
		<tr>
			<td>
				<img src="images/GitHub_Raw2.png" border="0" alt="Raw XML"">
			</td>
		</tr>
	</tbody>
</table>

Once you have the file saved, now we can import into Kaseya.  To do that, navigate to Agent Procedures > Manage Procedures > Schedule / Create. Here you can select a folder in which to import the script, and then click Import Folder/Procedure:

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="images/Import_XML.png" border="0" alt="Parameters from OpenDNS Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Choose the file to upload, and then click "Save."

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="images/Import_XML2.png" border="0" alt="Parameters from OpenDNS Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Now you should see the newly imported script in the selected folder.

<table style="width:75%">
	<tbody>
		<tr>
			<td>
				<center><img src="images/Script_Imported.png" border="0" alt="Script successfully imported!" style="vertical-align:middle"></center>
			</td>
		</tr>
	</tbody>
</table>

When running the script, you will be prompted to enter the <a href="https://docs.opendns.com/product/msp/automated-deployment/#section-deployment-parameters">parameters</a> found in the MSP Console.  

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="images/Parameters-Prompt.png" border="0" alt="Prompt for parameters">
			</td>
		</tr>
	</tbody>
</table>

The ```User_ID```, ```Org_ID``` and ```Org_Fingerprint``` parameters are found in the MSP Console under the Customer Management card in the _Deployment Parameters_ section.  
<table>
	<tbody>
		<tr>
			<td>
				<img src="images/CustomerManagement.png" border="0" alt="Click the Caret">
			</td>
		</tr>
	</tbody>
</table>

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="images/RoamingParameters.png" border="0" alt="Script Parameters">
			</td>
		</tr>
	</tbody>
</table>

You have the option to hide the Add/Remove Programs entry and the System Tray icon by filling in the appropriate value.

To confirm the Roaming Client is checking in, log into your OpenDNS Dashboard and choose the customer where you ran the deployment script.  Then navigate to Configuration -> Identities -> Roaming Computers.  If the computer is checking in properly, you’ll notice a green status icon as shown below.  

<table style="width:100%">
	<tbody>
		<tr>
			<td>
				<img src="images/PolicyStatus.png" border="0" alt="Roaming Client in Dashboard">
			</td>
		</tr>
	</tbody>
</table>

Computers without a green status icon are not checking in properly with OpenDNS.  Please check [this support article](https://docs.opendns.com/product/msp/appendix-a-status-and-functionality/) for more information on the status icons and troubleshooting.
