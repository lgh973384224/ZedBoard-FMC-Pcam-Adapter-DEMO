ZedBoard FMC Pcam Adapter DEMO
------------------------------

Description
------------

This project demonstrates the usage of the FMC Pcam Adapter as an interface from one to four different Pcam cameras and the ZedBoard platform.
The Video Stream from each different camera is getting in through the MIPI/FMC connectors and out through the carrier VGA port. For errors and feed-back messages, an uart interface is present.

First and foremost
------------------

* The Vivado projects are version-specific. Source files are not backward compatible and not automatically forward compatible. Release tags specify the targetted Vivado version. There is only one version targetted per year, as chosen by Digilent. Non-tagged commits on the master branch are either at the last tagged version or the next targeted version. This is not ideal and might be changed in the future adopting a better flow.
* Our projects use submodules to bring in libraries. Use --recursive when cloning or git submodule init, if cloned already non-recursively.

Hardware Requirements
---------------------

* ZedBoard
* FMC Pcam Adapter
* From one to four different Pcam 5C cameras
* Monitor with VGA input 

Software Requirements
---------------------

* Vivado 2018.2 Installation with Xilinx SDK: To set up Vivado, see the Installing Vivado and Digilent Board Files Tutorial.

Demo Setup
----------

1. Download the most recent release ZIP archive ("FMC-Pcam-Adapter-2018.2-*.zip") from the repo's [releases page]().
2. Extract the downloaded ZIP.
3. Open the XPR project file, found at \<archive extracted location\>/vivado_proj/ZedBoard-FMC-Pcam-Adapter-DEMO.xpr, included in the extracted release archive in Vivado 2018.2.
4. In the toolbar at the top of the Vivado window, select **File -> Export -> Export Hardware**. Select **\<Local to Project\>** as the Exported Location and make sure that the **Include bitstream** box is checked, then click **OK**.
5. In the toolbar at the top of the Vivado window, select **File -> Launch SDK**. Select **\<Local to Project\>** as both the workspace location and exported location, then click **OK**.
6. With Vivado SDK opened, wait for the hardware platform exported by Vivado to be imported.
7. In the toolbar at the top of the SDK window, select **File -> New -> Application Project**.
8. Fill out the fields in the first page of the New Application Project Wizard as in the table below. Most of the listed values will be the wizard's defaults, but are included in the table for completeness.

| Setting                                 | Value                                              |
| --------------------------------------- | -------------------------------------------------- |
| Project Name                            | ZedBoard_FMC_Pcam_Adapter_DEMO                     |
| Use default location                    | Checked box                                        |
| OS Platform                             | standalone                                         |
| Target Hardware: Hardware Platform      | system_wrapper_hw_platform_0                       |
| Target Hardware: Processor              | (default)                                          |
| Target Software: Language               | C++                                                |
| Target Software: Board Support Package  | Create New (ZedBoard_FMC_Pcam_Adapter_DEMO_bsp)    |

9. Click **Next**.
10. From the list of template applications, select "Empty Application", then click **Finish**.
11. In the Project Explorer panel to the left of the SDK window, expand the new application project (named "ZedBoard_FMC_Pcam_Adapter_DEMO").
12. Right click on the "src" subdirectory of the application project and select **Import**.
13. In the "Select an import wizard" pane of the window that pops up, expand **General** and select **File System**. Then click **Next**.
14. Fill out the fields of the "File system" screen as in the table below. Most of the listed values will be the defaults, but are included in the table for completeness.

| Setting                                                | Value                                                                     |
| -                                                      | -                                                                         |
| From directory                                         | \<archive extracted location\>/sdk_appsrc/ZedBoard_FMC_Pcam_Adapter_DEMO  |
| Files to import pane: pcam_vdmi_hdmi                   | Checked box                                                               |
| Into folder                                            | ZedBoard_FMC_Pcam_Adapter_DEMO/src                                        |
| Options: Overwrite existing resources without warning  | Checked box                                                               |
| Options: Create top-level folder                       | Unchecked box                                                             |

15. Click **Finish**.

**Note**: Users have reported some custom IP drivers missing from the hardware platform. Check the system_wrapper_hw_platform_0 project's drivers folder to ensure that the <code>MIPI_CSI_2_RX_v1_0</code>, <code>MIPI_D_PHY_RX_v1_0</code>, and <code>video_scaler_v1_0</code> drivers are present. If any of them are missing, they must be manually added to the workspace's software repositories. Click **Xilinx -> Repositories** in the menu bar at the top of the SDK window. For each missing driver, add a **New** local repository to the workspace, selecting "\<archive extracted location\>/vivado_proj/\<project name\>.ipdefs/vivado-library/ip/\<missing IP name\>/driver" as the repository directory. For more information, see [this thread](https://forums.xilinx.com/t5/Embedded-Development-Tools/Custom-IP-driver-not-present-on-BSP/td-p/902331) on the Xilinx Forums.

16. Open a serial terminal application (such as TeraTerm) and connect it to the ZedBoard serial port, using a baud rate of 115200.
17. In the toolbar at the top of the SDK window, select **Xilinx -> Program FPGA**. Leave all fields as their defaults and click "Program".
18. In the Project Explorer pane, right click on the "ZedBoard_FMC_Pcam_Adapter_DEMO" application project and select "Run As -> Launch on Hardware (System Debugger)".
19. The application will now be running on the ZedBoard. If there are any unconnected cameras, the serial interface should print a message which signals the improper initialization. 
20. If needed, create a first-stage bootloader (FSBL) using **File -> New -> Application Project** and choosing template **Zynq FSBL**.


Next Steps
----------
This demo can be used as a basis for other projects by modifying the hardware platform in the Vivado project's block design or by modifying the SDK application project.
Check out the wiki page of the demo [here](https://reference.digilentinc.com/learn/programmable-logic/tutorials/zedboard-fmc-pcam-adapter-demo/start#download_and_launch_the_zedboard_fmc-pcam-adapter_demo).

For technical support or questions, please post on the [Digilent Forum](https://forum.digilentinc.com/).

Additional Notes
----------------
For more information on how this project is version controlled, refer to the [digilent-vivado-scripts repo](https://github.com/digilent/digilent-vivado-scripts).

