Lab 6 - Deliver Apps with XenApp
--------------------------------

Create a master Windows 2012 image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the VM screen in Prism, click **+ Create VM** in the top right.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image169.png

2. Enter the following values:

   a. **Name:** Win2012-Gold

   b. **vCPU:** 2

   c. **Number of Cores Per vCPU:** 2

   d. **Memory:** 16

3. Click **+ Add New Disk**

   a. **Type:** Disk

   b. **Operation:** Clone from image Service

   c. **Bus Type:** SCSI

   d. **Image:** windows2012\_disk

   e.

4. Click **+ Add New Disk**

   a. **Type:** CDROM

   b. **Operation:** Clone from image Service

   c. **Bus Type:** IDE

   d. **Image:** XD\_79

5. Enter the following values and click **Add**:

   a. VLAN Name: <your\_network>

   b. VLAN ID: vlan.0

   c. IP Address: <blank>

6. Click **Save**.

Configure the Windows 2012 image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the Table view, select the Win2012-Gold VM and click **Power >
   on.**

2. Click **Launch Console**.

3. In the console, on the **Settings** screen, accept the defaults and >
   click **Next.**

4. On the next screen, click **I accept**.

5. For the built-in administrator account, enter the nutanix/4u >
   password twice and click **Finish**.

6. From the bar at the top of the console screen, click the >
   **Ctrl+Alt+Del** icon to access the logon screen.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image138.png

1. Enter the Administrator password nutanix/4u and press Enter.

2. From **Server Manager,** click on **Local Server.**

    **Tip:** Click the **Server Manager** icon in the taskbar if it is
    not already launched, and then click on **Local Server**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image164.png

1. Click on **Local Server**

2. Click on **IPv4 address assigned by DHCP, IPv6 enabled** to launch >
   the **Network Connections** window.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image193.png

1. Right click the network adapter and click **Properties**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image115.png

1. Select **Internet Protocol Version 4 (TCP/IPv4)** and click the >
   **Properties** button

2. Select **Use the following DNS server addresses** and enter in the >
   information from your lab sheet:

   a. **IP address:** *<dc\_ip\_address>*

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image156.png

14. Click **OK**.

15. Adjust the date and time.

    a. Right-click the time and date in the system tray and click >
       **Adjust date/time**.

    b. Click the **Internet Time** tab.

    c. Click **Change settings…**

    d. Click **Update now** to sync the time.

    e. Click **OK** twice to close all windows.

16. Install VDA.

    a. Click **Start > This PC**. There should be a disk in the CD >
       Drive labeled “XA and XD”.

    b. Double click the CD Drive, and then click **AutoSelect**.

    c. Click **Start** next to **XenApp**.

    d. Select **Virtual Delivery Agent for Windows Server OS**.

    e. If prompted by User Account Control, click **Yes**.

    f. Click **Create a Master Image**

    g. Make sure **Install the Citrix Receiver** is selected.

    h. Type the name of your controller address in the field. For >
       example, xd1.yourdomain.com

    i. Click **Test connection…** to make sure the connection is >
       successful. If it is not successful, verify the DNS settings >
       from earlier and ensure you can ping/resolve the FQDN of the >
       controller address.

    j. Click **Add,** then click **Next**

    k. Leave the default options for features and click **Next**.

    l. Select **Automatically** for firewall rules and click **Next.**

    m. Click **Install**. Installation will take several minutes. You >
       will be prompted to restart the machine during the >
       installation.

    n. Once complete, select **I do not want to participate in Call >
       Home** and click **Next**.

    o. Make sure **Restart machine** is unchecked and then click >
       **Finish**.

    p. Shut down the VM.

Take snapshot
~~~~~~~~~~~~~

1. From the VM screen in Prism, highlight the Win2012-Gold VM in the >
   table and click **Take Snapshot**.

2. Enter a name for the snapshot, for example Win2012-Snap and click >
   **Submit**.

Create a Machine Catalog
~~~~~~~~~~~~~~~~~~~~~~~~

1. Using Remote Desktop, connect to your XenDesktop server and launch >
   Citrix Studio by navigating to **Start > Down Arrow > Citrix >
   Studio**.

2. From within Studio, right click on **Machine Catalogs** on the left >
   hand side and click **Create Machine Catalog**.

3. If the splash screen is displayed, click **Don’t show this again** >
   and click **Next**.

4. Click **Next**.

5. Select **Server OS** and click Next.

6. Leave the defaults of **Machines that are power managed** and >
   **Citrix Machine Creation Services** and click **Next**.

7. Select the container and click **Next**.

8. Select the snapshot you took in the previous lab and click **Next**.

9. Create 2 virtual machines, and modify the memory to 16384 and click >
   **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image13.png

10. Select the **Citrix** OU for your machines and the account naming >
    scheme. For example, XenApp-##

    **Note:** The Citrix OU should have been created as part of the DC
    configuration steps (Lab 3e, step 13).

10. Give the Machine Catalog a name, for example XenApp Servers

11. Click **Finish.**

12. From Prism, power on the VMs that were just created. Alternatively >
    you can use the following acli command:

acli vm.on XenApp-\*

Create a Delivery Group and Add Applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab you will create the delivery group. This is what will
entitle your users to access your machine catalog.

1. On the left hand side, right-click on **Delivery Groups** and click >
   **Create Delivery Group**.

2. If the splash screen is displayed, click **Don’t show this again** >
   and click **Next**.

3. Select the machine catalog you created in the previous lab, and >
   choose the number of machines for the delivery group. Click >
   **Next**.

    **Note:** The number of machines you specify for the delivery group
    can be less than or equal to the total number of machines in the
    machine catalog.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image16.png

1. Click **Next** to allow any authenticated users to use this Delivery
   > Group.

2. On the **Applications** screen, click **Add…** and then select >
   **From start menu.**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image186.png

1. Applications from one of the host machines will be presented. From >
   the list, select **Calculator** and **Notepad**, and then click >
   **OK**.

2. Click **Next**.

3. Click **Next** to skip adding a desktop. This would allow users to >
   login to the server as if it were a desktop (RDS). For this lab we >
   will just present the applications.

4. Click **Next.**

5. Give the delivery group a name and an optional description (this is >
   the name that will be shown in Studio) and click **Finish**.

Test Delivery Group
~~~~~~~~~~~~~~~~~~~

1. From your laptop navigate to >
   *http://<xd\_ip\_address>/Citrix/NutanixStoreWeb/.* For > example >
   `*http://10.20.203.22/Citrix/NutanixStoreWeb* <http://10.20.203.22/Citrix/NutanixStoreWeb>`__

2. Enter your domain username and password and click Logon.

3. Click on Apps and you should see Calculator and Notepad.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image5.png

1. Click on Calculator

2. Save and launch the .ica file

3. Calculator will now be running on your local machine.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image217.png
