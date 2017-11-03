Lab 2 - Domain Controller Setup
-------------------------------

In this lab you will add the disks you uploaded to the VMs you created
in Lab 2, and configure the domain controller. This lab assumes you have
created the DC VM in Lab 2d and the XD VM in Lab 2e. If you haven’t
created the VMs, follow the steps in Labs 2d and 2e and then return to
this lab.

Add OS disk to DC VM
~~~~~~~~~~~~~~~~~~~~

1. Select the DC VM from the Table View and click **Update**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image37.png

1. Scroll to **+ Add New Disk**

2. Click **+ Add New Disk**

3. Enter the following values and click **Add**:

   a. **Type:** Disk

   b. **Operation:** Clone from Image Service

   c. **Bus Type:** SCSI

   d. **Image:** windows2012\_disk

4. Power on the VM.

   a. From the Table view, select the VM and click **Power on.**

+------------------------------------------------------------------------+
| **Note:** This can also be done from acli, with the following commands |
| run from the CVM:                                                      |
+------------------------------------------------------------------------+
| vm.disk\_create DC clone\_from\_image=windows2012\_disk                |
+------------------------------------------------------------------------+
| vm.on DC                                                               |
+------------------------------------------------------------------------+

Configure the IP address of the DC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Select the DC VM from the Table View and click **Launch Console**.

2. In the console, on the **Settings** screen, accept the defaults and >
   click **Next.**

3. On the next screen, click **I accept**.

4. For the built-in administrator account, enter the nutanix/4u >
   password twice and click **Finish**.

5. From the bar at the top of the console screen, click the >
   **Ctrl+Alt+Del** icon to access the logon screen.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image181.png

1. Enter the Administrator password nutanix/4u and press Enter.

2. From **Server Manager,** click on **Local Server.**

    **Tip:** Click the **Server Manager** icon in the taskbar if it is
    not already launched, and then click on **Local Server**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image247.png

1. Click on **IPv4 address assigned by DHCP, IPv6 enabled** to launch >
   the **Network Connections** window.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image180.png

1. Right click the network adapter and click **Properties**

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image142.png

1. Select **Internet Protocol Version 4 (TCP/IPv4)** and click the >
   **Properties** button

2. Select **Use the following IP address** and enter in the information
   > from your lab sheet.

   a. **IP address:** *<dc\_ip\_address>*

   b. **Subnet mask:** *<primary\_subnet\_mask>*

   c. **Default gateway:** *<primary\_gateway>*

3. Select **Use the following DNS server addresses** and enter in the >
   information from your lab sheet:

   a. **Preferred DNS server:** *<dc\_ip\_address>*

   b. **Alternate DNS server:** <blank>

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image78.png

1. Click **OK**.

2. Click **Close.**

3. Close all windows except for Server Manager.

Install DNS on the DC
~~~~~~~~~~~~~~~~~~~~~

In this lab, you will install DNS on the domain controller.

1. To prepare for DNS/Active Directory installation, rename the server,
   > but don’t join it to a domain yet.

   a. From Server Manager, click **Local Server.**

   b. Click on the Computer Name (starts with WIN\*) to bring up the >
      System Properties dialog box.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image205.png

a. Click **Change…**

b. In the **Computer Name** field, type DC1

c. Click **OK** and then click **Close**.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image139.png

2.  Click **Restart Now** to restart the computer.

3.  When the server comes back online, login with the Administrator >
    username and password.

4.  From **Server Manager**, click **Add roles and features** and click
    > **Next.**\ |image2|\ {width=“3.6854735345581804in” >
    height=“2.5052088801399823in”}

5.  Click **Next** on the Before You Begin page.

6.  Select **Role-based or feature-based installation** and click >
    **Next.**

7.  Select **Select a** **server from the server pool** and make sure >
    DC1 is selected. Click **Next**.

8.  Check **DNS Server** and click **Add Features** on the pop-up >
    window, and then click **Next**.

9.  Click **Next** twice more.

10. Click **Install**.

11. After installation is complete, click **Close.**

Install and Configure Active Directory on the DC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab, you will install and configure Active Directory on the
domain controller.

**Note:** The steps below can also be found as a Microsoft TechNet
article.
`*http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx* <http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx>`__

1. From **Server Manager**, click **Add roles and features** and click >
   **Next.**

2. Click **Next** on the Before You Begin page.

3. Select **Role-based or feature-based installation** and click >
   **Next.**

4. Select **Select a** **server from the server pool** and make sure >
   DC1 is selected and click **Next**.

5. Check **Active Directory Domain Services** and click **Add >
   Features** on the pop-up window, and then click **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image82.png

6. Click **Next** twice more.

7. Click **Install**.

8. After installation is complete, click **Close.**

9. Promote the server to a domain controller. Click the flag at the top
   > of the Server Manager dialog box and click **Promote this server >
   to a domain controller**

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image255.png

10. Select the third option **Add a new forest** and type the domain >
    name for your lab (from your lab sheet) in the **Root domain >
    name** field and click **Next**.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image38.png

11. On the next page, leave the defaults for the forest and domain >
    functional levels and set the Directory Services Restore Mode >
    (DSRM) password to nutanix/4u. Click **Next**.

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image107.png

12. Click **Next** to ignore the delegation warning for DNS. You will be
    > using the AD-integrated DNS so this warning can be ignored.

13. Click **Next** on the NetBIOS screen

14. Click **Next** twice

15. Click **Install**.

16. The computer will restart.

Create a Domain Admin User
~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Log back into the domain controller with the domain administrator >
   account.

2. From **Server Manager**, click **Tools,** then click **Active >
   Directory Users and Computers**

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image30.png

4. On the left-hand column, expand the root domain and navigate to the >
   **Users** folder.

5. Right click the **Users** folder and select **New User**

6. In the **New Object - User** dialog box, enter your first name, last
   > name and user logon name in the appropriate fields and click >
   **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image224.png

7. On the next screen, select a password. Additionally, uncheck **User >
   must change password at next logon** and check **Password never >
   expires**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image140.png

8.  Click **Next** and click **Finish**.

9.  On the right-hand column, locate the user you just created and >
    highlight and right-click on the user name.

10. Click **Add to a group…** to bring up the **Select Groups** dialog >
    box.

11. Type the name **Domain Admins,** click **Check Names**, and click >
    **OK**.\ |image4|\ {width=“4.916666666666667in” > height=“2.6875in”}

12. Click OK when prompted.

13. Create a new OU called **Citrix**.

    a. Right click the root domain and click **New** **> >
       Organizational Unit**

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image175.png


b. In the **Name** field, type Citrix and click **OK**.

8. Close **Active Directory Users and Computers**.
