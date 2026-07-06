# Create an IP Security Policy on Windows Servers (Wizard Method)

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
5. Leave the **Edit properties** box checked and click **Finish**.
6. In the policy properties dialog, click **Add** to add a security rule.
   Make sure **Use Add Wizard** is checked.
7. Click **Next** on the wizard welcome screen.
8. On the **Tunnel Endpoint** screen, leave the default (**This rule does not
   specify a tunnel**) and click **Next**.
9. Select **All network connections** for the network type and click **Next**.

### Add IP Filters

Two filters are required: one for **outbound** traffic (originating from port
29005) and one for **inbound** traffic (destined for port 29005). Steps 10–19
add the outbound filter; steps 20–28 add the inbound filter.

**Outbound filter (from port 29005):**

10. Click **Add** to create a new IP filter list.
11. Enter a name for the filter list, e.g. *ECX Communication Port*. Make sure
    **Use Add Wizard** is checked and click **Add**.
12. Click **Next** on the welcome screen.
13. Leave the **Mirrored** box checked and click **Next**.
14. Change **Source address** to **A specific IP Address or Subnet** and enter
    the MDC IP address of the **current server**. Click **Next**.
15. Change **Destination address** to **A specific IP Address or Subnet** and
    enter the MDC IP address of the **other server**. Click **Next**.
16. Change the **protocol type** to **TCP** and click **Next**.
17. Set the **From** port to **From this port** and enter `29005`.
18. Leave the **To** port as **To any port** and click **Next**.
19. Click **Finish**.

**Inbound filter (to port 29005):**

20. Click **Add** again to add the second filter. Make sure **Use Add Wizard**
    is checked.
21. Click **Next** on the welcome screen.
22. Leave the **Mirrored** box checked and click **Next**.
23. Change **Source address** to **A specific IP Address or Subnet** and enter
    the MDC IP address of the **current server**. Click **Next**.
24. Change **Destination address** to **A specific IP Address or Subnet** and
    enter the MDC IP address of the **other server**. Click **Next**.
25. Change the **protocol type** to **TCP** and click **Next**.
26. Leave the **From** port as **From any port**.
27. Set the **To** port to **To this port**, enter `29005`, and click **Next**.
28. Click **Finish**.

    > Filtering is now configured to encrypt all TCP traffic that originates
    > from or is destined for port 29005 on either server.

29. Review the two filters and click **OK**.
30. Select the newly added filter list (e.g. *ECX Communication Port*) and
    click **Next**.

### Add Filter Action

31. In the **Filter Action** window, make sure **Use Add Wizard** is checked
    and click **Add**.
32. Click **Next** on the welcome screen.
33. Enter a name for the filter action, e.g. *ECX Communication Encryption*.
    Click **Next**.
34. Set the behavior to **Negotiate security** and click **Next**.
35. Leave the default (**Do not allow unsecured communication**) and click
    **Next**.
36. Leave **IP Traffic Security** set to **Integrity and encryption** and click
    **Next**.

    > The default ESP confidentiality algorithm is **3DES** and the integrity
    > algorithm is **SHA1**. Note that 3DES and SHA1 are considered weak by
    > modern cryptographic standards. If your security policy requires stronger
    > algorithms, use the [manual configuration method](Create%20Manual%20IPsec%20Policy.md),
    > which exposes additional algorithm options such as AES and SHA-256.

37. Check **Edit properties** and click **Finish**.
38. Check **Use session key perfect forward secrecy (PFS)** and click **OK**.
39. Select the newly created filter action (e.g. *ECX Communication
    Encryption*) and click **Next**.

### Set Authentication Method

40. On the **Authentication Method** screen, select **Use this string to
    protect the key exchange (preshared key)** and enter a secure key of your
    choosing.

    > The value *ECXSecurity* is used as a placeholder example only. **Use a
    > strong, unique key in production.** This same key must be entered on both
    > servers.

41. Click **Next**, then click **Finish**.
42. Verify that the security rule just created is checked and click **OK**.

---

## Repeat on the Secondary Server

Before enabling the policy, **complete all steps above on the second server**
in the cluster. Use the same filter settings (swapping source and destination
IP addresses where appropriate — note that the **Mirrored** checkbox handles
bidirectionality, so the addresses can be entered the same way on both servers)
and the same preshared key.

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
