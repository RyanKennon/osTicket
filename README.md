<p align="center">
  <img width="500" height="320" alt="image" src="Images/Header.png" />
</p>

# osTicket: Deployment & Service Desk Workflow

This project demonstrates the complete deployment, configuration, and operational workflow of the osTicket ticketing system within a Windows 10 virtualized environment hosted in Microsoft Azure. The lab begins with configuring the full web stack—installing and enabling Internet Information Services (IIS), registering PHP, enabling required extensions, configuring MySQL, and preparing the file system for secure operation. After successfully deploying the application, the lab transitions into realistic IT service desk operations, including configuring roles, departments, teams, SLAs, help topics, agents, and end-users.

The final portion of the lab focuses on the full ticket lifecycle, simulating real-world IT support scenarios. You create tickets, triage them based on severity, assign them to appropriate agents and departments, adjust priorities and SLAs, and work them through resolution. This end-to-end lab mirrors enterprise help desk operations and showcases technical skills in system deployment, web server configuration, database management, IT service workflows, and structured ticket handling used across IT Support, Help Desk, and Service Desk Analyst roles.

---

## Environments and Technologies Used

- Microsoft Azure
- Windows 10 Pro Virtual Machine
- Internet Information Services (IIS)
- PHP Ecosystem
- HeidiSQL
- osTicket Application
- IT Service Management Concepts

---

## Table of Contents

- [1)	Create Virtual Machine](#1-create-virtual-machine)
- [2)	Enable Internet Information Services (IIS)](#2-enable-internet-information-services-iis)
- [3)	Download osTicket Dependencies](#3-download-osticket-dependencies)
- [4)	Configure Internet Information Services (IIS) and Register PHP](#4-configure-internet-information-services-iis-and-register-php)
- [5)	Install osTicket](#5-install-osticket)
- [6)	Enable PHP Extension](#6-enable-php-extensions)
- [7)	Grant osTicket Permissions](#7-grant-osticket-permissions)
- [8)	Install HeidiSQL](#8-install-heidisql)
- [9)	Setup osTicket in Browser](#9-setup-osticket-in-browser)
- [10) Verify Installation Success](#10-verify-installation-success)
- [11) Configure Roles, Departments, and Teams](#11-configure-roles-departments-and-teams)
- [12) Create Agents](#12-create-agents)
- [13) Create a User](#13-create-a-user)
- [14) Configure SLAs and Help Topics](#14-configure-slas-and-help-topics)
- [15) Create Help Tickets](#15-create-help-tickets)
- [16) Triage Tickets](#16-triage-tickets)
- [17) Work Ticket to Completion](#17-work-ticket-to-completion)

---

### 1) Create Virtual Machine

1. Search Virtual Machines then create give the Virtual Machine the following settings then create the Virtual Machine
  - **Basics**
    - **Resource Group:** osTicket-vm_group
    - **Name:** osTicket-vm
    - **Image:** Windows 10 Pro
    - **Size:** 2 vCPUs
    - **Region:** South Central US
    - **Username:** userryan
    - **Password:** *your password*

<p align="center">
  <img width="600" alt="Azure VM settings" src="Images/Image%201.png" />
</p>

---

### 2) Enable Internet Information Services (IIS)

1. In the Virtual Machine open the computers **Control Panel** and select **Programs**
2. Select **Turn windows features on or off**
3. Check the box labeled **Internet Information Services**
4. Navigate through **Internet Information Services** to **CGI** and check the box then complete installation

<p align="center">
  <img width="413" height="422" src="Images/Image%202.PNG" />
</p>

---

### 3) Download osTicket Dependencies

1. Download and extract [osTicket Dependencies file](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD) on the Virtual Machine
2. Install the **PHP Manager** and the **Rewrite Module** from the **osTicket Dependencies file**
3. On the **`C: \`** create a folder named **PHP**
4. In the **osTicket Dependencies** folder extract the file named **php** to the **PHP folder on the `C: \`**
5. Install **VC_redist** and **mysql** when asked choose **Typical Setup**
6. Launch the **MySQL configuration wizard** and choose **Standard Configuration** when asked
7. Create a **root password** and complete the wizard

<p align="center">
  <img width="1079" height="697" alt="Untitled Diagram-Page-12 drawio" src="Images/Image%202.5.PNG" />
</p>

---

### 4) Configure Internet Information Services (IIS) and Register PHP

1. In the **Start Menu** search **Internet Information Services (IIS)** and open as an admin

<p align="center">
  <img width="1079" height="697" alt="Untitled Diagram-Page-12 drawio" src="Images/Image%203.PNG" />
</p>

2. Open **PHP Manager**
3. Select **Register new PHP version**

<p align="center">
  <img width="1079" height="697" alt="Untitled Diagram-Page-12 drawio" src="Images/Image%204.PNG" />
</p>

4. Select **PHP executable** on the **`C:\`**
5. **Stop** and **start** the server

<p align="center">
  <img width="1056" height="607" alt="Untitled Diagram-Page-16 drawio" src="Images/Image%205.PNG" />
</p>

---

### 5) Install osTicket

1. In the **osTicket Installation Files** folder extract the contents of the **osTicket** folder
2. Copy the upload folder to **`c:\inetpub\wwwroot`** and rename the folder **osTicket**

<p align="center">
  <img width="877" height="460" alt="Untitled Diagram-Page-18 drawio" src="Images/Image%206.PNG" />
</p>

3. Stop and start the server in IIS

---

### 6) Enable PHP Extensions

1. Navigate to the **osTicket** folder in IIS
2. Select **Browse 80** and the **osTicket site** should pull up in the web browser

<p align="center">
  <img width="1050" height="591" alt="Untitled Diagram-Page-20 drawio" src="Images/Image%207.PNG" />

  <img width="1050" height="591" alt="Untitled Diagram-Page-20 drawio" src="Images/Image%207.5.PNG" />
</p>

3. In **IIS** navigate to the **osTicket** folder select **PHP Manager**
4. Click **enable or disable an extension**
5. Find these three extensions:
   - **php_imap**
   - **php_intl**
   - **php_opcache**
6. Right click and **enable them**

<p align="center">
  <img width="643" height="612" alt="Untitled Diagram-Page-24 drawio" src="Images/Image%208.PNG" />
</p>

7. **Stop** and **Start** the server in the **IIS**
8. **Refresh** the **osTicket** page in the browser and observe changes

<p align="center">
  <img width="643" height="612" alt="Untitled Diagram-Page-24 drawio" src="Images/Image%208.5.PNG" />
</p>

---

### 7) Grant osTicket Permissions

1. Navigate to **`c:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`**
2. Rename the file to **`c:\inetpub\wwwroot\osTicket\include\ost-config.php`**
3. For the **`ost-config.php`** file right click and open **Properties**

<p align="center">
  <img width="1111" height="662" alt="Untitled Diagram-Page-28 drawio" src="Images/Image%209.5.PNG" />
</p>

4. Select **Security** then click **Advanced**
5. **Disable Inheritance**

<p align="center">
  <img width="1111" height="662" alt="Untitled Diagram-Page-28 drawio" src="Images/Image%209.PNG" />
</p>

6. Select **Add** then **Select a Principal**
7. Enter **Everyone** and select **Check Names**
8. Check the box labeled **Full Control** and apply the changes

<p align="center">
  <img width="911" height="588" alt="Untitled Diagram-Page-29 drawio" src="Images/Image%2010.PNG" />
</p>

---

### 8) Install HeidiSQL

1. In the **osTicket Installation Files** folder install and launch **HeidiSQL**
2. Select **New** then enter the information for the **root user** then click **open**

<p align="center">
  <img width="683" height="480" alt="Untitled Diagram-Page-31 drawio" src="Images/Image%2011.PNG" />
</p>

3. Right click **unnamed** and create a new database name **osTicket**

<p align="center">
  <img width="930" height="587" alt="Untitled Diagram-Page-32 drawio" src="Images/Image%2012.PNG" />
</p>

---

### 9) Setup osTicket in Browser

1. Go back to **osTicket** in the browser and select **continue**
2. Fill out the helpdesk information and when you get to the **Database Settings** enter the following information:
   - **MySQL Database:** osTicket
   - **MySQL Username and Password:** enter the root user information
3. Complete the Installation

<p align="center">
  <img width="562" height="371" alt="Untitled Diagram-Page-33 drawio" src="Images/Image%2013.PNG" />
</p>

---

### 10) Verify Installation Success

1. Go to the osTicket helpdesk login page: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
2. Log in to the helpdesk

<p align="center">
  <img width="975" height="389" alt="Untitled Diagram-Page-34 drawio" src="Images/Image%2014.PNG" />
</p>

---

### 11) Configure Roles, Departments, and Teams

1. Open **osTicket** as an admin in the **Virtual Machine**
   - [Admin/Analyst Login Page](http://localhost/osTicket/scp/login.php)

<p align="center">
  <img width="826" height="619" alt="Capture1" src="Images/Image%2014.5.PNG" />
</p>

2. In the **admin** account open the **Admin Panel**
3. Select the **Agents** tab then select **Roles** then **Add New Role**
4. Create a **Supreme Admin** and grant all **Permissions** and create role

<p align="center">
  <img width="984" height="566" alt="Untitled Diagram-Page-2 drawio" src="Images/Image%2015.PNG" />
</p>

5. Select **Departments** then **Add New Department**
6. Create a **SysAdmins** department and make it a **Top Level Department**
7. Delete the **Maintenance** department

<p align="center">
  <img width="973" height="487" alt="Untitled Diagram-Page-3 drawio" src="Images/Image%2016.PNG" />
</p>

8. Select **Teams** then **Add New Team**
9. Create an **Online Banking** team

<p align="center">
  <img width="977" height="447" alt="Untitled Diagram-Page-4 drawio" src="Images/Image%2017.PNG" />
</p>

---

### 12) Create Agents

1. Select **Settings** then **Users** and uncheck the box labeled **Require registration and login to create tickets**

<p align="center">
  <img width="976" height="793" alt="Untitled Diagram-Page-5 drawio" src="Images/Image%2018.PNG" />
</p>

2. Open the **Agents** tab then **Agents** then **Add New Agent**
3. Create two Agents: named **Jane** and **John**
   - **Jane**
       - **Role:** Supreme Admin
       - **Department:** SysAdmins
       - **Team:** Online Banking

    - **John**
        - **Role:** All Access
        - **Department:** Support
        - **Team:** Leave Blank
     
<p align="center">
  <img width="980" height="516" alt="Untitled Diagram-Page-6 drawio" src="Images/Image%2019.PNG" />
</p>

---

### 13) Create a User

1. Select the **Agent Panel** then select **Users** then **Add User**
2. Name the user **Karen** and fill out necessary information

<p align="center">
  <img width="976" height="462" alt="Untitled Diagram-Page-7 drawio" src="Images/Image%2020.PNG" />
</p>

---

### 14) Configure SLAs and Help Topics

1. Go back to the **Admin Panel** select **Manage** then **SLA**
2. **Add New SLA Plan** and create 3 SLAs:
   - **Sev-A**
     - **Grace Period:** 1 hour
     - **Schedule:** 24/7

    - **Sev-B**
      - **Grace Period:** 4 hours
      - **Schedule:** 24/7
     
    - **Sev-C**
      - **Grace Period:** 8 hours
      - **Schedule:** 24/5
     
<p align="center">
  <img width="975" height="535" alt="Untitled Diagram-Page-8 drawio" src="Images/Image%2021.PNG" />
</p>

3. Select **Help Topics** and **Add New Help Topic**
4. Create 5 Help Topics
   - **Business Critical Outage**
     - **Parent Topic:** Report a Problem
    
   - **Personal Computer Issues**
     - **Parent Topic:** Report a Problem
    
   - **Equipment Request**
     - **Parent Topic:** General Inquiry
    
   - **Password Reset**
     - **Parent Topic:** Report a Problem
    
   - **Other**
     - **Parent Topic:** General Inquiry
    
<p align="center">
  <img width="975" height="758" alt="Untitled Diagram-Page-9 drawio" src="Images/Image%2022.PNG" />
</p>

---

### 15) Create Help Tickets

1. [Log in as an end user](http://localhost/osTicket) and create a ticket with the following information:
  - Ticket 1
    - **Help Topic:** General Inquiry / Other
    - **Issue Summary:** entire mobile/online banking system is down
    - **Issue Description:** When I got back from lunch, I couldn't log into the online banking system portal, and none of my tellers at the bank can either.
  
<p align="center">
  <img width="848" height="907" alt="Untitled Diagram-Page-1 drawio" src="Images/Image%2023.PNG" />
</p>

2. Create a second ticket with the following information:
  - Ticket 2
    - **Help Topic:** Report a Problem / Personal Computer Issues
    - **Issue Summary:** Adobe Reader not working
    - **Issue Description:** Some people in the accounting department can't use adobe reader

<p align="center">
  <img width="847" height="886" alt="Untitled Diagram-Page-2 drawio" src="Images/Image%2024.PNG" />
</p>

---

### 16) Triage Tickets

1. [Log into the agent portal](http://localhost/osTicket/scp/login.php) as **John**

<p align="center">
  <img width="966" height="418" alt="Untitled Diagram-Page-3 drawio" src="Images/Image%2024.5.PNG" />
</p>

2. Observe the **Adobe Reader not working** ticket
3. Make the following changes:
  - **Priority:** High
  - **Department:** Support
  - **SLA:** Sev-B
  - **Assigned To:** John

<p align="center">
  <img width="970" height="321" alt="Untitled Diagram-Page-4 drawio" src="Images/Image%2025.png" />
</p>

4. Next to **Status** select **Open** then select **Closed** then **Close** ticket
5. Open the **Tickets** tab then select **Closed** to confirm the ticket has been closed

<p align="center">
  <img width="970" height="252" alt="Untitled Diagram-Page-5 drawio" src="Images/Image%2026.PNG" />
</p>

6. Select **Open** then observe the **entire mobile/online banking system is down** ticket
7. Make the following changes:
  - **Priority:** Emergency
  - **SLA:** Sev-A
  - **Help Topic:** Business Critical Outage
  - **Assigned To:** Jane

<p align="center">
  <img width="965" height="308" alt="Untitled Diagram-Page-6 drawio" src="Images/Image%2027.png" />
</p>

8. Scroll down to the **Post Reply** section and enter the response: Business critical outage, escalating ticket
9. Select **Post Reply**

<p align="center">
  <img width="965" height="308" alt="Untitled Diagram-Page-6 drawio" src="Images/Image%2027.5.PNG" />
</p>

---

### 17) Work Ticket to Completion

1. Log into the agent portal as **Jane**

<p align="center">
  <img width="975" height="681" alt="Untitled Diagram-Page-7 drawio" src="Images/Image%2028.PNG" />
</p>

2. Observe the **entire mobile/online banking system is down** ticket
3. Post reply to the ticket that says: System restored, closing ticket then **Post Reply**

<p align="center">
  <img width="975" height="681" alt="Untitled Diagram-Page-7 drawio" src="Images/Image%2029.PNG" />
</p>

4. Next to **Status** select **Open** then select **Closed** then **Close** ticket
