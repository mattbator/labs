Lab 7 - Acropolis File Services & Profile Management
----------------------------------------------------

In this lab you will create a File Server and share using Acropolis File
Services for storing profile data. You will install ProfileUnity for the
profile management.

Deploy AFS Cluster
~~~~~~~~~~~~~~~~~~

1. First, ensure that your cluster name server is set to your domain >
   controller IP.

   a. Click the Gear icon.

   b. Click Name Servers.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image177.png

a. Check that the IP address shown matches your domain controller IP. >
   If it doesn’t, add it.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image245.png

1. From Prism, click **Home > File Server**

2. Click **+ File Server**

3. Enter in a name for your file server (e.g. FS) and a size (e.g. >
   2048). You can leave the rest default, and click Next. |Screen > Shot
   2016-02-27 at 12.42.00 > AM.png|\ {width=“6.03125in” >
   height=“5.854166666666667in”}

4. On the next screen, choose the following and click **Next**:

   a. Internal network: *<secondary\_network\_name>* e.g. > FS-Network

   b. External network: *<primary\_network\_name>* e.g. > LJ-Network

   c. DNS Server: *<dc\_ip\_address>*

   d. NTP Server: pool.ntp.org

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image159.png

5. On the next screen, enter in your domain information and click >
   **Create**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image151.png

5. It will take about 8-10 minutes for the file server to be created.

Create a File Share
~~~~~~~~~~~~~~~~~~~

1. Click on **Home > File Server**

2. Click **+ Share**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image89.png

1. Give the file share a name, for example, users

2. Check **Enable Previous Version**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image54.png

5. Log in to one of your desktops through Citrix Receiver (Refer to >
   `*Lab 6c* <#c.-test-delivery-group>`__ for detailed instructions).

6. Launch File Explorer and navigate to your file share by typing in >
   *\\\\<fileservername>\\<sharename>*. For example >
   \\\\fs.laurajordana.com\\users

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image231.png

7. You should be able to navigate the share and create folders.

Prepare a VM to install ProfileUnity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab we will create another Windows 2012 VM to install
ProfileUnity on.

1. From a web browser, navigate to the Prism interface of your assigned
   > AHV cluster.

2. Navigate to **Home > VM**

3. Click **+ Create VM** in the top right.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image232.png

1. Enter the following values:

   a. **Name:** ProfileUnity

   b. **Description:** Profile Unity

   c. **vCPU:** 2

   d. **Number of Cores Per vCPU:** 1

   e. **Memory:** 4

2. Attach the Windows disk:

   a. **Type:** Disk

   b. **Operation:** Clone from Image Service

   c. **Bus Type:** SCSI

   d. **Image:** windows2012\_disk

5.  Click **+ Add new NIC**

6.  Enter the following values and click **Add**:

    a. VLAN Name: <your\_network>

    b. VLAN ID: vlan.0

    c. IP Address: <blank>

7.  Click **Save**.

8.  From the Table view, select the ProfileUnity VM and click **Power >
    on.**

9.  Click **Launch Console**.

10. In the console, on the **Settings** screen, accept the defaults and
    > click **Next.**

11. On the next screen, click **I accept**.

12. For the built-in administrator account, enter the nutanix/4u >
    password twice and click **Finish**.

13. From the bar at the top of the console screen, click the >
    **Ctrl+Alt+Del** icon to access the logon screen.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image147.png

5. Enter the Administrator password nutanix/4u and press Enter.

6. From **Server Manager,** click on **Local Server.**

    **Tip:** Click the **Server Manager** icon in the taskbar if it is
    not already launched, and then click on **Local Server**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image18.png

5. Click on **Local Server**

6. Click on **IPv4 address assigned by DHCP, IPv6 enabled** to launch >
   the **Network Connections** window.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image53.png

5. Right click the network adapter and click **Properties**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image137.png

5. Select **Internet Protocol Version 4 (TCP/IPv4)** and click the >
   **Properties** button

6. Select **Use the following IP address** and enter in the information
   > from your lab sheet.

   a. **IP address:** *<profile\_unity\_ip\_addr>*

   b. **Subnet mask:** *<subnet\_mask>*

   c. **Default gateway:** *<default\_gateway>*

7. Select **Use the following DNS server addresses** and enter in the >
   information from your lab sheet:

   a. **Preferred DNS server:** *<dc\_ip\_address>*

   b. **Alternate DNS server:** <blank>

8. Click **OK**.

9. Join the computer to the domain you created above and change the >
   name.

   a. From **Server Manager**, click **Local Server.**

   b. Click on the Computer Name (starts with WIN\*) to bring up the >
      **System Properties** dialog box.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image52.png

a. Click **Change…**

b. Enter the following info:

   i.  **Computer Name:** profileunity

   ii. **Domain:** *yourdomain*

c. Click **OK.**

d. In the **Windows Security** dialog box, enter the Domain >
   Administrator username and password (the DSRM password you created >
   in Lab 3e. above).

    **Note:** You can also use the domain admin account you created in
    Lab 3f.

a. Click **OK**.

    You should receive a prompt that says “Welcome to the yourdomain
    domain”.

a. Click **OK** on the subsequent dialog box that appears.

b. Click **Close**.

c. Click **Restart Now** to reboot the computer.

Install ProfileUnity
~~~~~~~~~~~~~~~~~~~~

1.  Log in to the ProfileUnity server via RDP.

2.  Launch Internet Explorer by clicking **Start > Internet > Explorer**

3.  In the address bar, type or paste >
    `*http://ntnx.info/profileunity* <http://ntnx.info/profileunity>`__

4.  Click **Download**.

5.  If prompted to create a Dropbox account, click **No thanks, continue
    > to download** at the bottom of the prompt.

6.  Click **Save**.

7.  Once it is done downloading, click **Run**, or navigate to the >
    download folder and double-click the .exe.

8.  On the UAC pop up, click **Yes**.

9.  Select a language and click **OK.**

10. The Prerequisites Wizard will pop up. Click **Next**.

11. Click **Next** to install the prerequisites.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image225.png

1. Once the prerequisites are installed, the ProfileUnity Setup wizard >
   will come back. Click **Next**.

2. On the next screen, leave the default folder and click **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image40.png

1. On the Logon Information screen, enter nutanix/4u for the password >
   and click **Next**.

12. Specify **Citrix** as the broker mode and click **Next**.

13. Accept the EULA and click **Next**.

14. Click **Install** to begin the installation.

15. Once complete, click **Finish**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image103.png

Configure ProfileUnity
~~~~~~~~~~~~~~~~~~~~~~

1. Login to the ProfileUnity console by navigating to >
   https://<profile\_unity\_ip\_address>:8000 from a web > browser with
   your domain username and credentials.

2. Once logged in, enter in “Domain Users” under valid active directory
   > groups for login and click Add.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image62.png

1. Click **Next** in the lower right corner.

2. Click **No** when asked “Would you like to always skip Settings >
   setup?”

3. ProfileUnity has several template configurations to choose from. >
   From the template library, select **Windows 7, New Non-Persistent >
   VDI Deployment**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image15.png

7. Click **Next.**

8. Enter in the home share and home drive information.

   a. **Home Share:** >
      \\\\\ *<fileserver>*\\\ *<sharename>*\\%username%

   b. **Home Drive:** H:

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image77.png

9.  Click **Next**.

10. Select **Citrix** from the **Select the Active Directory Computer >
    OU** dropdown and **Domain Users** from the **Active Directory >
    User Group** dropdown.

    **Note:** Ensure your MCS desktops are in the Citrix OU by logging
    into the domain Controller, running Active Directory Users and
    Computers, and checking the Citrix OU folder. If they are not in the
    Citrix OU (and are in Computers or another OU), move them to the
    Citrix OU.

9.  Click **Run.**

10. When complete, you should see a dialog like this

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image146.png

13. Click **Close**, and then Click **Finish**.

Login to your desktop via Citrix Receiver
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From your laptop navigate to >
   http://\ *<xd\_ip\_address>*/Citrix/NutanixStoreWeb/. For > example >
   `*http://10.20.138.22/Citrix/NutanixStoreWeb* <http://10.20.138.22/Citrix/NutanixStoreWeb>`__

2. Enter in your domain user and password and click Log On.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image83.png

3. Connect to your desktop.

4. When you log in you should see this (if you don’t, you may need to >
   reboot the desktops first)

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image203.png

   Screen Shot 2016-03-03 at 7.16.49 AM.png

3. Click the **Start** menu

4. Where you would normally see “Computer”, you should now see >
   *%username%* on *%desktopname%*, for example laura\_jordana on >
   DEMO-XD-00046

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image96.png

7. Click on it and navigate to My Documents

8. Right click anywhere in the window and select **Properties** to >
   verify the location of the folder on the file share.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image185.png
