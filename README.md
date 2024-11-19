# **Setup Domain Controller and Client in Azure Lab**

This tutorial guides you through the process of setting up a **Domain Controller** (DC-1) and a **Client VM** (Client-1) within **Azure**, and configuring basic network connectivity between them.

---

## **Part 1: Setup Domain Controller (DC-1)**

### **1.1 Create a Resource Group**

1. **Login to the Azure Portal**.
2. In the Azure portal, navigate to **Resource Groups** and click **Create**.
3. Choose a **Resource Group Name** (e.g., `DomainLabRG`) and a **Region** (preferably `East US` or `West US`).
4. Click **Review + Create** and then **Create**.

---

### **1.2 Create a Virtual Network and Subnet**

1. In the Azure portal, go to **Virtual Networks** and click **Create**.
2. Enter a **Name** for the Virtual Network (e.g., `DomainLabVNet`).
3. Choose the **Region** that matches your Resource Group (e.g., `East US`).
4. Under **Address space**, provide an address range such as `10.0.0.0/16`.
5. Under **Subnets**, create a **Subnet** named `Subnet-DC` with an address range of `10.0.0.0/24`.
6. Click **Review + Create** and then **Create**.

---

### **1.3 Create the Domain Controller VM (DC-1)**

1. In the Azure portal, navigate to **Virtual Machines** and click **Create**.
2. Choose **Windows Server 2022** as the OS image.
3. Under **VM Name**, enter `DC-1`.
4. Select the **Region** (must match the Resource Group and Virtual Network region).
5. For **Authentication Type**, choose **Password** and enter:
   - **Username**: `labuser`
   - **Password**: `Cyberlab123!`
6. Under **Networking**, ensure that the VM is attached to the **DomainLabVNet** and **Subnet-DC**.
7. Click **Review + Create** and then **Create** to deploy the VM.

---

### **1.4 Configure Static IP for DC-1**

1. After the VM deployment completes, go to the **Networking** tab of **DC-1**.
2. Click the **NIC** (Network Interface) for **DC-1**.
3. Under **IP Configurations**, click **Private IP** and change the assignment to **Static**.
4. Save the changes.

---

### **1.5 Log into DC-1 and Disable Windows Firewall**

1. In the Azure portal, navigate to **Virtual Machines** and select **DC-1**.
2. Click **Connect** and follow the instructions to log into **DC-1** using **labuser** and the password `Cyberlab123!`.
3. Once logged into the VM, open **Windows Firewall**:
   - Type `Windows Defender Firewall` in the start menu.
   - Click **Turn Windows Defender Firewall on or off**.
   - Select **Turn off Windows Defender Firewall** for both private and public networks.
4. Click **OK** to apply changes.

---

## **Part 2: Setup Client-1 VM**

### **2.1 Create the Client VM (Client-1)**

1. In the Azure portal, navigate to **Virtual Machines** and click **Create**.
2. Choose **Windows 10** as the OS image.
3. Under **VM Name**, enter `Client-1`.
4. Select the **Region** (should match the region of `DC-1`).
5. For **Authentication Type**, choose **Password** and enter:
   - **Username**: `labuser`
   - **Password**: `Cyberlab123!`
6. Under **Networking**, ensure that the VM is attached to the **DomainLabVNet** and the same subnet as **DC-1**.
7. Click **Review + Create** and then **Create** to deploy the VM.

---

### **2.2 Set DNS for Client-1**

1. After **Client-1** is deployed, go to **Networking** and select the **NIC** for **Client-1**.
2. Under **IP Configurations**, click **DNS servers** and select **Custom**.
3. Set the **DNS server** to the **Private IP Address** of **DC-1** (the static IP configured in Step 1.4).
4. Save the changes.

---

### **2.3 Restart Client-1 VM**

1. Go to the **Overview** tab for **Client-1**.
2. Click **Restart** to apply the DNS changes.

---

### **2.4 Test Network Connectivity from Client-1**

1. Log into **Client-1** using **labuser** and the password `Cyberlab123!`.
2. Open **Command Prompt** and run the following command to test the network connection to **DC-1**:
   ```powershell
   ping <DC-1_Private_IP_Address>
Ensure the ping command succeeds, confirming that the network connection between Client-1 and DC-1 is working.
