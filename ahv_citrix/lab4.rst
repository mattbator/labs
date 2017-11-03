Lab 4 - Gold Image Creation
---------------------------

In this lab you will create a gold image from scratch and prepare it for
use as a golden image. This VM will contain 2 vCPU, 2 GB RAM and will
have 4 disks attached (1 OS disk and 3 CD-ROM devices - Win7 ISO, virtio
drivers, and XenDesktop ISO for installing the Virtual Delivery Agent).

Create Windows 7 VM
~~~~~~~~~~~~~~~~~~~

1. Login to the Prism interface.

2. From the VM screen in Prism, click **+ Create VM** in the top right.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image84.png

2. Enter the following values:

   a. **Name:** Win7-Gold

   b. **vCPU:** 2

   c. **Number of Cores Per vCPU:** 1

   d. **Memory:** 2

3. Click **+ Add New Disk**

4. Enter the following values and click **Add**:

   a. **Type:** Disk

   b. **Operation:** Allocate on Container

   c. **Bus Type:** SCSI

   d. **Container:** default-container-xxxxx

   e. **Size (GiB):** 30

5. Click **+ Add New Disk**

6. Enter the following values and click **Add**:

   a. **Type:** CDROM

   b. **Operation:** Clone from Image Service

   c. **Bus Type:** IDE

   d. **Image:** Win7

+----------------------------------------------------------------------------------------------------------------------------+
| **Note:** You can also edit the existing empty CDROM device attached to the VM for any one of the 3 CDROM’s being added.   |
+----------------------------------------------------------------------------------------------------------------------------+

3. Click **+ Add New Disk**

4. Enter the following values and click **Add**:

   a. **Type:** CDROM

   b. **Operation:** Clone from Image Service

   c. **Bus Type:** IDE

   d. **Image:** virtio

5. Enter the following values and click **Add**:

   a. **Type:** CDROM

   b. **Operation:** Clone from Image Service

   c. **Bus Type:** IDE

   d. **Image:** XD\_79

6. Click **+ Add new NIC**

7. Enter the following values and click **Add**:

   a. VLAN Name: <your\_network>

   b. VLAN ID: vlan.0

   c. IP Address: <blank>

8. Click **Save**.

Install and Configure Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the Table view, select the Win7-Gold VM and click **Power on.**

2. Click **Launch Console**.

3. Install Windows using the virtio drivers. Please refer to pages >
   31-32 from the **AHV Lab Manual** for detailed instructions: >
   `*https://goo.gl/ZrZZ4Y* <https://goo.gl/ZrZZ4Y>`__ The instructions
   > are for Windows 2012 but the steps are similar.

**Note:**

-  When installing virtio drivers, use the path: >
   **<CDROM\_PATH>\\vioscsi\\w7\\amd64**

-  Set the Windows username and password as follows:

   -  Username: nutanix

   -  Password: nutanix/4u

-  Select **Ask Me Later** for Windows Updates.

1. Once Windows is done installing (~15 minutes), navigate to Device >
   Manager.

   a. Click **Start >** right-click on **Computer > > Properties >
      Device Manager**

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image144.png

1. Install the drivers for the Ethernet controller and the VirtIO >
   Balloon Driver as described in the **Acropolis Hands On Lab > Guide**
   above (or install the Nutanix Guest Tools by highlighting > the VM in
   Prism and clicking **Manage Guest Tools**).

2. Update the network adapter to point to your domain controller as the
   > primary DNS server (required for the VDA installation).

   a. Right-click the network adapter in the system tray and click >
      **Open Network and Sharing Center**.

   b. On the left-hand side, click **Change adapter settings.**

   c. Right-click the adapter and select **Properties**.

   d. Select **Internet Protocol Version 4 (TCP/IPv4)** and click the >
      **Properties** button

   e. Select **Use the following DNS server addresses** and enter in >
      the information from your lab sheet:

      i. **IP address:** *<dc\_ip\_address>*

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image212.png

7.  Click **OK.**

8.  Click **Close**.

9.  Adjust the date and time.

    a. Right-click the time and date in the system tray and click >
       **Adjust date/time**.

    b. Click the **Internet Time** tab.

    c. Click **Change settings…**

    d. Click **Update now** to sync the time.

    e. Click **OK** twice to close all windows.

10. Disable the firewall.

    a. Click **Start > Control Panel.**

    b. Click **System and Security.**

    c. Click **Windows Firewall**.

    d. Click **Advanced settings**.

    e. Click > **Properties.**

    f. For each Profile tab, select **Firewall State:** Off

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image214.png

a. Click **OK.**

b. The firewall settings should look like the screenshot.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image202.png

Install Citrix Virtual Delivery Agent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Click **Start > Computer**. There should be a disk in one of the > CD
   Drives labeled “XA and XD”.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image46.png

3.  Double-click on the CD Drive to open it, and then double-click >
    **AutoSelect**.

4.  Click **Start** next to XenDesktop.

5.  The following screen should look familiar, from when the Delivery >
    Controller was installed. This time, click **Virtual Delivery >
    Agent for Windows Desktop > OS**.

6.  Click **Yes** when prompted by UAC.

7.  Click **Create a Master Image.**

8.  Click **No, install the standard VDA.**

9.  Make sure **Install the** **Citrix Receiver** is selected.

10. Type the name of your controller address in the field. For example,
    > xd1.yourdomain.com

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image206.png

3.  Click **Test connection…** to make sure the connection is >
    successful. If it is not successful, verify the DNS settings from >
    the previous lab and ensure you can ping/resolve the FQDN of the >
    controller address.

4.  Click **Add.**

5.  Click **Next.**

6.  Leave the default options for features and click **Next**.

7.  Click **Next.**

8.  Select **Automatically** for firewall rules and click **Next**.

9.  Click **Install**. Installation will take several minutes.

10. Select **I do not want to participate in Call Home** and click >
    **Next**.

11. Make sure **Restart machine** is checked and then click **Finish**.
    > Installation will take several minutes and the computer will >
    reboot.

Install BPAnalyzer
~~~~~~~~~~~~~~~~~~

1. Login to the Windows 7 VM with the default nutanix credentials.

2. If the Citrix Receiver dialog pops up, click **Close**.

3. Launch **Internet Explorer** from the taskbar and navigate to >
   `*http://www.bpanalyzer.com* <http://www.bpanalyzer.com>`__

4. Click **Download the BPA**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image179.png

1. Download both the Analyzer and the XML >
   file.

2. Unzip the files so there are two folders **BPASetupv1** and >
   **BPAProfile\_v0.6**.

3. Open the folder **BPASetupv1** and double-click on the .msi >
   installer.

4. Click **Run** when prompted.

5. Click **Yes** when prompted by UAC.

6. Step through the installer, accepting the defaults.

7. Click **Close.**

Run BPAnalyzer
~~~~~~~~~~~~~~

1. Disable UAC.

   a. Navigate to **Start >** **Control Panel**

   b. Search for UAC.

   c. Click **Change User Account Control** **Settings**

   d. Move the slider to **Never notify** and click **OK.**

   e. Click **Yes** at the UAC prompt.

2. Reboot the computer.

3. Login with the nutanix credentials.

4. Navigate to **Start > All Programs > BP Analyzer > BP > Analyze**\ r

5. Click **File > Load BPA Ruleset**

6. Navigate to the **BPAProfile** folder you extracted and double-click
   > the BPAProfile XML document to open it. For example, >
   BPAProfile\_v0.7.xml

7. Click **Select > Select Failed**

8. Click **Apply Items** to update the registry with the recommended >
   best practices. The **Failed to set: VMware Tools installed > error**
   is expected because VMware Tools is not installed on this > VM. Click
   **OK**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image88.png

1. Close BP Analyzer.

2. Click **Start > Shut Down.**

Take a Snapshot of the Gold Image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the VM screen in Prism, highlight the Win7-Gold VM in the table
   > and click **Take Snapshot**.

2. Enter a name for the snapshot, for example Win7-Snap and click >
   **Submit**.
