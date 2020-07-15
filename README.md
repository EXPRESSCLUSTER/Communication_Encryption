Data being mirrored between two EXPRESSCLUSTER servers is currently unencrypted. One way to provide a more secure data stream is through a VPN connection. 3rd party VPN software exists but can be expensive or complicated to set up. Windows servers have a VPN feature which can be installed and configured without too much difficulty. Another method to provide encryption on the mirrored data stream is to create an IP Security Policy (IPsec) which will automatically encrypt ECX mirrored communication. IPsec is often used in site to site VPN. It provides security at the IP packet level and provides data authentication, integrity, and confidentiality. This project includes instructions on how to set up a basic VPN server which can be used with EXPRESSCLUSTER to securely transfer data between two ECX servers. It also provides steps to set up an IP Security Policy to securely pass mirrored data between two ECX servers.   

\*Note that the configuration guide is just one of many variations on how to configure a VPN server. An IP Security Policy also has other settings which can be configured. All testing was done on Microsoft Windows 2019 Servers.
 

# Windows VPN

![Configuration](ECX%20VPN%20LAN%20Cluster.png)

[Set up the VPN server](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Set%20up%20VPN%20Server.md)   

[Set up the VPN client](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Set%20up%20VPN%20client.md)    

# IP Security Policy

[Set up IP Security Policy using the configuration wizard[(https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Create%20IP%20Security%20Policy.md)
