# Create an IP Security Policy on Windows servers (manual method)
## Open the IP Security Policy Management snap-in
01. Open the **Microsoft Management Console** by accessing the **Run** menu (Windows key + R), enter **MMC**, and click **OK**.
02. Click **File** and select **Add/Remove Snap-in...**
03. Scroll down the **Available snap-ins** to find and select **IP Security Policy Management**. Click **Add**.
04. Leave the default (**Local computer**) selected and click **Finish**.
05. Click **OK**.
## Create IP Security Policy
01. Right click **IP Security Policies on Local Computer** and click on **Create IP Security Policy...**
02. Click **Next** in the **Welcome** screen.
03. Enter a **Name** for the new policy e.g. *ECX IP Security*. Click **Next**.
04. In the **Requests for Secure Communication** window click **Next** without checking the box.
05. Leave the **Edit properties** box checked and click **Finish**.
06. Uncheck the **Use Add Wizard** box and click **Add** to create a new security rule.
    ### IP Filter List tab
    01. Click **Add** on the **IP Filter List** tab.
    02. Enter a name for the new filter list e.g. ECX2 Communication Port.
    03. Uncheck the 'Use Add Wizard' box and click 'Add'.
   Addresses tab
   01. On the 'Addresses' tab change the 'Source address:' from 'Any IP Address' to 'A specific IP Address or Subnet' and enter the IP address used for mirrored communication (ECX MDC) on the current server.
   02. Change the 'Destination address' from 'Any IP Address' to 'A specific IP Address or Subnet' and enter the IP address of the other server's ECX MDC.
   03. The 'Mirorred' check box can be left checked.
   Protocol tab
   01. Click the 'Protocol' tab and change the 'protocol type' from 'Any' to 'TCP'.
   02. Set the 'From' IP protocol port to 'From this port:' and enter 29005.
   03. Leave the 'To' IP protocol port as 'To any port' and click 'OK'.
04. Click 'Add' again to input an incoming filter.
   Addresses tab
   01. On the 'Addresses' tab change the 'Source address:' from 'Any IP Address' to 'A specific IP Address or Subnet' and enter the IP address used for mirrored communication (ECX MDC) on the current server.
   02. Change the 'Destination address' from 'Any IP Address' to 'A specific IP Address or Subnet' and enter the IP address of the other server's ECX MDC.
   03. The 'Mirorred' check box can be left checked.
   Protocol tab
   01. Click the 'Protocol' tab and change the 'protocol type' from 'Any' to 'TCP'.
   02. Leave the 'From' IP protocol port as 'From any port' and click 'OK'.
   03. Set the 'To' IP protocol port to 'To this port:' and enter 29005 and click 'OK'.
05. Verify that there is one filter from 29005 to any port and one filter from any port to 29005 and click 'OK'.
06. Select the newly added filter (e.g. ECX2 Communication Port).
07. Select the Filter Action tab
Filter Action tab
01. Make sure the 'Use Add Wizard' box is unchecked and click 'Add'
    Security Methods tab
    01. On the Security Methods tab leave 'Negotiate security' selected and click 'Add'.
    02. Leave the default as 'Integrity and encryption' and click 'OK'. Move this security method to the top if there are others.
        (the default ESP confidentiality method is 3DES and integrity method is SHA1)
    03. Check the 'Use session key perfect forward secrecy (PFS)'.
    General tab
    01. Click the 'General' tab and enter a name for the filter action e.g. ECX Communication Encryption. Click OK.
02. Select the newly entered filter action (e.g. ECX Communication Encryption).
03. Select the Authentication Methods tab.
Authentication Methods tab
    01. Click on 'Add' for a new authentication method.
    02. Select 'Use this string (preshared key):' and enter a character string e.g. ECXSecurity. Click 'OK'
04. Select the newly entered key and move it up to the top position. 
05. Click 'Apply' and then 'OK'.
06. Make sure the newly created security rule box is checked and click 'OK'.
07. Repeat all steps above on the other server in the ECX cluster.
08. Enable the policy on both servers
Open the IP Security Policy Management snap-in and select 'IP Security Policies on Local Computer' to display all security policies.
Right click on the policy recently created and click Assign. Repeat on the other server.
*Note that only one policy can be assigned at a time.

