# EXPRESSCLUSTER mirrored data encryption
Data being mirrored between two EXPRESSCLUSTER servers is currently unencrypted. Two different methods to encrypt the data have been investigated. One method to provide encryption on the mirrored data stream is to create an IP Security Policy (IPsec) in Windows which will automatically encrypt ECX mirrored communication once configured. IPsec is often a standard used in site to site VPN. It provides security at the IP packet level and provides data authentication, integrity, and confidentiality. Another way to provide a more secure data stream is through a VPN connection. 3rd party VPN software exists but can be expensive or complicated to set up. Windows servers have a VPN feature which can be installed and configured without too much difficulty, providing a secure connection between a client and server using a tunneling protocol. The VPN client makes a virtual call to a virtual port on a VPN server. This project provides steps on how to set up an IP Security Policy to securely pass mirrored data between two ECX servers. Instructions on how to set up a basic VPN server which can be used with EXPRESSCLUSTER to securely transfer data between two ECX servers are also included.    

\*Note that the configuration guide shows just one way an IP Security Policy can be configured. Other configuration options are possible. The VPN instruction also shows just one of many variations on how to configure a VPN server. All testing was done on Microsoft Windows 2019 Servers.
 
[Which method should I use?](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Final_Notes.md)

# IP Security Policy

![Configuration](ECX%20IPsec%20LAN%20Cluster.png)

[Set up IP Security Policy using the configuration wizard](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Create%20IP%20Security%20Policy.md)

[Set up up IP Security Policy manually](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Create%20Manual%20IPsec%20Policy.md) (For an inside look at the configuration options)

# Windows VPN

![Configuration](ECX%20VPN%20LAN%20Cluster.png)

[Set up the VPN server](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Set%20up%20VPN%20Server.md)   

[Set up the VPN client](https://github.com/EXPRESSCLUSTER/Communication_Encryption/blob/master/Set%20up%20VPN%20client.md)    

# Mirroring Performance With Encryption
We have evaluated encrypted mirroring performance on EXPRESSCLUSTER by changing RAM size, # of CPUs, and block size, using disk performance measuring tools such as iometer, CrystalDiskMark and DiskSpd. Even with configuration changes, encrypted mirroring seems to perform at about 10MB/sec at most. We assume that the encryption process is executed with a fixed RAM and CPU size because an increase to RAM and CPU size does not affect encrypted mirroring performance. Customers can use our solution if 10MB/sec is enough for their environment.
