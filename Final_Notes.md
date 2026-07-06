# Which Method Should I Use?

## Recommendation

**IPsec is the recommended method for most deployments.** It integrates more
cleanly with EXPRESSCLUSTER, reconnects automatically after a server restart,
and requires no changes to the MDC configuration.

Use VPN only if a specific network requirement — such as routing over a WAN
where IPsec traffic is blocked — makes it necessary.

---

## IP Security Policy (IPsec)

**Advantages:**

- The encrypted connection is restored automatically when either server
  restarts — no manual intervention or workarounds needed.
- No changes to the EXPRESSCLUSTER MDC configuration are required.
- Configuration is contained entirely within Windows with no additional
  software.

**Disadvantage:**

- The wizard-based setup involves more steps than the VPN setup, though a
  [manual configuration guide](Create%20Manual%20IPsec%20Policy.md) is also
  provided for reference.

---

## Windows VPN

**Advantage:**

- Quicker initial setup compared to configuring an IPsec policy.

**Limitations:**

1. **MDC configuration requires the VPN to already be connected.**
   When configuring the Mirror Disk Connection in the Cluster WebUI, the VPN
   must be active because mirror disk communication uses the virtual IP
   addresses assigned by the VPN tunnel — not the physical MDC IP addresses.
   A new MDC connection must be created in the Cluster WebUI using those
   virtual IPs and given the highest priority. In some cases this step may
   not apply cleanly and a workaround is required.

2. **The VPN client does not reconnect automatically after the client server
   restarts.**
   Workaround: create a Task Scheduler task on the client machine to run the
   following command at OS startup:
   ```
   C:\Windows\System32\rasdial.exe <VPN Connection Name>
   ```
   This handles restarts of the client server only — it does not handle
   restarts of the VPN server.

3. **The VPN client does not reconnect automatically if the VPN server
   restarts.**
   Workaround: configure a monitor resource in EXPRESSCLUSTER to detect VPN
   disconnection and periodically retry the connection using `rasdial.exe`.
   No automated solution for this case is provided in this guide.
