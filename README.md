# 📡 Cisco Packet Tracer: Home Wireless Router & Client Configuration

A hands-on networking lab demonstrating the end-to-end setup of a SOHO (Small Office/Home Office) network using Cisco Packet Tracer. This project covers physical media connections (coaxial, copper straight-through), SOHO wireless router configuration, WPA2-Personal security implementation, DHCP scope management, and end-to-end connectivity verification.

---

## 🎯 Lab Objectives

* **Part 1: Physical Layer Connectivity**
  * Connect WAN infrastructure using Coaxial media via Cable Splitter to Modem and TV.
  * Establish LAN wired links using Copper Straight-Through cables for SOHO router and host PCs.
* **Part 2: SOHO Router Setup & Hardening**
  * Access SOHO router GUI using dynamic DHCP default gateway addressing.
  * Reconfigure administrative authentication credentials.
  * Manage DHCP pool limits to restrict active leases.
  * Enable 2.4 GHz wireless radio, assign custom SSID, and secure via WPA2-Personal (AES/PSK).
* **Part 3: Host Configuration & Verification**
  * Provision wireless client connectivity on laptop host via PC Wireless interface.
  * Verify dynamic IPv4 address allocation across all endpoints.
  * Test WAN-edge web connectivity via simulated FQDN (`skillsforall.srv`).

---

## 🛠️ Network Topology & Architecture Overview

```
                          [ Internet / ISP ]
                                  |
                           (Coaxial Cable)
                                  |
                         [ Cable Splitter ]
                         /                \
          (Coaxial Cable)                  (Coaxial Cable)
                /                                \
             [ TV ]                         [ Cable Modem ]
                                                  |
                                       (Straight-Through Cable)
                                                  |
                                     [ Home Wireless Router ]
                                      /          |         \
                   (Straight-Through)  (Straight-Through)  (Wi-Fi 2.4 GHz WPA2)
                                 /               |               \
                       [ Office PC ]       [ Bedroom PC ]      [ Laptop ]
```

---

## 🚀 Execution Steps & Configuration Flow

### Phase 1: Physical Connections
1. **Coaxial Connections:**
   * `Cable Splitter` (`Coaxial1`) ➔ `Cable Modem` (`Port 0`)
   * `Cable Splitter` (`Coaxial2`) ➔ `TV` (`Port 0`)
2. **Wired Ethernet Connections:**
   * `Cable Modem` (`Port 1`) ➔ `Home Wireless Router` (`Internet Port`)
   * `Office PC` (`FastEthernet0`) ➔ `Home Wireless Router` (`GigabitEthernet 1`)
   * `Bedroom PC` (`FastEthernet0`) ➔ `Home Wireless Router` (`GigabitEthernet 2`)

### Phase 2: SOHO Router Hardening & WLAN Setup
1. **GUI Access:** Accessed `Office PC`, enabled DHCP to receive a `192.168.x.x` lease, and navigated to the Default Gateway IP in the web browser.
2. **DHCP Scope Modification:** Restricted `Maximum Number of Users` to **10** under `Setup > Network Setup` to minimize the attack surface.
3. **Administrative Hardening:** Updated default `admin` credentials to `MyPassword1!` under the `Administration` tab.
4. **WLAN Configuration:**
   * **SSID:** `MyHome` (2.4 GHz Radio Enabled)
   * **Security Standard:** WPA2-Personal
   * **Pre-Shared Key (PSK):** `MyPassPhrase1!`

### Phase 3: Endpoint Provisioning & Verification
1. **Wireless Laptop Provisioning:** Connected `Laptop` to SSID `MyHome` via `Desktop > PC Wireless`, authenticated using the pre-shared passphrase, and confirmed `192.168.x.x` lease assignment.
2. **Connectivity Validation:** Verified complete HTTP/DNS network traversal across `Office PC`, `Bedroom PC`, and `Laptop` by querying `http://skillsforall.srv`.

---

## 🔍 Key Security & Engineering Takeaways

* **Credential Management:** Default SOHO router credentials (`admin/admin`) pose an immediate security threat and must be updated upon initial setup to prevent unauthorized administrative takeover.
* **DHCP Pool Optimization:** Limiting the maximum number of leases reduces unauthorized rogue host access on small local networks.
* **WLAN Security Standard:** WPA2-Personal provides robust encryption over legacy standards (WEP/WPA), ensuring pre-shared key security for home wireless clients.
