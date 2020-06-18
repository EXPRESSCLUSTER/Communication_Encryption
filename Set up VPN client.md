## Configure the VPN client
*First enable a user to use VPN to access a server and then set up a VPN client*
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
    - Enter a name in the **Connection name** field e.g. MyVPN.
    - In the **Server name or address field** enter the public IP address of the VPN server.
    - Change the **VPN type** to **L2TP/IPsec with pre-shared key** and enter the key used in the VPN server setup in the **Pre-shared key** field.
    - *Optional* - Enter a **User name** and **Password** if you want it to be remembered.
4. Click **Save**.
5. Click on the newly created VPN connection icon e.g. MyVPN and click **Connect**  
If the user name and password weren't saved previously, enter them and click **OK**.
### Verify connection
#### Client
1. Beneath the VPN connection icon should be the word **\"Connected\"**.
2. Open **Network Connections** (ncpa.cpl) and you should see a new connection with the name of your VPN connection name created previously e.g. MyVPN  
Right click the new VPN connection, select **Status**, and click **Details** to see Network Connection Details, including the assigned IP address.
3. Open a command prompt. Type IPConfig and look for a new entry with a new IP address 
#### Server
1. On the VPN server open **Routing and Remote Access**. 
2. **Remote Access Clients** should show a new connection. Refresh the display if it doesn't show up.
3. **Ports** should have a new **WAN Miniport (L2TP)** entry which has an **Active** status.
