# Create an IP Security Policy on Windows Servers (Manual Method)

This guide covers the same configuration as the
[wizard-based guide](Create%20IP%20Security%20Policy.md) but uses the manual
interface, which exposes all available options including algorithm selection.
Use this method if you need to configure stronger encryption algorithms (e.g.
AES, SHA-256) in place of the wizard defaults (3DES, SHA1).

> **Note:** These steps must be performed on **both servers** in the cluster.
> Complete the full configuration on the first server, then repeat on the
> second before enabling the policy.

Port **29005** is the EXPRESSCLUSTER mirror disk communication port. The
filters created below restrict encryption to TCP traffic on this port between
the two MDC IP addresses.

---

## Open the IP Security Policy Management Snap-in

1. Open the **Microsoft Management Console**: press **Windows key + R**, type
   `MMC`, and click **OK**.
2. Click **File** and select **Add/Remove Snap-in...**.
3. In the **Available snap-ins** list, scroll down to find **IP Security Policy
   Management**. Select it and click **Add**.
4. Leave **Local computer** selected and click **Finish**.
5. Click **OK**.

---

## Create the IP Security Policy

1. Right-click **IP Security Policies on Local Computer** and select **Create
   IP Security Policy...**.
2. Click **Next** on the welcome screen.
3. Enter a name for the policy, e.g. *ECX IP Security*. Click **Next**.
4. On the **Requests for Secure Communication** screen, click **Next** without
   checking the box.
5. Leave **Edit properties** checked and click **Finish**.
6. In the policy properties dialog, uncheck **Use Add Wizard** and click
   **Add** to create a new security rule manually.

---

## IP Filter List Tab

1. On the **IP Filter List** tab, click **Add**.
2. Enter a name for the filter list, e.g. *ECX Communication Port*.
3. Uncheck **Use Add Wizard** and click **Add** to create the outbound filter.

   **Addresses tab:**
   - Change **Source address** from **Any IP Address** to **A specific IP
     Address or Subnet** and enter the MDC IP address of the **current server**.
   - Change **Destination address** from **Any IP Address** to **A specific IP
     Address or Subnet** and enter the MDC IP address of the **other server**.
   - Leave the **Mirrored** checkbox checked.

   **Protocol tab:**
   - Click the **Protocol** tab and change the protocol type from **Any** to
     **TCP**.
   - Set the **From** port to **From this port** and enter `29005`.
   - Leave the **To** port as **To any port** and click **OK**.

4. Click **Add** again to create the inbound filter.

   **Addresses tab:**
   - Change **Source address** to **A specific IP Address or Subnet** and enter
     the MDC IP address of the **current server**.
   - Change **Destination address** to **A specific IP Address or Subnet** and
     enter the MDC IP address of the **other server**.
   - Leave the **Mirrored** checkbox checked.

   **Protocol tab:**
   - Click the **Protocol** tab and change the protocol type from **Any** to
     **TCP**.
   - Leave the **From** port as **From any port**.
   - Set the **To** port to **To this port**, enter `29005`, and click **OK**.

5. Verify there is one filter from port 29005 to any port, and one filter from
   any port to port 29005. Click **OK**.

   > Filtering is now configured to encrypt all TCP traffic that originates
   > from or is destined for port 29005 on either server.

6. Select the newly added filter list (e.g. *ECX Communication Port*).

---

## Filter Action Tab

7. Click the **Filter Action** tab. Uncheck **Use Add Wizard** and click
   **Add**.

   **Security Methods tab:**
   - On the **Security Methods** tab, leave **Negotiate security** selected and
     click **Add**.
   - Leave the default as **Integrity and encryption** and click **OK**. If
     other security methods are listed, move this entry to the top.

   > The default ESP confidentiality algorithm is **3DES** and the integrity
   > algorithm is **SHA1**. Both are considered weak by modern cryptographic
   > standards. To use stronger algorithms (e.g. AES-256, SHA-256), click
   > **Custom** instead of accepting the default, and select the desired
   > algorithms from the dropdowns.

   - Check **Use session key perfect forward secrecy (PFS)**.

   **General tab:**
   - Click the **General** tab and enter a name for the filter action, e.g.
     *ECX Communication Encryption*. Click **OK**.

8. Select the newly created filter action (e.g. *ECX Communication
   Encryption*).

---

## Authentication Methods Tab

9. Click the **Authentication Methods** tab and click **Add**.
10. Select **Use this string (preshared key)** and enter a secure key of your
    choosing.

    > The value *ECXSecurity* is used as a placeholder example only. **Use a
    > strong, unique key in production.** This same key must be entered on
    > both servers.

    Click **OK**.

11. If a Kerberos entry exists in the list, select the preshared key entry and
    move it **above** the Kerberos entry so it takes priority.
12. Click **Apply**, then click **OK**.

13. Verify that the newly created security rule is checked and click **OK**.

---

## Repeat on the Secondary Server

Before enabling the policy, **complete all steps above on the second server**
in the cluster. Use the same filter settings and the same preshared key.

---

## Enable the Policy on Both Servers

1. Before enabling encryption, **stop the cluster** to prevent mirroring
   errors. Skip this step if EXPRESSCLUSTER has not yet been configured.
2. Open the **IP Security Policy Management** snap-in and select **IP Security
   Policies on Local Computer**.
3. Right-click the policy (e.g. *ECX IP Security*) and click **Assign**.
   Repeat on the other server.

   > Only one policy can be assigned at a time on each server.

4. If the cluster was stopped, start it again.

---

## Verify Encryption

**Option 1: IP Security Monitor (MMC snap-in)**

1. Open MMC (**Windows key + R** → `mmc`).
2. Add the **IP Security Monitor** snap-in.
3. Expand the server node and check **Main Mode** and **Quick Mode**. Active
   security associations (SAs) will appear here when the policy is working
   correctly.

**Option 2: Network protocol analyzer (e.g. Wireshark)**

1. Capture traffic on the MDC network interface.
2. Filter for traffic between the two MDC IP addresses.
3. Packets should show protocol **ESP** (Encapsulating Security Payload) rather
   than plain TCP, confirming that encryption is active.
