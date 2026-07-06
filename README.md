# EXPRESSCLUSTER Mirrored Data Encryption

By default, data mirrored between two EXPRESSCLUSTER servers is unencrypted.
This project documents two methods to encrypt the mirrored data stream on
Windows Server:

- **IP Security Policy (IPsec)** — encrypts at the IP packet level using
  Windows' built-in IPsec engine. Provides data authentication, integrity,
  and confidentiality. Commonly used in site-to-site VPN scenarios.
- **Windows VPN (L2TP/IPsec)** — establishes an encrypted tunnel between
  servers using Windows' built-in VPN server/client feature. No third-party
  software required.

> All testing was performed on **Windows Server 2019**. The configurations
> shown represent one working example; other valid configurations exist.

---

## Prerequisites

- Two-node EXPRESSCLUSTER cluster configured with a Mirror Disk Connection (MDC)
- Administrator access on both servers
- Active Directory domain (required for VPN user account configuration)

---

## Which Method Should I Use?

See [Comparison and Recommendations](Final_Notes.md) for a side-by-side
discussion of both methods, including known limitations of the VPN approach.
**IPsec is recommended for most deployments.**

---

## IP Security Policy (IPsec)

![Configuration](ECX%20IPsec%20LAN%20Cluster.png)

- [Set up IP Security Policy using the wizard](Create%20IP%20Security%20Policy.md)
- [Set up IP Security Policy manually](Create%20Manual%20IPsec%20Policy.md)
  *(provides a detailed look at all configuration options)*

---

## Windows VPN

![Configuration](ECX%20VPN%20LAN%20Cluster.png)

- [Set up the VPN server](Set%20up%20VPN%20Server.md)
- [Set up the VPN client](Set%20up%20VPN%20client.md)

---

## Mirroring Performance With Encryption

Encrypted mirroring performance was evaluated by varying RAM, CPU count, and
block size using iometer, CrystalDiskMark, and DiskSpd.

**Result: encrypted mirroring peaks at approximately 10 MB/sec regardless of
hardware configuration.** Increasing RAM or CPU count does not improve
throughput, suggesting the encryption workload runs at a fixed resource
allocation rather than scaling with available hardware. This solution is
suitable for environments where 10 MB/sec is acceptable.
