#  Multi-Honeypot-Platform
                   
# Deploying T-Pot on Azure Virtual Machine to Monitor Honeypot Data

A honeypot is a sophisticated cybersecurity technique that involves deploying a decoy system deliberately designed to appear vulnerable and/or valuable to malicious actors. This strategy allows security analysts to monitor and study the behaviour of attackers. In this blog, I will demonstrate the deployment of T-Pot on an Azure Virtual Machine to monitor and analyze honeypot data, enabling the detection of potential cyber threats.

## What is T-Pot?

T-Pot is an open-source honeypot platform that emulates a variety of services and systems to attract and gather intelligence on attackers and their techniques. It is meticulously designed to mimic real-world systems and services, thereby presenting itself as a legitimate and enticing target for attackers. This facilitates the collection of valuable data on attack methodologies, which is critical for enhancing cybersecurity defenses.

## Creating our Honeypot VM

To deploy T-Pot on an Azure Virtual Machine, follow these steps:

### Access the Azure Portal

Log in to the Azure Portal.

### Create a Virtual Machine

1. Click on the "Create a resource" button, then select "Virtual Machine".

### Configure Basic Settings

1. **Name your virtual machine**: For example, "MYHPMAchines".
2. **Select or create a Resource Group**: For instance, "New_virtual".
3. **Choose your Region**: Select the region closest to you or your organization's operations, such as "West Europe".

### Select the Image

1. Under the Image section, click on "See all images" and search for "Debian 11 'Bullseye' - x64 Gen2".
2. Select this image to use it for your virtual machine.

### Choose the Size

In the Size section, select `D4s_v3`. This size offers a good balance of CPU, memory, and cost, which is suitable for running T-Pot.

<div style="text-align:center;">
  <img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture1.png?raw=true" alt="img">
</div>

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture2.png?raw=true" alt="img">
</div>

### Configure Administrator Account

- Fill in the **Username** for your VM. For example, `azureuser`.
- Choose **SSH public key** as the authentication type for secure access.
- Provide a name for the **Key pair**. For example, `MY_HPMAchines_key`.

<div style="text-align:center;">
  <img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture3.png?raw=true" alt="img">
</div>

### Configure Disk

Navigate to the **Disks** section.

- Click on **"Create and attach a new disk"**.
- Click on **"Create and attach a new disk"** again.

#### Set Disk Size

- In the **Name** field, you can use a name like `MYHPMAchines`.
- Change the **Size (GiB)** to `128` to meet the system requirements for T-Pot.
<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture4.png?raw=true" alt="img">
</div>

### Create the Virtual Machine

- After reviewing all our configurations, click on **Create** to start the VM deployment process.

### Download the Private Key

- As part of the VM creation process, Azure will prompt you to download the private key for SSH authentication.
- Download the private key file (typically named something like `TPotKeyPair.pem`) to a secure location on your local machine.

### Connect to the VM

- Once the VM is successfully deployed, you can connect to it using SSH.
<div style="text-align:center;">
  <img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture6.png?raw=true" alt="img" >
</div>

### Configure Networking Settings for T-Pot

To configure the networking settings for our Azure Virtual Machine to support the T-Pot honeypot, follow these steps:

#### Navigate to Networking Settings

- Go to the Azure Portal.
- Find and select your virtual machine.
- In the left-hand menu, click on **Networking** under the **Settings** section.

#### Add an Inbound Port Rule

- In the **Networking** section, click on **Add inbound port rule**.

#### Configure Inbound Port Rule

- Change the **Destination port ranges** value to `0-65535`.
- Set **Protocol** to `Any`.
- Optionally, you can provide a name for this rule, such as `AllowAllPortsForTPot`.
- Ensure the **Action** is set to `Allow`.

#### Add the Rule

- Click on **Add** to create the rule.

By adding this inbound port rule, you are allowing all ports from `0 to 65535`, ensuring that your VM will be accessible on every port that T-Pot requires for its various honeypot services.
<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture7.png?raw=true" alt="img">
</div>

### Download and Install PuTTY

- Visit the [PuTTY download page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
- Download the Windows installer package (e.g., `putty-<version>-installer.msi`) and run it to install PuTTY.

### Convert the Private Key Using PuTTYgen

- Open **PuTTYgen**, which is included in the PuTTY installation.
- Click on **Load** and navigate to the location where you saved your private key file (e.g., `TPotKeyPair.pem`).
- In the file dialog, change the file type filter to **All Files (*.*)** to see your `.pem` file.
- Select your `.pem` file and click **Open**.
- Once the key is loaded, click on **Save private key**. You can choose to save without a passphrase or set one for additional security.
- Save the file with a `.ppk` extension, which is the format PuTTY uses (e.g., `TPotKeyPair.ppk`).

### Open PuTTY and Configure the Connection

- Open **PuTTY**.
- In the **Host Name (or IP address)** field, enter the public IP address of your VM.
- Ensure the **Port** is set to `22` and the **Connection type** is `SSH`.

### Load the Private Key in PuTTY

- In the left-hand menu, under **Connection**, expand **SSH** and select **Auth**.
- Click on **Browse** and select the `.ppk` file you saved earlier (e.g., `TPotKeyPair.ppk`).

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture8.png?raw=true" alt="img">
</div>

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture9.png?raw=true" alt="img">
</div>

### Open PuTTY and Configure the Connection

- Open **PuTTY**.
- In the **Host Name (or IP address)** field, enter the public IP address of your VM.
- Ensure the **Port** is set to `22` and the **Connection type** is `SSH`.

#### Load the Private Key in PuTTY

- In the left-hand menu, under **Connection**, expand **SSH** and select **Auth**.
- Click on **Browse** and select the `.ppk` file you saved earlier (e.g., `TPotKeyPair.ppk`).

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture10.png?raw=true" alt="img">
</div>

### Load the Private Key in PuTTY

- In the left-hand menu, under **Connection**, expand **SSH** and select **Auth**.
- Click on **Browse** and select the `.ppk` file you saved earlier (e.g., `TPotKeyPair.ppk`).

### Save the Session Configuration (optional)

- Go back to the **Session** category at the top of the left-hand menu.
- Enter a name for the session in the **Saved Sessions** field (e.g., `TPotVM`).
- Click **Save** to save these settings for future use.

### Connect to the VM

- Click **Open** to start the SSH session.
- A security alert may appear the first time you connect; click **Yes** to trust the host.
- When prompted, enter the username you specified when creating the VM.

By following these steps, you will successfully connect to your Azure VM using PuTTY, allowing you to proceed with configuring T-Pot on your virtual machine.

### Login with your Username for the VM
<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture11.png?raw=true" alt="img">
</div>

### Install T-Pot on Your Azure Virtual Machine

After connecting to your VM using PuTTY, follow these steps:

#### Update and Upgrade the System

Run the following commands to update the package list and upgrade all installed packages:
```bash
sudo apt update
sudo apt upgrade -y
```
#### Install Git
Install Git using the following command:
```bash
sudo apt install git
```

#### Clone the T-Pot Repository
Clone the T-Pot repository from GitHub:
```bash
sudo git clone https://github.com/telekom-security/tpotce
```
#### Navigate to the Installer Directory
Change directory to the T-Pot installer location:
```bash
cd tpotce/iso/installer/
```

#### Run the Installer
Start the installation process with the following command:
```bash
sudo ./install.sh --type=user
```

After the install, select the ‘STANDARD’ T-pot edition and provide your username and create a password.
<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture12.png?raw=true" alt="img">
</div>

### Exploring the T-Pot Web Interface

You can open the T-Pot Landing Page from your browser via `https://<your VM's public IP address>:64297`.

- You will get a warning from your browser, click on **advanced** and **proceed unsafe**.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture13.png?raw=true" alt="img">
</div>

### Explore the T-Pot Interface

- After logging in, you will be greeted with the T-Pot dashboard.
- Here, we can access various features and tools for monitoring and analyzing honeypot data.
- Use the interface to view attack patterns, analyze traffic, and gain insights into potential cyber threats.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture14.png?raw=true" alt="img">
</div>

### Attack Map

The 'Attack Map' provides real-time visualization of attempted intrusions onto a virtual machine (VM), displaying geolocations, IP addresses, hit frequencies, and targeted ports utilized by potential attackers. The screenshot captured herein was obtained mere minutes after deploying the honeypot, showcasing the immediate interest and activity directed towards the system.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture15.png?raw=true" alt="img">
</div>

### SpiderFoot

SpiderFoot is a comprehensive reconnaissance and data-gathering tool designed for extracting additional insights about attackers engaging with the honeypot. By querying diverse sources, SpiderFoot unveils valuable information regarding the attacker's infrastructure, potential vulnerabilities, and potential associations with known malicious activities.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture16.png?raw=true" alt="img">
</div>

### Target Scans with SpiderFoot

With SpiderFoot, we can run scans on targets, such as the IP address of an attacker, to gather a wide range of various open-source information. It automatically collects data about IP addresses, domain names, email addresses, and other attributes associated with attackers. This enables us to gather valuable insights and intelligence about potential threats and their infrastructure.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture17.png?raw=true" alt="img">
</div>

### Kibana
Kibana stands as an open-source data visualization and exploration platform, adept at dissecting data through tailored visualizations, dashboards, and charts. With its capabilities, it enables the parsing of intricate information, empowering users to discern patterns, trends, and anomalies within the acquired dataset. Offering a diverse array of dashboards, Kibana facilitates efficient data analysis across a spectrum of contexts and domains

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture18.png?raw=true" alt="img">
</div>

### T-Pot Dashboard in Kibana

'T-Pot' is one of the dashboards available in Kibana. Cowrie, a component of our honeypot, emulates an SSH and Telnet server, presenting itself as a legitimate system for attackers to target. As attackers interact with Cowrie, it meticulously logs their activities, commands, and behavior. This recording captures the techniques and tools utilized by the attackers, providing valuable insights into their tactics and methodologies.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture19.png?raw=true" alt="img">
</div>

### Brute-Force Attempts Visualization

In Kibana, we can observe the usernames and passwords employed by attackers during brute-force attempts. The frequency of each specific term is visually represented, with the text size increasing proportionally to the number of occurrences. This visualization provides valuable insights into the common usernames and passwords used by attackers, aiding in the identification of potential security weaknesses and the implementation of stronger authentication measures.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture20.png?raw=true" alt="img">
</div>

### Attack Monitoring with Kibana

With Kibana, we can monitor various aspects of attacks, including:

- **Operating Systems:** We can track the operating systems used by attackers.
- **IP Reputation:** We can assess the reputation of attacker IP addresses.
- **Geolocation:** We can determine the countries of origin of attackers.
- **Honeypot Component Attacks:** We can analyze attacks originating from various honeypot components.

This comprehensive monitoring allows us to gain insights into the types of attackers targeting our system, their origins, and the techniques they employ, enabling us to enhance our security measures effectively.

<div style="text-align:center;">
<img src="https://github.com/Walikhan7866/Multi-Honeypot-Platform/blob/my-new-branch/screenshot/Picture21.png?raw=true" alt="img">
</div>

### Conclusion

Hosting a honeypot provides invaluable insights into the behavior of attackers. By mimicking vulnerable systems, honeypots allow us to gain an understanding of the methods and tactics employed by potential attackers. They also serve as early warning systems; when an attacker engages with a honeypot, it indicates their presence before they reach critical production systems. This provides security analysts with valuable time to respond and mitigate potential damage.

It's important to note that honeypots require careful planning and management. Improperly deployed honeypots could potentially attract malicious actors to your network. Therefore, organizations should consider their goals, resources, and expertise before implementing honeypots as part of their cybersecurity strategy.


