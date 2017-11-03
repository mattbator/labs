Lab 1 - Nutanix Cluster Setup
-----------------------------

This lab will familiarize you with your AHV environment that you will be
using for the majority of the labs. You will set up the networking and
NTP, as well as learn how to create a VM both from Prism and the command
line with acli. You will also look at the Acropolis Server http page on
the 2030 port, and leverage the Image Service to upload images necessary
for later labs.

Log in to Prism
~~~~~~~~~~~~~~~

1. Open a web browser and navigate to https://<*Your-cluster-IP*>:9440. Log in
to Prism using the supplied credentials.

Configure the networks
~~~~~~~~~~~~~~~~~~~~~~

In this section we will create two separate virtual networks:

-  An external network used for VMs

-  An internal network used for Acopolis File Services, which will be deployed and configured in Lab 11.

1. Click **Home > VM**

2. Click **Network Config** in the top right.

3. Enter the following info:

   a. **Name:** create a name for your network, for example >
      *LJ-Network*

   b. **VLAN ID:** 0

    **Note:** The VLAN ID is 0 because the upstream switch ports are
    configured with a native VLAN that corresponds with the third octet
    of your IP address scheme. All traffic destined for your host will
    be untagged.

4. Click **Enable IP Address Management.** Replace >
   *<primary\_network>* with the **Primary Network/Prefix > Length**
   value from your lab sheet, and *<primary\_gateway>* > with the
   **Primary Gateway** value from your lab sheet.

   a. **Network IP Address/Prefix Length:** *<primary\_network>*

   b. **Gateway:** *<primary\_gateway>*

5. Click **Configure Domain Settings.** Replace > *<dc\_ip\_address>*
   with the **DC IP Address** from your lab > sheet for the Domain Name
   Server field, and *<domain\_name>* > with the name of the domain you
   will create (it is not yet > created).

   a. **Domain Name Servers:** *<dc\_ip\_address>*

   b. **Domain Search:** <*domain\_name>*

   c. **Domain Name:** <*domain\_name>*

   d. **TFTP Server:** <blank>

   e. **Boot File Name:** <blank>

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image36.png

6. Click **+ Create Pool** and a new dialog box will open. Enter the >
   following info and click **Submit**. Fill in the values from your >
   lab sheet.

   a. **Start Address:** *<primary\_start\_ip>*

   b. **End Address:** *<primary\_end\_ip>*

    .. image:: http://static.nutanixworkshops.com/ahv_citrix/image81.png

7. Check the box **Override DHCP server**

   a. Leave the **DHCP Server IP Address** field blank

   b. Click **Submit**.

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image42.png

8. Click **+ Create Network** to create a second network.

9. Enter the following info. Refer to your lab sheet for the >
   **Secondary VLAN ID** value.

   a. **Name**: FS-Network

   b. **VLAN ID:** *<secondary\_vlan\_id>*

10. Click **Enable IP Address Management.** Replace >
   *<secondary\_network>* with the **Secondary Network/Prefix > Length**
   value from your lab sheet, and > *<secondary\_gateway>* with the
   **Secondary Gateway** value > from your lab sheet.

   a. **Network IP Address:** *<secondary\_network>*

   b. **Gateway:** *<secondary\_gateway>*

11. Click **Configure Domain Settings.** Replace > *<dc\_ip\_address>*
   with the **DC IP Address** from your lab > sheet for the Domain Name
   Server field, and *<domain\_name>* > with the name of the domain you
   will create (it is not yet > created).

   a. **Domain Name Servers:** *<dc\_ip\_address>*

   b. **Domain Search:** <*yourdomain>*

   c. **Domain Name:** <*yourdomain>*

   d. **TFTP Server:** <blank>

   e. **Boot File Name:** <blank>

12. Click **+ Create Pool** and a new dialog box will open. Enter the >
   following info and click **Submit**. Fill in the values from your >
   lab sheet.

   a. **Start Address:** *<secondary\_start\_ip>*

   b. **End Address:** *<secondary\_end\_ip>*

13. Check the box **Override DHCP server**

   a. Leave the **DHCP Server IP Address** field blank

   b. Click **Submit**.

14. Click **Close**.

Set up NTP
~~~~~~~~~~

1. Click the gear icon and click **NTP Servers.**

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image58.png

1. Enter pool.ntp.org in the field and click **Add**, then click >
   **Close**.

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image20.png

Set up Name Servers
~~~~~~~~~~~~~~~~~~~

1. Click the gear icon and click **Name Servers**.

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image51.png

1. Enter the DC IP Address from your lab sheet in the field and click >
   **Add,** then click **Close**.

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image210.png

Create the Domain Controller VM using Prism
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This lab will show you how to create an AHV VM in Prism. This VM will be
used as your Domain Controller in future labs.

**Note:** A disk will be added to the VM in a separate lab.

1. From a web browser, navigate to the Prism interface of your assigned
   > AHV cluster.

2. Navigate to **Home > VM**

3. Click **+ Create VM** in the top right.

.. image:: http://static.nutanixworkshops.com/ahv_citrix/image4.png

4. Enter the following values:

   a. **Name:** DC

   b. **Description:** Domain Controller

   c. **vCPU:** 2

   d. **Number of Cores Per vCPU:** 1

   e. **Memory:** 4

5. Click **+ Add new NIC**

6. Enter the following values and click **Add.** For >
   <primary\_network\_name> select the name of the primary > network you
   created above in step 3 of lab 2b. For example, > *LJ-Network*

   a. VLAN Name: *<primary\_network\_name>*

   b. VLAN ID: vlan.0

   c. IP Address: <blank>

7. Click **Save**.

    .. image:: http://static.nutanixworkshops.com/ahv_citrix/image187.png

Create the XenDesktop VM using acli
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This lab will show you how to create an AHV VM using acli. This VM will
be used as your XenDesktop server in future labs.

**Note:** Disks will be added to the VM in a separate lab.

1. Login to one of your CVMs using ssh.

2. Use acli to create the XenDesktop server VM.

   a. Type acli to enter the acli prompt

nutanix@cvm:~$ acli

a. Enter the following commands, where *<primary\_network>* is > the
   name of the primary network you created earlier (hint: use tab > to
   auto complete commands and fields):

    <acropolis> vm.create XD memory=24G num\_cores\_per\_vcpu=1
    num\_vcpus=4

    <acropolis> vm.nic\_create XD network=\ *<primary\_network>*

Upload required images for later labs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You will be uploading the following images:

-  Windows 2012 pre-configured disk image

-  XenDesktop installation iso

-  Windows 7 installation iso

-  virtio drivers

1. From a web browser, navigate to the Prism interface of your assigned
   > AHV cluster.

2. Open three additional tabs and launch Prism in each tab in order to >
   upload images in parallel. (4 tabs total)

3. In the first tab, begin the upload of the pre-configured Windows >
   disk image.

   a. From Prism, click the gear wheel and click **Image >
      Configuration**

   b. Click + **Upload Image** and enter the following information:

-  **Name:** windows2012\_disk

-  **Annotation:** <blank>

-  **Image Type:** DISK

-  **Container:** default-container-#####

-  **Image Source (from URL):** >
   nfs://10.21.249.12/se/Laura/SE\_Bootcamp/windows2012\_disk

   a. Click **Save**.

    **Note:** It will take approximately 15-20 minutes for this upload
    to complete.

1. In the second tab, begin the upload of the XenApp/XenDesktop >
   installation media.

   a. From Prism, click the gear wheel and click **Image >
      Configuration**

   b. Click + **Upload Image** and enter the following information:

-  **Name:** XD\_79

-  **Annotation:** <blank>

-  **Image Type:** ISO

-  **Container:** default-container-#####

-  **Image Source (from URL):** >
   nfs://10.21.249.12/iso/Citrix/XenDesktop7\_9/XenApp\_and\_XenDesktop\_7\_9.iso

   a. Click **Save**.

1. In the third tab, begin the upload of the Windows 7 installation >
   media.

   a. From Prism, click the gear wheel and click **Image >
      Configuration**

   b. Click + **Upload Image** and enter the following information:

-  **Name:** Win7

-  **Annotation:** <blank>

-  **Image Type:** ISO

-  **Container:** default-container-#####

-  **Image Source (from URL):** >
   nfs://10.21.249.12/iso/Microsoft/Win7.iso

c. Click **Save**.

.. raw:: html

   <!-- -->

1. In the fourth tab, begin the upload of the virtio drivers.

    **Note:** As of the time of this writing, the Nutanix branded virtio
    drivers do not yet work as per bug ENG-41466 so the Fedora drivers
    will be used.

a. From Prism, click the gear wheel and click **Image Configuration**

b. Click + **Upload Image** and enter the following information:

-  **Name:** virtio

-  **Annotation:** <blank>

-  **Image Type:** ISO

-  **Container:** default-container-#####

-  **Image Source (from URL):** >
   nfs://10.21.249.12/se/Laura/SE\_Bootcamp/virtio-win-0.1.102.iso

c. Click **Save**.
