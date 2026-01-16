## ✅ Student checklist (read first)

Before the workshop, make sure you have:

* ⬜ A **Windows laptop (Windows 10 or 11)**
* ⬜ **VMware Workstation Pro** installed
* ⬜ At least **16 GB RAM** (8 GB minimum, but 16 strongly recommended)
* ⬜ At least **70 GB free disk space** (120 GB recommended)
* ⬜ A stable internet connection

> ⚠️ Mac users with **M-series (M1/M2/M3)** CPUs must use the **ARM version** of the lab.

---
## Step 1 — Install VMware Workstation (if needed)

Download from [TechSpot](https://www.techspot.com/downloads/189-vmware-workstation-for-windows.html):
* VMware Workstation Pro 17.6.3

>You can download directly from VMware, now Broadcom, but you'll need to make an account.

During install:
* Accept defaults
* Reboot if prompted

No license key required for this workshop.

---
## Step 2 — Download the lab image

Download the .tar and SHA256 checksum from the provided Google Drive link:

```
dfth-workshop
> dfth-workshop-x64.tar
> dfth-workshop-x64-sha256.txt
```

⚠️ **Important**

* Select Download anyway
* Download the contents **fully** before importing
* Do **not** open it directly from Google Drive

Expected size: ~30 GB

Google Drive . This will take some **time**.

---
## (Optional but recommended) Step 2.5 — Verify the download

If you want to confirm the file downloaded correctly:
### On Windows (PowerShell):

```powershell
Get-FileHash dfth-workshop-x64.tar -Algorithm SHA256
```

Compare the output to the checksum in `dfth-workshop-x64-sha256.txt`

If it matches, your download is intact.

---
## Step 3 — Import the virtual machine

1. Extract the contents of `dfth-workshop-x64.tar` 
2. Open **VMware Workstation**
3. Click `File → Open...`
4. Double-click the folder and select the file that appears.
5. Choose "I copied it" if prompted.
6. If a SATA warning comes up, click No.
7. Wait for import to complete

⏱ Import time: a few minutes

---
## Step 4 — First boot

1. Select the imported VM
2. You'll need to input a password for the TPM
	1. Paste `Lived$Unreal$Bootlace$Program$Skier9`
3. Click **Power On**
4. The user password is `findevil89!`
5. Wait for Windows to start

You should see:

* Windows 11 desktop
* Network connected
* No setup prompts

If Windows asks about:

* Network type → select **Private**
* Updates → skip for now

---
## Step 5 — Verify everything works (2 minutes)

Inside the VM:

* ⬜ Mouse and keyboard work
* ⬜ Internet access works (open a browser)
* ⬜ The VM is responsive

If this is true, **you’re done**.

---
## 🚨 Common issues & quick fixes

### “Download quota exceeded”

* Sign into any Google account
* Right-click the file → **Make a copy**
* Download the copy

---
### VM won’t start or is very slow

* Make sure **no other VMs** are running
* Close heavy apps (browsers, IDEs, games)
* Ensure virtualization is enabled in BIOS (rare, but possible)

---
### “This VM was created by a newer version”

* Click **Upgrade**
* Accept defaults

Safe and expected.
