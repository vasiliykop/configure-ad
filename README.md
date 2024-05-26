
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1> Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

<h2>Configuring AD
</h2>
<p>
<img src="https://github.com/vasiliykop/configure-ad/assets/170582503/a190cb6d-a9d2-48d3-bbd2-93c69801722c">
</p>
<br/>

<p>1.Creating 2 VM in Azure<p/>
 
<p>2.Client 1 (Windows 10 )<p/>
<p>3.DC-1 Domain Controller(Window server2022)<p/>
<p>4.Set Domain Controller’s NIC Private IP address to be static<p/>
  <P>
    <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/04c25aaf-2234-4ff6-a14f-31f5bfebef82">
  </P>
<p>5.Remote Desktop into VMs<p/>
<br/>

<p>
  6.Ensure Connectivity between the client and Domain Controller
</p>
<p>
  7.Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
</p>
<p>
  8.Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
</p>
<p>
  9.Check back at Client-1 to see the ping succeed(3)
</p>
<p>

  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/87eee0e8-910e-4426-98fa-bf098c811622">
</p>
<p>
  10.Enable Firewall on the server
</p>
<p>
  <img src ="https://github.com/vasiliykop/configure-ad/assets/170582503/95326b08-850b-459e-92c0-670a3055daae">
</p>
<br/>

<h2>
  Install Active Directory
</h2>
<br/>

<p>
  1. Login to DC-1 and install Active Directory Domain Services
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/b6fcf588-5c15-4e06-b1d8-4436e7842c13
">
</p>
<br/>

<p>
  2. Promote as a DC: Setup a new forest as mydomain.com 
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/905db6f5-f879-4773-a58f-e480e866e0cc">
</p>
<br/>
<p>
  3. Restart and then log back into DC-1 as user: mydomain.com\labuser

</p>
<br/>

<h2>
  Create an Admin and Normal User Account in AD
</h2>
<br/>

<p>
  1. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”(7)
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/4fb8d996-66c5-4f99-ac58-f060dc6542fe">
</p>
<br/>

<p>
  2.Create a new OU named “_ADMINS”

</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/39629309-8c58-4087-9e4c-6a35b65a15f9">
  </p>
<br/>

<p>
  3. Create a new employee named “Jane Doe” as jane_admin
</p>

<br/>

<p>
  dd jane_admin to the “Domain Admins” Security Group
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/2dd7c5cb-325a-4da0-98a4-de4d03e1387c">
</p>
<br/>

<p>
  3. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/e498a567-d962-468d-8142-e160b3e3112a">
</p>
<br/>

<h2>
  Join Client-1 to your domain (mydomain.com)
</h2>
<br/>

<p>
  1. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/7b6319f9-d4bd-4b34-9d95-f8457a937f49">
</p>
<br/>

<p>
  2. From the Azure Portal, restart Client-1
</p>
<br>

<p>
  3. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
</p>
<br/>

<p>
  4. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
</p>
<br/>

<p>
  S.etup Remote Desktop for non-administrative users on Client-1
</p>
<p>
  <img src="https://github.com/vasiliykop/configure-ad/assets/170582503/ee7d9817-6a1e-4b6f-b656-be3a7f413cc2">
</p>
