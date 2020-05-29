## Configure the VPN client
*Enable a user to use VPN to access a server and then set up a VPN client*
### Enable VPN access to a user or group
1. Launch **Active Directory Users and Computers** on the Domain Controller.
2. Under **Users** create and select a new user or select an existing account to grant VPN access.
3. Right-click on the user and select **Properties**.
4. Select the **Dial-in** tab. The **Network Access Permission** default setting is **Control access through NPS Network Policy**. NPS policies can be created and enabled but the simplest method is to select **Allow access**.
5. Click **Apply**. Click **OK**.
### Set up VPN client
1. On the client machine right-click on the **Start** menu and select **Network Connections**.
2. Click **VPN** in the left pane.
3. Click **Add a VPN connection** and a dialog will come up which has several fields to fill out:  
    - For **VPN provider** choose **Windows (built-in)**. 
