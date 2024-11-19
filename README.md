

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop


<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)







# **Setup Domain Controller and Client in Azure Lab**

This tutorial guides you through the process of setting up a **Domain Controller** (DC-1) and a **Client VM** (Client-1) within **Azure**, and configuring basic network connectivity between them.

---

## **Part 1: Setup Domain Controller (DC-1)**

### **1.1 Create a Resource Group**

1. **Login to the Azure Portal**.
2. In the Azure portal, navigate to **Resource Groups** and click **Create**.
3. Choose a **Resource Group Name** (e.g., `Active-Directory-Lab`) and a **Region** (preferably `East US` or `West US`).
4. Click **Review + Create** and then **Create**.
![image](https://github.com/user-attachments/assets/038f83e5-358f-457c-aa0c-a242f3f04f7f)
![image](https://github.com/user-attachments/assets/7d6dbf11-92d3-4cd6-89f6-14df8b671437)
![image](https://github.com/user-attachments/assets/42f55108-cb14-488a-8593-b5faa6e375f3)



---

### **1.2 Create a Virtual Network and Subnet**

1. In the Azure portal, go to **Virtual Networks** and click **Create**.
2. Enter a **Name** for the Virtual Network (e.g., `Active-Directory-VNet`).
3. Choose the **Region** that matches your Resource Group (e.g., `East US`).
4. Under **Address space**, provide an address range such as `10.0.0.0/16`.
5. Under **Subnets**, create a **Subnet** named `Subnet-DC` with an address range of `10.0.0.0/24`.
6. Click **Review + Create** and then **Create**.
![image](https://github.com/user-attachments/assets/aabea289-8e96-43c9-a427-b345042f7970)
![image](https://github.com/user-attachments/assets/6d1d26ac-7725-4a08-a97f-63ac03c7bb0b)
![image](https://github.com/user-attachments/assets/42654450-a4a0-4784-b745-b0f8eea6c8be)
![image](https://github.com/user-attachments/assets/cbd6361b-4ca4-4661-8935-1777fa29a9e2)


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
   ![image](https://github.com/user-attachments/assets/e0390ff0-7a59-4676-b2ad-e798ae4eb035)
   ![image](https://github.com/user-attachments/assets/3c7a2aa6-502a-45eb-a31c-49b3229f1414)
   ![image](https://github.com/user-attachments/assets/6e45b0e8-cb50-4c1a-b729-8b0861c61589)
   ![image](https://github.com/user-attachments/assets/f6e01c9f-e3e1-4a1a-8951-1f9199761901)
   ![image](https://github.com/user-attachments/assets/08a5e634-ebb1-409f-8930-09910292a0dd)
   ![image](https://github.com/user-attachments/assets/83d06cf3-bcf0-4960-ad9d-6d7ae15940d2)
   ![image](https://github.com/user-attachments/assets/91733d4b-ab62-4921-97f4-f2dd6175f260)
   ![image](https://github.com/user-attachments/assets/d0a699e6-335e-497e-99f2-43020a669c2a)
   ![image](https://github.com/user-attachments/assets/abf00612-8aeb-4cf5-86d8-b50ff0ebba69)
   ![image](https://github.com/user-attachments/assets/b821b575-2c1e-40d9-80e6-8e228ce70fc9)





---

### **1.4 Configure Static IP for DC-1**

1. After the VM deployment completes, go to the **Networking** tab of **DC-1**.
2. Click the **NIC** (Network Interface) for **DC-1**.
3. Under **IP Configurations**, click **Private IP** and change the assignment to **Static**.
4. Save the changes.

   ![image](https://github.com/user-attachments/assets/7e6d6903-e628-4424-a0fb-330f5421fa27)
   ![image](https://github.com/user-attachments/assets/b64bd2ee-09a7-4a4e-b374-e180a58d870e)
   ![image](https://github.com/user-attachments/assets/98a8bb40-92c9-445e-9264-cad5c7424275)
   ![image](https://github.com/user-attachments/assets/73f5655b-c62b-4cf1-a8be-0dad94d45bec)
   ![image](https://github.com/user-attachments/assets/2245c58d-513f-41a0-bee8-2ea33c65bc07)
   ![image](https://github.com/user-attachments/assets/c6cce704-8b48-4cea-b1b8-1b935e2f86ed)






   
---

### **1.5 Log into DC-1 and Disable Windows Firewall**

1. In the Azure portal, navigate to **Virtual Machines** and select **DC-1**.
2. Click **Connect** and follow the instructions to log into **DC-1** using **labuser** and the password `Cyberlab123!`.
3. Once logged into the VM, open **Windows Firewall**:
   - Type `Windows Defender Firewall` in the start menu.
   - Click **Turn Windows Defender Firewall on or off**.
   - Select **Turn off Windows Defender Firewall** for both private and public networks.
4. Click **OK** to apply changes.

   ![image](https://github.com/user-attachments/assets/d6f5b88e-6d38-4081-8271-a933157cbb3d)
   ![image](https://github.com/user-attachments/assets/d9290830-799e-4e7b-9230-ba2265cbbf68)
   ![image](https://github.com/user-attachments/assets/d727fcad-239b-4c35-b272-fab275299eb9)
   ![image](https://github.com/user-attachments/assets/7a76f305-d7c9-430d-9502-428749ff2c30)
   ![image](https://github.com/user-attachments/assets/c8682690-c346-4709-84c1-32a27f71d825)
   ![image](https://github.com/user-attachments/assets/1c398f8b-e183-4148-aeae-72c924cce29b)
   ![image](https://github.com/user-attachments/assets/825cab9e-7afa-42a3-a7e6-d1b6712cf8cf)
   ![image](https://github.com/user-attachments/assets/7e928033-220a-43ab-94e5-7749d1b50356)
   ![image](https://github.com/user-attachments/assets/05042fa5-e93b-49b5-be27-a0e536a179ea)
   ![image](https://github.com/user-attachments/assets/8bc971b0-f76a-4333-ae14-c68f863ee7f2)
   ![image](https://github.com/user-attachments/assets/17366559-b2fb-4497-9aa1-10f547633cd8)
   ![image](https://github.com/user-attachments/assets/0e8ad15b-a5f2-440a-855e-d537b09887f6)













   

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
   ![image](https://github.com/user-attachments/assets/1d741714-7a21-4faa-913f-7ef2c7f02459)
   ![image](https://github.com/user-attachments/assets/1312b364-9a7e-48f6-98ac-9a6f709ff677)
   ![image](https://github.com/user-attachments/assets/8c606044-2e0a-4467-be71-cdcea1262891)
   ![image](https://github.com/user-attachments/assets/e631ea1e-2ce9-476e-9c8b-29f06599e1d7)
   ![image](https://github.com/user-attachments/assets/a1d26a90-1a26-4d93-89e4-2fd8ea112cb1)
   ![image](https://github.com/user-attachments/assets/3696dc97-f65d-4ea7-b2bf-12ad847611e1)
   ![image](https://github.com/user-attachments/assets/730c6571-b0ce-4728-972b-c7fbbfeb43d9)
   ![image](https://github.com/user-attachments/assets/6f2d34f5-0d9b-4ea0-893a-6d4731129627)
   ![image](https://github.com/user-attachments/assets/0be048cb-b55e-4485-9d72-1022a33ca7d0)









   

---

### **2.2 Set DNS for Client-1**

1. After **Client-1** is deployed, go to **Networking** and select the **NIC** for **Client-1**.
2. Under **IP Configurations**, click **DNS servers** and select **Custom**.
3. Set the **DNS server** to the **Private IP Address** of **DC-1** (the static IP configured in Step 1.4).
4. Save the changes.
![image](https://github.com/user-attachments/assets/72532707-2ac1-4562-b3cc-bc052a4a1c89)
![image](https://github.com/user-attachments/assets/6e00f018-bf85-444d-bedc-688b58da04a3)
![image](https://github.com/user-attachments/assets/596ee0a9-821d-4023-8d73-4f2190cf67d2)
![image](https://github.com/user-attachments/assets/2f0aa034-6eed-45e7-aea8-128056d1a6ac)
![image](https://github.com/user-attachments/assets/1ea305c4-c08c-4ffa-a7fa-50911c6e750a)
![image](https://github.com/user-attachments/assets/ada8576a-6ac8-46cd-b3a9-8e25fc555837)
![image](https://github.com/user-attachments/assets/97a3ead0-8d78-4b03-a2fd-e12c01361343)









---

### **2.3 Restart Client-1 VM**

1. Go to the **Overview** tab for **Client-1**.
2. Click **Restart** to apply the DNS changes.
   ![image](https://github.com/user-attachments/assets/59376d76-8207-4b96-869b-cb98af6cd551)
   ![image](https://github.com/user-attachments/assets/b17a9f62-dcdb-4bda-9660-50538028199b)



---

### **2.4 Test Network Connectivity from Client-1**

1. Log into **Client-1** using **labuser** and the password `Cyberlab123!`.
2. Open **Command Prompt** and run the following command to test the network connection to **DC-1**:
   ```powershell
   ping <DC-1_Private_IP_Address>
Ensure the ping command succeeds, confirming that the network connection between Client-1 and DC-1 is working.
![image](https://github.com/user-attachments/assets/1e94a3ac-f71f-463a-92f4-6ad8184fd396)
![image](https://github.com/user-attachments/assets/37bb75f2-c1df-4f30-bc86-2602fddbe662)
![image](https://github.com/user-attachments/assets/0415d313-1098-4cbe-b0aa-3d4424d39467)
![image](https://github.com/user-attachments/assets/b93ac03c-3ff9-47e2-94d9-6de3637858f2)





---

### **2.5 Verify DNS Settings on Client-1**

1. Open PowerShell on Client-1.
2. Run the following command to verify the DNS settings:
  ipconfig /all
3. The DNS Servers section should display the Private IP Address of DC-1.

---

### **Part 3: Finalizing the Lab**

3.1 Stop VMs to Save Resources

1. After completing the lab, you may choose to stop the VMs to save resources.

2. Go to the Azure Portal.

3. Under Virtual Machines, select both DC-1 and Client-1.

4. Click Stop to shut down the VMs.

Note: Do not delete the VMs as you will use them in upcoming labs.

___


### **Conclusion**

In this tutorial, you have:
Created a Resource Group, Virtual Network, and Subnet.

Deployed a Domain Controller VM (DC-1) with Windows Server 2022 and set it up with a static IP address.

Created a Client VM (Client-1) with Windows 10 and configured it to use DC-1 as its DNS server.

Tested connectivity between Client-1 and DC-1 using ping and verified DNS settings.

This setup prepares the environment for further Active Directory configurations and domain management tasks in subsequent labs.


----


### Key Features:
- **Step-by-step instructions** for creating Azure resources like Virtual Machines, Resource Groups, Virtual Networks, and configuring DNS.
- **Commands and PowerShell scripts** are included to test the connectivity and verify settings.
- **Instructions for stopping the VMs** to save costs while preserving the environment for future labs.





