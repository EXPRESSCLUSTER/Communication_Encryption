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
  \*If you have already closed this dialog, click on the notifications icon in the **Server Manager** window. Click on the **'Add Roles and Features'** link, which will reopen the dialog at the *Installation succeeded* stage.
