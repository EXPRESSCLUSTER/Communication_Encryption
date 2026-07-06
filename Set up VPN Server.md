# Set up the VPN Server

*Windows Server 2019 — L2TP over IPsec*

> **Before you begin:**
> - Install all pending Windows updates on the server.
> - Ensure the following ports are open on any firewall between the servers:
>   - **UDP 500** — IKE (IPsec key exchange)
>   - **UDP 4500** — IPsec NAT traversal
>   - **UDP 1701** — L2TP

---

## Install the Remote Access Role

1. Open **Server Manager**, click the **Manage** menu, and select **Add Roles
   and Features**.
2. Click **Next** on the **Before you begin** screen.
3. Select **Role-based or feature-based installation** and click **Next**.
4. The local server should be pre-selected. Click **Next**.
5. In the **Server Roles** list, check **Remote Access** and click **Next**.
6. No additional features are needed. Click **Next** to skip the Features
   screen, then click **Next** again past the Remote Access introduction page.
7. On the **Role Services** screen, check **DirectAccess and VPN (RAS)** and
   click **Next**.
8. Click **Add Features** when prompted to add required features, then click
   **Next**.
9. Click **Next** to skip the additional roles screen.
10. On the **Confirmation** screen, click **Install**.

---

## Configure the VPN Role — Part 1

1. Before closing the **Add Roles and Features** wizard, click **Open the
   Getting Started Wizard** at the top of the dialog.

   > If you have already closed the wizard, click the notifications (flag) icon
   > in Server Manager and click the **Open the Getting Started Wizard** link
   > to reopen it.

2. Click **Deploy VPN only**. The **Routing and Remote Access** console opens.
3. Right-click the server name in the left pane and select **Configure and
   Enable Routing and Remote Access**.
4. Click **Next** on the welcome screen.
5. Select **Custom configuration** and click **Next**.
6. Check **VPN access** only and click **Next**.
7. Click **Finish** on the summary screen.
8. Click **Start service** to start the Routing and Remote Access service.

---

## Configure the VPN Role — Part 2

1. In the **Routing and Remote Access** console, right-click the server name
   and select **Properties**.
2. Click the **Security** tab.
3. Check **Allow custom IPsec policy for L2TP/IKEv2 connection** and enter a
   preshared key, e.g. `MyVPNkey`.

   > This key will be required when configuring the VPN client. Use a strong,
   > unique value in production.

4. Click **Apply**.
5. Click the **IPv4** tab.
6. If DHCP is available, no changes are needed. Otherwise select **Static
   address pool** and enter an IP address range.

   > **For cluster use, a static address pool is recommended.** The virtual IP
   > addresses assigned from this pool will become the VPN tunnel endpoints
   > used in the EXPRESSCLUSTER MDC configuration. Note these addresses for
   > use when configuring the VPN client and setting up the MDC connection.

7. Click **OK**.
8. Right-click the server name and select **All Tasks → Restart** to restart
   the Routing and Remote Access service.

---

## Enable VPN Access for a User Account

A domain user account must be granted VPN access before a client can connect.

1. Open **Active Directory Users and Computers** on the Domain Controller.
2. Under **Users**, create a new account or select an existing one to grant
   VPN access.
3. Right-click the user and select **Properties**.
4. Click the **Dial-in** tab. The default **Network Access Permission** is
   **Control access through NPS Network Policy**. NPS policies can be
   configured for more granular control, but the simplest approach is to
   select **Allow access**.
5. Click **Apply**, then click **OK**.

---

## Next Step

Proceed to [Set up the VPN client](Set%20up%20VPN%20client.md) on the other
server.
