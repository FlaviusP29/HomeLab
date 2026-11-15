# Hardening SonicWall NSv Security

With licenses successfully synchronized, the next phase of the build focused on hardening the firewall's security posture. This involved enabling critical security services and locking down management access to prevent unauthorized administrative control.

## 1. Enabling Security Services

Using the newly activated licenses, I enabled the core protection suites to ensure deep packet inspection and threat prevention are active on all traffic flows.

| Service | Status | Purpose |
| :--- | :---: | :--- |
| **Intrusion Prevention (IPS)** | On | Detects and blocks malicious network activity. |
| **Gateway Anti-Virus** | On | Scans inbound traffic for malware and viruses. |
| **Anti-Spyware** | On | Prevents communication with known command-and-control servers. |
| **Content Filter** | On | Filters web content based on category policies. |
| **DPI SSL / SSH** | On | Inspects encrypted traffic for hidden threats. |

> *Note: With DPI enabled, the firewall can now inspect HTTPS traffic for deeper visibility.*

<img width="600" height="641" alt="image" src="https://github.com/user-attachments/assets/93f2d5d2-96d3-488f-989f-15d3dc580af9" />


## 2. Management Interface Hardening

By default, SonicOS allows management via standard ports (HTTP/HTTPS). To reduce the attack surface, I implemented strict controls over how the device can be accessed.

### Changing the Management Port
I changed the default management port from `443` to a non-standard custom port. This effectively hides the interface from automated internet scanners that target default configurations.

### Forcing HTTPS & Disabling HTTP
- **HTTP:** Completely disabled to prevent credentials being sent in clear text.
- **HTTPS:** The only allowed protocol for GUI access.
- **Redirection:** Any attempt to connect via HTTP is automatically redirected to HTTPS.

## 3. Restricting Access with "FWMGMT" Object

To ensure that **only my workstation** can manage the firewall via the WAN interface, I created a specific address object and applied it to an Access Rule.

### Step A: Create the Address Object
Created a Network Object named `FWMGMT` containing the static IP of the host PC.

<img width="1286" height="34" alt="image" src="https://github.com/user-attachments/assets/78ca9b54-8660-4196-98ea-7c49bb685a49" />


### Step B: Configure the Access Rule
Created a rule allowing traffic from `WAN` to `LAN` (Management) specifically for the `FWMGMT` object. All other management attempts are dropped by the implicit deny rules.

*   **Action:** Allow
*   **From Zone:** WAN
*   **To Zone:** WAN
*   **Source:** `FWMGMTACCESS` (My Host IP)
*   **Service:** HTTPS MANAGEMENT (Custom Port)

<img width="1096" height="649" alt="image" src="https://github.com/user-attachments/assets/82ccce94-bad6-4c9f-9e01-917e228ce202" />

## Conclusion
The firewall is now hardened against external brute-force attacks and unauthorized configuration changes. Management is restricted to a single IP address over an encrypted channel on a non-standard port.

---
*Previous: [Synchronize Licenses](../Synchronize_Licenses/README.md)*
