# Synchronize SonicWall Licenses

Once the NSv is up and running, the next step is to access the management interface using the default IP address (`192.168.168.168`) and credentials. From there, we can proceed with license synchronization.

SonicOS supports two activation modes:
- **Online:** Requires WAN internet connectivity (used in this setup).
- **Offline:** Manual key entry via SonicWall Knowledge Base articles.

Since WAN connectivity was already verified on my NSv, I proceeded with the online method. The process was straightforward — see below for the exact steps taken.

### 1. Navigate to License Manager

Once logged in, go to **Device → Settings → Licenses**.

![License Manager Location](https://github.com/user-attachments/assets/a62a0404-212c-4d43-bee6-c38ea1ca9ea9)

### 2. Connect to MySonicWall

Click **MySonicWall**. You will be redirected to the official SonicWall portal. Enter your registered account credentials and click **LOGIN**.

![MySonicWall Portal](https://github.com/user-attachments/assets/8c53acc7-17c0-472c-8c1d-823a6bfaf4e6)

### 3. Authenticate and Sync

After successful authentication, you will see your account details. Return to the firewall interface and click the **Synchronize** button.

![Sync Button](https://github.com/user-attachments/assets/6e5cd371-1e15-434d-ac09-05e67c09cad2)

The NSv will automatically pull down and activate all your registered licenses.

![Synchronization in Progress](https://github.com/user-attachments/assets/12ccbd07-afd6-48cb-9144-65e99fb0466e)

---

### Result

Once the sync completes, all licensed services — **IPS, Anti-Malware, Gateway Anti-Virus, and Content Filter** — are immediately available.

![Licenses Activated](https://github.com/user-attachments/assets/cb7ffe81-e830-4726-9740-840a0fb38782)

*Status check: All modules now show as Active.*

![License Status Check](https://github.com/user-attachments/assets/ff850760-6acd-49a6-ad29-151fe951209f)

---

[< Back to Home Lab Guide](../README.md)
