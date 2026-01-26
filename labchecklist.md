## ✅ Setup Checklist

Before the workshop, make sure you have:

* [ ] A **Windows (Windows 10 or 11)** or **Mac M-series (M1-4)** laptop
* [ ] At least **12 GB RAM** (8 GB minimum, but 12-16 strongly recommended)
* [ ] At least **80 GB free disk space** (120 GB recommended)
* [ ] A stable internet connection

---
## Step 1 - Install VMware

### Windows
Download from [TechSpot](https://www.techspot.com/downloads/189-vmware-workstation-for-windows.html):
* VMware Workstation Pro 17.6.3
### Mac
Download from [TechSpot](https://www.techspot.com/downloads/2755-vmware-fusion-mac.html):
- VMware Fusion Pro 13.6.3

>You can download directly from VMware, now Broadcom, but you'll need to make an account.

During install:
* Accept defaults
* Reboot if prompted

No license key required for this workshop.

---
## Step 2 - Download the lab image

Download the .tar and SHA256 checksum for your image from the Mega link provided by the organizers:

```
dfth-workshop
> dfth-workshop-x64.tar
> dfth-workshop-x64-sha256.txt
> dfth-workshop-arm64.tar.gz
> dfth-workshop-arm64-sha256.txt
```

>Windows users should select the x64 files, while Mac M-series users should use the arm64 ones.
>Intel Mac users *may* be able to run the x64 VM. Windows Snapdragon users *may* be able to run arm64.

⚠️ **Important**
* Download the contents **fully** before importing.

Expected size: ~30 GB

---
## (Optional but recommended) Step 2.5 - Verify the download

If you want to confirm the file downloaded correctly, run the following in your terminal:
### Windows
```powershell
Get-FileHash dfth-workshop-x64.tar -Algorithm SHA256
```
### Mac
```bash
shasum -a 256 dfth-workshop-arm64.tar.gz
```

Compare the output to the checksum in the respective .txt file.

If it matches, your download is intact.

---
## Step 3 - Import the virtual machine

1. Extract the contents of the tar file.
	1. Mac users should run `tar -xzf dfth-workshop-arm64.tar.gz` instead of using the Extract utility.
2. Open **VMware**.
3. Click `File → Open...`
4. Double-click the folder and select the file that appears.
5. You'll need to input a password for the TPM:
```
Lived$Unreal$Bootlace$Program$Skier9
```
7. Choose "I copied it" if prompted.
8. If a SATA warning comes up, click No.
9. Wait for import to complete

⏱ Import time: a few minutes

---
## Step 4 - First boot

1. Select the imported VM.
2. Input the TPM password from above if prompted.
3. Click **Power On**.
4. Wait for Windows to start.
5. The user is `dfthrunter` and the password is `findevil89!`
6. If prompted, opt out of backup.

You should see:
* Windows 11 desktop
* Network connected

If Windows asks about:
* Updates → skip for now

---
## Step 5 - Networking Fix
1. Open up `C:\Elastic\kibana-9.2.4\config\kibana.yml`.
2. At the bottom of the file, after where it says `# This section was automatically generated during setup.`, leave `elasticsearch.serviceAccountToken` as is, replace everything else such that it looks like this:
```yaml
elasticsearch.hosts: ["https://localhost:9200"]
elasticsearch.ssl.verificationMode: none
elasticsearch.serviceAccountToken: <your actual token value>
```
3. Save the file and restart the VM.

---
## Step 5 - Verify everything works

Inside the VM:
* [ ] Mouse and keyboard work
* [ ] Internet access works (open a browser)
* [ ] Wait up to 10-15min, `http://localhost:5601` should load an Elastic login window
	- Username: `elastic`, Password:  
#### x64
```
61*FE8bjC2hrgcE2YtfG
```
#### arm64
```
*_nFAP+ynp6yf=S+VKeP
```

If you can login to Elastic/Kibana successfully, you're done!

---
## 🚨 Common issues & quick fixes

### VM won’t start or is very slow

* Make sure **no other VMs** are running
* Close heavy apps (browsers, IDEs, games)
* Ensure virtualization is enabled in BIOS (rare, but possible)
* If you could only allocate 8 GB RAM for the VM, run `setx ES_JAVA_OPTS "-Xms1g -Xmx1g"` in the VM terminal

---
### “This VM was created by a newer version”

* Click **Upgrade**
* Accept defaults

Safe and expected.

---
### `localhost:5601` won't load

* Make sure you use `http://` not https
* Inspect the bottom of `C:\Elastic\kibana-9.2.4\logs\kibana.log`
* If you just see `[root] Kibana is starting` and one or two more lines, it's still loading
* Once you see `[INFO ][http.server.Kibana] http server running at http://localhost:5601` the app should be available (not `[http.server.Preboot]`)

---
### Kibana Error 503

* All good, just refresh
