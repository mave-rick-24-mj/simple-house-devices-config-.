# 📡 Cisco Packet Tracer: SOHO Network Deployment & Connectivity Verification

This documentation covers the step-by-step workflow for deploying, securing, and testing a SOHO (Small Office/Home Office) network inside Cisco Packet Tracer.

---

## 🛠️ Phase 1: Physical Topology & Device Layout

The physical environment is structured into distinct zones across a residential setup, connecting broadband WAN to local LAN hosts.

<p align="center">
  <img src="assets/houselay out.jpg" width="100%" alt="Packet Tracer Physical Layout" />
</p>

* **WAN Ingress:** Coaxial connection entering via the **Cable Splitter**, delivering internet data to the **Cable Modem** and video signal to the **TV**.
* **Core Distribution:** The **Cable Modem** bridges to the **Home Wireless Router** via a Copper Straight-Through cable.
* **Wired LAN Endpoints:** 
  * `Office PC` connected to `GigabitEthernet 1`
  * `Bedroom PC` connected to `GigabitEthernet 2`
* **Wireless LAN Endpoint:** `Laptop` provisioned over 2.4 GHz Wi-Fi.

---

## ⚙️ Phase 2: Dynamic IP Addressing (DHCP Provisioning)

Once the network infrastructure is established, endpoints dynamically request IPv4 configurations from the Home Wireless Router's DHCP server pool (`192.168.0.0/24`).

<table align="center" width="100%">
  <tr>
    <td width="50%" align="center" valign="top">
      <h4>Office PC Configuration</h4>
      <img src="assets/office pc.png" width="100%" alt="Office PC IP Settings" />
      <p align="left">
        <b>Interface:</b> FastEthernet0<br>
        <b>IPv4 Address:</b> <code>192.168.0.3</code><br>
        <b>Subnet Mask:</b> <code>255.255.255.0</code><br>
        <b>Default Gateway:</b> <code>192.168.0.1</code><br>
        <b>DNS Server:</b> <code>209.165.200.230</code>
      </p>
    </td>
    <td width="50%" align="center" valign="top">
      <h4>Laptop Wireless Configuration</h4>
      <img src="assets/ip laptop.jpg" width="100%" alt="Laptop IP Settings" />
      <p align="left">
        <b>Interface:</b> Wireless0<br>
        <b>IPv4 Address:</b> <code>192.168.0.2</code><br>
        <b>Subnet Mask:</b> <code>255.255.255.0</code><br>
        <b>Default Gateway:</b> <code>192.168.0.1</code><br>
        <b>DNS Server:</b> <code>209.165.200.230</code>
      </p>
    </td>
  </tr>
</table>

---

## 🧪 Phase 3: Cross-Subnet Ping & Connectivity Testing

To confirm full L3 communication across both wired and wireless segments, ICMP echo requests were issued from the endpoint command prompts.

<p align="center">
  <img src="assets/ping .png" width="100%" alt="Ping Verification Tests" />
</p>

### Verification Results:
1. **Bedroom PC (`192.168.0.3`) ➔ Office PC (`192.168.0.4`):**
   * **Packets Sent:** 4 | **Received:** 4 | **Loss:** 0% (0ms avg)
2. **Office PC (`192.168.0.4`) ➔ Bedroom PC (`192.168.0.3`):**
   * **Packets Sent:** 4 | **Received:** 4 | **Loss:** 0% (0ms avg)

---

## 📊 Summary of Network Diagnostic Data

| Endpoint Device | Interface Type | Config Mode | Assigned IPv4 | Subnet Mask | Gateway IP |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Home Wireless Router** | LAN / Gateway | Static | `192.168.0.1` | `255.255.255.0` | N/A |
| **Laptop** | Wireless0 | DHCP | `192.168.0.2` | `255.255.255.0` | `192.168.0.1` |
| **Bedroom PC** | FastEthernet0 | DHCP | `192.168.0.3` | `255.255.255.0` | `192.168.0.1` |
| **Office PC** | FastEthernet0 | DHCP | `192.168.0.4` | `255.255.255.0` | `192.168.0.1` |
