# Create an IP Security Policy on Windows servers (using the wizard)
## Open the IP Security Policy Management snap-in
01. Open the **Microsoft Management Console** by accessing the **Run** menu (Windows key + R), enter '**MMC**', and click **OK**.
02. Click **File** and select **Add/Remove Snap-in...**.
03. Scroll down the **Available snap-ins** to find and select **IP Security Policy Management**. Click **Add**.
04. Leave the **default (Local computer)** selected and click **Finish**.
05. Click **OK**.
## Create IP Security Policy
01. Right click **IP Security Policies** on **Local Computer** and click on **Create IP Security Policy...**
02. Click **Next** in the **Welcome screen**.
03. Enter a name for the new **IP Security Policy** e.g. *ECX IP Security*. Click **Next**.
04. In the **Requests for Secure Communication** window click **Next** without checking the box.
05. Leave the **Edit properties** box checked and click **Finish**.
06. Click the **Add** button to add an **IP Security rule**, leaving the **Use Add Wizard** box checked.
07. Click **Next** on the wizard welcome screen.
08. Leave the default selection of **This rule does not specify a tunnel** in the **Tunnel Endpoint** window and click **Next**.
09. Select **All network connections** for the **Network Type** and click **Next**.
10. Click **Add** to include filters for the **IP Filter List**.
11. Enter a name for the filter list. e.g. *ECX Communication Port*. Check the **Use Add Wizard** box and click **Add**.
12. Click **Next** in the welcome window.
13. Leave the **Mirrored** box checked and click **Next**.
14. Change the **Source address** to **A specific IP Address or Subnet** and enter the IP address used for mirrored communication (ECX MDC) on the current server. Click **Next**.
15. Change the **Destination address** to **A specific IP Address or Subnet** and enter the IP address of the ECX MDC of the other server. Click **Next**.
16. Change the **protocol type** to **TCP** and click **Next**.
17. Set the **From** IP protocol port to **From this port:** and enter **29005**.
18. Leave the **To** IP protocol port as **To any port** and click **Next**.
19. Click **Finish**.
20. Leave the **Use Add Wizard** box checked and click **Add** to add another filter.
21. Click **Next** on the welcome screen.
22. Leave the **Mirrored** box checked and click **Next**.
23. Change the **Source address** to **A specific IP Address or Subnet** and enter the IP address used for mirrored communication (ECX MDC) on the current server. Click **Next**.
24. Change the **Destination address** to **A specific IP Address or Subnet** and enter the IP address of the ECX mDC of the other server. Click **Next**.
25. Change the **protocol type** to **TCP** and click **Next**.
26. Leave the **From** IP protocol port as **From any port**.
27. Set the **To** IP protocol port as **To this port**, enter **29005**, and click **Next**.
28. Click **Finish**.
29. Review the two new filters and click **OK**.
30. Select the newly added filter (e.g. *ECX Communication Port*) and click **Next**.
31. In the **Filter Action** window, click the **Use Add Wizard** box and click **Add**.
32. Click **Next** in the **Welcome** window.
33. Enter a name for the **Filter Action** e.g. *ECX Communication Encryption*, and click **Next**.
34. Set the **filter action behavior** to **Negotiate security** and click **Next**.
35. Leave the default setting as **Do not allow unsecured communication** and click **Next**.
36. Leave the **IP Traffic Security** set to **Integrity and encryption** and click **Next**.   
    (the default ESP confidentiality method is 3DES and integrity method is SHA1)
37. Check the **Edit properties** box and click **Finish**.
38. Check **Use session key perfect forward secrecy (PFS)** and click **OK**.
39. Select the newly created filter action (e.g. *ECX Communication Encryption*) and click **Next**.
40. In the **Authentication Method** window, select **Use this string to protect the key exchange (preshared key):** and enter a string, e.g. *ECXSecurity*. Click **Next**.
41. Click **Finish**.
42. Verify that the security rule just created is checked, and click **OK**.
43. **Repeat all steps above on the secondary server.**
## Enable the policy on both servers
01. Open the **IP Security Policy Management** snap-in and select **IP Security Policies on Local Computer** to display all security policies.
02. Right click on the policy recently created (e.g. *ECX IP Security*) and click **Assign**. Repeat on the other server.    
    \*Note that only one policy can be assigned at a time.
## Encryption verification
01. Use the IP Security Monitor snap-in for MMC.
02. Use a network protocol analyzer. The protocol for an encrypted packet should be ESP (Encapsulating Security Payload).
