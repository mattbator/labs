Lab 5 - Deliver Desktops with XenDesktop
----------------------------------------

Create Machine Catalog
~~~~~~~~~~~~~~~~~~~~~~

In this lab you will create the machine catalog with VMs based on your
Win7-Gold image.

1. Log in to the XD server.

2. From within Studio, right click on **Machine Catalogs** on the left >
   hand side and click **Create Machine Catalog**.

3. If the splash screen is displayed, click **Don’t show this again** >
   and click **Next**.

4. Click **Next**.

5. Select **Desktop OS** and click Next.

6. Leave the defaults of **Machines that are power managed** and >
   **Citrix Machine Creation Services** and click **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image243.png

5. Select **I want users to connect to a new (random) desktop each time
   > they log on** and click **Next**.

6. Select the Nutanix container where the virtual machines’ disks will >
   be placed and click **Next**.

7. Select the snapshot you created in the previous lab and click >
   **Next**.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image33.png

8. Enter the number of virtual machines to create, for example 5. >
   Optionally adjust the resources for the machines, and click >
   **Next**.

9. Select the **Citrix** OU for placing the computer accounts and >
   create an account naming scheme, for example Win7-MCS-##

    **Note:** The Citrix OU should have been created as part of the DC
    configuration steps (Lab 3e, step 13).

8. Click **Next**.

9. Provide a name for the Machine Catalog.

    **Note:** The Machine Catalog name is not displayed to users.

11. Click **Finish. **

    **Note:** It will take a few minutes to create the Machine Catalog.
    In Prism, you will see a new temporary VM created with the prefix
    **Preparation**. This VM will disappear after the machine creation
    is complete.

11. In Prism, you should see your VMs created.

12. Power on the VMs.

    **Note:** You can power on the VMs either from Prism or from Citrix
    Studio, by highlighting the machines within the Machine Catalog and
    clicking Start.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image246.png

13. From Citrix Studio, ensure all the VMs registered with the DDC by >
    double clicking the Machine Catalog and checking the >
    **Registration State** tab under the **Desktop OS Machines** tab.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image98.png
   :alt:
   :width: 6.50000in
   :height: 1.25000in

Create Delivery Group
~~~~~~~~~~~~~~~~~~~~~

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

    .. figure:: http://static.nutanixworkshops.com/ahv_citrix/image24.png

1. Click **Next** to allow any authenticated users to use this Delivery
   > Group.

2. Click **Next** to skip adding applications.

3. Click **Add…** to add users or groups who can launch a desktop from >
   this Delivery Group.

4. On the **Add Desktop** dialog, give the Delivery Group a name and a >
   display name (the latter will be what the users see when they >
   login).

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image35.png

1. Click **OK.**

2. Click **Next.**

3. Give the delivery group a name and an optional description.

4. Click **Finish**. After a few minutes, all desktops should be >
   registered so that Unregistered shows 0.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image166.png

Test Delivery Group
~~~~~~~~~~~~~~~~~~~

1. From your laptop, navigate to >
   http://\ *<xd\_ip\_address>*/Citrix/NutanixStoreWeb/ For > example: >
   `*http://10.20.138.22/Citrix/NutanixStoreWeb* <http://10.20.138.22/Citrix/NutanixStoreWeb>`__

2. Click **Install** to install Citrix Receiver on your >
   laptop.

3. On the next page, click **I agree** and **Download**

4. Install the Citrix Receiver on your laptop, and then click >
   **Continue**.

5. Click **Launch Application** and click **Open** if prompted.

6. If Citrix Receiver doesn’t launch then click **Already installed** >
   to go to the logon prompt.

7. Enter in your domain user and password and click **Log >
   On**.

8. Under the **Desktops** tab, you should be able to see and connect to
   > **My Desktop**. You may also be automatically prompted to download
   > and launch an .ica file which will launch Citrix Viewer and >
   connect you to your desktop.

.. figure:: http://static.nutanixworkshops.com/ahv_citrix/image227.png
