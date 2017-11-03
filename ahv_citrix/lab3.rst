Lab 3 - XenDesktop Install
--------------------------

Configure XenDesktop Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab you will configure the XenDesktop server IP address and
domain membership.

1. From Prism, select the XD VM from the Table View and click **Launch >
   Console**.

2. In the console, on the **Settings** screen, accept the defaults and >
   click **Next.**

3. On the next screen, click **I accept**.

4. For the built-in administrator account, enter the nutanix/4u >
   password twice and click **Finish**.

5. From the bar at the top of the console screen, click the >
   **Ctrl+Alt+Del** icon to access the logon screen.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image134.png

1. Enter the Administrator password nutanix/4u and press Enter.

2. From **Server Manager,** click on **Local Server.**

    **Tip:** Click the **Server Manager** icon in the taskbar if it is
    not already launched, and then click on **Local Server**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image14.png

1. Click on **Local Server**

2. Click on **IPv4 address assigned by DHCP, IPv6 enabled** to launch >
   the **Network Connections** window.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image188.png

1. Right click the network adapter and click **Properties**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image55.png

1. Select **Internet Protocol Version 4 (TCP/IPv4)** and click the >
   **Properties** button

2. Select **Use the following IP address** and enter in the information
   > from your lab sheet.

   a. **IP address:** *<xd\_ip\_address>*

   b. **Subnet mask:** *<primary\_subnet\_mask>*

   c. **Default gateway:** *<primary\_gateway>*

3. Select **Use the following DNS server addresses** and enter in the >
   information from your lab sheet:

   a. **Preferred DNS server:** *<dc\_server\_ip>*

   b. **Alternate DNS server:** <blank>

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image160.png

1. Join the computer to the domain you created above and change the >
   name.

   a. From **Server Manager**, click **Local Server.**

   b. Click on the Computer Name (starts with WIN\*) to bring up the >
      **System Properties** dialog box.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image87.png

a. Click **Change…**

b. Enter the following info:

   -  **Computer Name:** XD1

   -  **Domain:** >
      *yourdomain*

c. Click **OK.**

d. In the **Windows Security** dialog box, enter the Domain >
   Administrator username and password (the DSRM password you created >
   in Lab 3e. above).

    **Note:** You can also use the domain admin account you created in
    Lab 3f.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image102.png

a. Click **OK**.

    You should receive a prompt that says “Welcome to the yourdomain
    domain”.

a. Click **OK** on the subsequent dialog box that appears.

b. Click **Close**.

c. Click **Restart Now** to reboot the computer.

Install XenDesktop
~~~~~~~~~~~~~~~~~~

16. Login with the Domain Admin user you created in Lab 3f. For example,
    > yourdomain\\laura\_jordana

17. Click **Start** and then click **This PC**. There should be a disk >
    in the CD Drive labeled “XA and XD”.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image154.png

18. Double-click on the CD Drive to open it, and then double-click >
    **AutoSelect**.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image221.png

11. When the XenDesktop splash screen launches, click **Start** next to
    > **XenDesktop**.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image135.png

12. Click on **Delivery Controller**. > |image8|

13. If prompted, click **Yes** on the **User Account Control** screen.

14. Accept the Software License Agreement by selecting **I have read, >
    understand, and accept the terms of the license agreement.**

15. On the next screen, make sure all Core Components are selected and >
    click **Next**. Compare these components to the components listed >
    on the architecture sheet. > |image9|\ {width=“6.5in” >
    height=“4.861111111111111in”}

    **Note:** Citrix generally recommends to install each component on a
    separate server, but for the purpose of this lab we will be
    installing everything together.

12. On the next screen, make sure both **Install Microsoft SQL Server >
    2012 SP2 Express** and **Install Windows Remote Assistance** are >
    checked, and then click **Next**. > |image10|\ {width=“6.5in” >
    height=“4.861111111111111in”}

16. On the **Firewall** screen, make sure **Automatically** is selected
    > and click Next.

17. Click **Install**.

    **Note:** Installation can take several minutes and the computer
    will restart 1-2 times during the process. When the computer
    restarts, log back in so installation can complete.

18. Once complete, select **I do not want to participate in Call Home**
    > and click **Next**

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image92.png

18. Uncheck **Launch Studio** and click **Finish**.

Install the Nutanix plugin for MCS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the XenDesktop VM, open a web browser and navigate to >
   `*http://ntnx.info/xdplugin* <http://ntnx.info/xdplugin>`__ to access
   > the Nutanix plugin for MCS.

2. Click **Download**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image133.png

1. If prompted to create a Dropbox account, click **No thanks, continue to download** at the bottom of the prompt.

3. Click **Save** when prompted, then click **View Downloads**.

4. Click **Run** to launch the installer.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image141.png

5. When the installation dialog pops up, click **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image235.png

6.  Select **I accept the terms in the License Agreement** and click >
    **Next.**

7.  Click **Next**, then click **Install**.

8.  If prompted, click **Yes** on the **User Account Control** screen.

9.  Click **Finish**.

10. Close all windows.

Set up the XenDesktop site
~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Launch Citrix Studio by navigating to **Start > Down Arrow > > Citrix
   Studio**

2. If prompted, click **Yes** on the **User Account Control** screen.

3. From Citrix Studio, select **Deliver applications and desktops to your users**

4. Select the radio box **A fully configured, production-ready Site >
   (recommended for new users)** and select a name for your site, >
   e.g. NutanixLab. Click **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image57.png

   Screen Shot 2016-03-31 at 5.10.18 PM.png

1. Leave the defaults for Databases and click **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image239.png

1. On the **Licensing** screen, leave the defaults as follows and click
   > **Next**:

   a. **License server address:** localhost:27000

   b. Select **Use the free 30-day trial**

2. Click **Nutanix Acropolis** as the Connection type and enter in the >
   connection details for your cluster, then click **Next**.

   a. **Connection address:** <cluster\_external\_ip>

   b. **Username:** admin

   c. **Password:** nutanix/4u

   d. **Connection name:** AHV

   e. **Create virtual machines using:** Studio tools (Machine >
      Creation Services)

3. On the next screen, select your network and enter a name for your >
   resources, for example the name of your cluster, then click >
   **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image150.png

1. Click **Next**, leaving the additional features unchecked.

2. Click **Finish**.

    **Note:** Configuration will take several minutes.

Create Storefront Server
~~~~~~~~~~~~~~~~~~~~~~~~

In this lab you will create a Storefront server. This is where your
users will connect to to access their desktops.

1. Using Remote Desktop, connect to your XenDesktop server and launch >
   Citrix Studio by navigating to **Start > Down Arrow > Citrix >
   Studio**.

2. Click **Citrix Storefront** on the left hand side and click **Create a Store**

3. Click **Next**.

4. Enter NutanixStore for the store name and click **Next**.

5. Click **Add..**. to bring up the Add Delivery Controller dialog.

6. Click **Add..**. to add your delivery controller to the Servers >
   field.

7. Enter the FQDN of your delivery controller. For example, >
   xd1.yourdomain.com. Click **OK**.

8. Change the transport type to **HTTP**. This is needed because we >
   don’t have a self-signed certificate.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image248.png

1. Click **OK** to close the **Add Delivery Controller** screen.

2. Click **Next**.

3. Uncheck **Enable Remote Access** if it is checked and click >
   **Next**.

4. Click **Next** on the **Configure Authentication Methods** screen.

5. Leave the defaults and click **Create**.

6. Click **Finish**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image201.png
