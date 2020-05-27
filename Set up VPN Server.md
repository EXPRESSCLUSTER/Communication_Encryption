# VPN Server Setup
*Windows Server 2019 with L2TP over IPSec* 
Before beginning, install the latest updates onto the server
## Install Remote Access Role (with VPN)
1. Launch the **Server Manager**, select the **Manage** menu, and select **Add Roles and Features**.
2. Click **Next** at the **Before you begin** screen.
3. Select **Role-based or feature-based installation** for the **Installation type**. Click **Next**.
4. The **local server** should be selected. Click **Next**.
5. For the **Server role**, locate and check the box for **Remote Access**. Click **Next**.
6. No additional features are necessary. Click **Next**. Click **Next**.
7. Select **DirectAccess and VPN (RAS)** for the **Roles Services**. Click **Next**.
8. Click the **Add Features** button to add the necessary additional features. Click **Next**.
9. Click **Next** since no additional roles are needed.
10. On the **Confirmation** screen click **Install**.
## Configure VPN Role Part 1
1. Before closing the **Add Roles and Features** wizard, click **'Open the Getting Started Wizard'** at the top of the dialog box.  
  \*If you have already closed this dialog, click on the notifications (flag) icon in the **Server Manager** window. Click on the **'Add Roles and Features'** link, which will reopen the dialog at the *Installation succeeded* stage.
2. This link launches the **Configure Remote Access - Getting Started** wizard. Click **Deploy VPN only**.
3. The **Routing and Remote Access** console opens.
4. Right-click your server name in the left pane and select **Configure and Enable Routing and Remote Access**.
5. Click **Next** on the welcome screen.
6. Select **Custom Configuration** on the **Configuration** screen. Click **Next**.
7. On the **Custom Configuration** screen only check **VPN access**. Click **Next**.
8. Click **Finish** on the **Summary** screen.
9. On the next screen click **Start service** to start the Routing and Remote Access service.
## Configure VPN Role Part 2
1. In the **Routing and Remote Access** console right-click the server name and select **Properties**.
2. Select the **Security** tab.
3. Check **Allow custom IPsec policy for L2TP/IKEv2 connection** and enter a **Preshared Key** e.g. MyVPNkey.
4. Click **Apply**.
5. Select the **IPv4** tab.
6. If using **DHCP** no changes are needed. Otherwise choose **Static address pool** and enter an IP address range.
7. Click **OK**.
8. Restart the **Routing and Remote Access** service by right-clicking on the server name. Select **All Tasks->Restart**.
## Enable VPN access to a user or group
