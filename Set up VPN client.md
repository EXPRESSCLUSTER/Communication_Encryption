# Set up the VPN Client

*Windows Server 2019 — L2TP over IPsec*

> **Prerequisite:** The VPN server must already be configured and a user
> account must have been granted VPN access on the Domain Controller. If this
> has not been done, complete the [VPN server setup](Set%20up%20VPN%20Server.md)
> first.

---

## Create the VPN Connection

1. Right-click the **Start** menu and select **Network Connections**.
2. Click **VPN** in the left pane.
3. Click **Add a VPN connection** and fill in the fields:
   - **VPN provider:** Windows (built-in)
   - **Connection name:** a descriptive name, e.g. `MyVPN`
   - **Server name or address:** the IP address of the VPN server on the local
     network (in a LAN cluster environment this is typically the server's
     management or MDC network IP address — **not** a public internet address)
   - **VPN type:** L2TP/IPsec with pre-shared key
   - **Pre-shared key:** the key set during VPN server configuration
   - **User name / Password:** optional — enter if you want credentials saved
4. Click **Save**.
5. Click the newly created connection (e.g. `MyVPN`) and click **Connect**.
   If credentials were not saved, enter them when prompted and click **OK**.

---

## Verify the Connection

**On the client:**

1. The VPN connection icon should display **Connected**.
2. Open **Network Connections** (`ncpa.cpl`). A new connection with the VPN
   connection name should appear.
   Right-click it, select **Status**, and click **Details** to view the Network
   Connection Details, including the virtual IP address assigned to the client.
3. Open a command prompt and run `ipconfig`. Look for a new **PPP adapter**
   entry — the IP address shown is the client's VPN virtual IP address. Note
   this address; it will be needed for the MDC configuration.

**On the server:**

1. Open **Routing and Remote Access**.
2. **Remote Access Clients** should show a new connection. Refresh if it does
   not appear immediately.
3. **Ports** should show a new **WAN Miniport (L2TP)** entry with an **Active**
   status.

---

## Configure the EXPRESSCLUSTER MDC Connection

Once the VPN connection is verified, the Mirror Disk Connection in
EXPRESSCLUSTER must be updated to route mirror disk traffic over the VPN
tunnel.

1. Note the virtual IP addresses assigned to the VPN server and VPN client
   (visible via `ipconfig` on each machine — look for the PPP adapter entry).
2. In the **Cluster WebUI**, add a new MDC connection using the two virtual IP
   addresses as the connection endpoints.
3. Set this new MDC connection to the **highest priority** for mirror disk
   communication.
4. Apply the configuration. A cluster restart may be required.

> See [Final Notes](Final_Notes.md) for known issues and workarounds related
> to this step, including what to do if applying the new MDC connection does
> not go smoothly.

---

## Automatic Reconnection After Restart

The VPN client does not reconnect automatically when the client server
restarts. To work around this, create a scheduled task to reconnect at startup:

1. Open **Task Scheduler** and create a new task.
2. Set the trigger to **At startup**.
3. Set the action to run the following command:
   ```
   C:\Windows\System32\rasdial.exe <VPN Connection Name>
   ```
   Replace `<VPN Connection Name>` with the name used when creating the
   connection (e.g. `MyVPN`).

> **Note:** This task handles restarts of the client server. It does **not**
> handle the case where the VPN server restarts. See
> [Final Notes](Final_Notes.md) for the server-restart limitation and a
> possible workaround.
