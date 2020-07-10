# Create and IP Security Policy on Windows servers
## Open the IP Security Policy Management snap-in
01. Open the **Microsoft Management Console** by accessing the **Run** menu (Windows key + R), enter '**MMC**', and click **OK**.
02. Click **File** and select **Add/Remove Snap-in...**.
03. Scroll down the **Available snap-ins** to find and select **IP Security Policy Management**. Click **Add**.
04. Leave the **default (Local computer)** selected and click **Finish**.
05. Click **OK**.
## Create IP Security Policy
06. Right click IP Security Policies on Local Computer and click on Create IP Security Policy...
07. Click Next in the Welcome screen
08. Enter a name for the new IP Security Policy e.g. ECX IP Security. Click Next.
09. In the Requests for Secure Communication window click Next without checking the box.
10. Leave the Edit properties box checked and click Finish.
11. Click the Add button to add an IP Security rule, leaving the Use Add Wizard box checked.
12. Click Next on the wizard welcome screen.
13. Leave the default selection of 'This rule does not specify a tunnel' in the Tunnel Endpoint window and click Next.
14. Select 'All network connections' for the Network Type and click Next.
15. Click Add to include filters for the IP Filter List.
16. Enter a name for the filter list. e.g. ECX Communication Port. Check the 'Use Add Wizard' box and click Add.
17. Click Next in the welcome window.
18. Leave the Mirrored box checked and click Next.
19. Change the 'Source address' to 'A specific IP Address or Subnet' and enter the IP address used for mirrored communication on the current server. Click Next.
20. Change the 'Destination address' to 'A specific IP Address or Subnet' and enter the IP address of the other server. Click Next.
21. Change the protocol type to TCP and click Next.
22. Set the 'From' IP protocol port to 'From this port:' and enter 29005.
23. Leave the 'To' IP protocol port as 'To any port' and click Next.
24. Click Finish.
25. Leave the 'Use Add Wizard' box checked and click Add to add another filter.
26. Click Next on the welcome screen.
27. Leave the Mirrored box checked and click Next.
28. Change the 'Source address' to 'A specific IP Address or Subnet' and enter the IP address used for mirrored communication on the current server. Click Next.
29. Change the 'Destination address' to 'A specific IP Address or Subnet' and enter the IP address of the other server. Click Next.
30. Change the protocol type to TCP and click Next.
31. Leave the 'From' IP protocol port as 'From any port'.
32. Set the 'To' IP protocol port as 'To this port', enter 29005, and click Next.
33. Click Finish.
34. Review the two new filters and click OK.
35. Select the newly added filter (e.g. ECX Communication Port) and click Next.
36. In the Filter Action window, click the 'Use Add Wizard' box and click Add.
37. Click Next in the Welcome window.
38. Enter a name for the Filter Action e.g. ECX Communication Encryption, and click Next.
39. Set the filter action behavrio to 'Negotiate security' and click Next.
40. Leave the default setting as 'Do not allow unsecured communication' and click Next.
41. Leave the IP Traffic Security set to 'Integrity and encryption' and click Next.   
    (the default ESP confidentiality method is 3DES and integrity method is SHA1)
42. Check the 'Edit properties' box and click Finish.
43. Check 'Use session key perfect forward secrecy (PFS) and click OK.
44. Select the newly created filter action (e.g. ECX Communication Encryption) and click Next.
45. In the Authentication Method window, select 'Use this string to protect the key exchange (preshared key):' and enter a string, e.g. ECXSecurity. Click Next.
46. Click Finish.
47. Verify that the security rule just created is checked, and click OK.
48. Repeat all steps above on the secondary server.
## Enable the policy on both servers
Open the IP Security Policy Management snap-in and select 'IP Security Policies on Local Computer' to display all security policies.
Right click on the policy recently created and click Assign. Repeat on the other server.
\*Note that only one policy can be assigned at a time.
