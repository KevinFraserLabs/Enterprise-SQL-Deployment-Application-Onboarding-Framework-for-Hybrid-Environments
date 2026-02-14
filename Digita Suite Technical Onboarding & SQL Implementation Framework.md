## 🧩 Virtual Machine (VM) and Network Setup

To simulate the customer’s IT environment for the PracticeSuite Pro deployment, I built a dedicated virtual lab using Hyper‑V on my host PC. This provides a controlled setup where I can test the full installation and configuration process end‑to‑end.

---

### **1. Internal Network Configuration**

To create an isolated internal network for the lab, I configured a dedicated Hyper‑V internal switch and assigned a static IP to the host’s vEthernet adapter. NAT was then configured to provide internet access to all VMs.

**Configuration:**

- **Internal Switch Name:** `GF-Lab-Network`
- **Host vEthernet Adapter IP:** `192.168.2.1/24`
- **Lab Subnet:** `192.168.2.0/24`
- **NAT Name:** `GF-Lab-NAT`

#### **PowerShell NAT Configuration**

```powershell
New-NetNat -Name "GF-Lab-NAT" -InternalIPInterfaceAddressPrefix 192.168.2.0/24
```

<img width="719" height="677" alt="Screenshot 2026-02-14 113059" src="https://github.com/user-attachments/assets/a6c4edae-5f86-4b84-b1f4-c5e466a6b2b4" />
<img width="733" height="469" alt="Screenshot 2026-02-14 113226" src="https://github.com/user-attachments/assets/de9e5dc1-aa4d-4b2d-91bc-495dc3a433a3" />

### **2. Domain Control Server (DC)**

| Service | Configuration | IP Address |
| :--- | :--- | :--- |
| **VM Name** | DC (Created first VM) | `192.168.2.2` (Static) |
| **Operating System** | Windows Server 2022 (ISO used) | N/A |
| **Gateway** | `192.168.2.1` | N/A |
| **Public DNS** | `8.8.8.8` (Used for Internet Connectivity) | N/A |
| **Domain** | **Root Domain:** `GreenfieldAccountancyLtd.com` | N/A |


<img width="1267" height="706" alt="Screenshot 2026-02-14 131956" src="https://github.com/user-attachments/assets/a56a721a-49c5-4584-aed9-b5c84e34ab9f" />




#### **Core Services Configuration**

* **Active Directory:** Enabled and server promoted to a Domain Controller.

<img width="1768" height="838" alt="Screenshot 2025-11-13 164251" src="https://github.com/user-attachments/assets/abaf4625-fadc-4234-90fe-0e6e25f7e075" />


* **DNS Server:** Enabled with Forward and Reverse Lookup Zones. Hostname and IP confirmed resolving.

<img width="1220" height="566" alt="Screenshot 2025-11-13 171625" src="https://github.com/user-attachments/assets/b008c3e0-2eaf-4a31-bdfe-9b10944bced5" />


* **DHCP Server:** Enabled.
    * **Scope Range:** `192.168.2.4` to `192.168.2.10`.

<img width="1903" height="1023" alt="Screenshot 2025-11-13 165722" src="https://github.com/user-attachments/assets/fbd07250-7980-4493-a55d-6aef02075493" />

  

---



