# ColorLight_FPGA_boards
Update IceStudio (Windows version) to support ColorLight 5A-75X, i5 and ICeSugar Pro FPGA boards


## New supported boards in IceStudio and Apio

- Colorlight 5A-75B
- Colorlight 5A-75F
- Colorlight i5
- IceSugar Pro 

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/icestudio_boards.png)

## How to Update IceStudio and Apio to support these boards

Download the Windows WIP version of IceStudio **0.5.1w210224** from https://downloads.icestudio.io/  
The required files are included in the folder **Icestudio_update_boards**

**Icestudio** 
1) In the folder -> **C:\Program Files\icestudio\resources\boards**
Add the files of   [icestudio_add.zip](https://github.com/benitoss/ColorLight_FPGA_boards/raw/main/Icestudio_update_boards/icestudio_add.zip) file (overwrite the menu.json file)

**APIO**
1)  In the folder   -> **C:\Users\your_user\.icestudio\apio\packages**  
Add the files of [toolchain-opefpgaload.zip](https://github.com/benitoss/ColorLight_FPGA_boards/raw/main/Icestudio_update_boards/toolchain-opefpgaload.zip) file
2)  In the folder   -> **C:\Users\your_user\.icestudio\apio\packages**  
Add the files of  [toolchain-ecpdap.zip](https://github.com/benitoss/ColorLight_FPGA_boards/raw/main/Icestudio_update_boards/toolchain-ecpdap.zip) file
3)  In the folder    --> **C:\Users\your_user\.icestudio\apio**  
Overwrite profile.json file of [profile.zip](https://github.com/benitoss/ColorLight_FPGA_boards/raw/main/Icestudio_update_boards/profile.zip) file
4)   In the folder   --> **C:\Users\your_user\.icestudio\venv\Lib\site-packages\apio\resources**  
Overwrite programmers.json y boards.json  files of [resources.zip](https://github.com/benitoss/ColorLight_FPGA_boards/raw/main/Icestudio_update_boards/resources.zip) file
5)  In the folder  --> **C:\Users\your_user\.icestudio\venv\Lib\site-packages\apio**  
Overwrite util.py file of [util.zip](https://github.com/benitoss/ColorLight_FPGA_boards/raw/main/Icestudio_update_boards/util.zip) file

# JTAG Programmers

Because the Colorlight 5A-75B and 5A-75E not include a JTAG programmer, you will need an external JTAG programmer
In case of Colorlight i5 or ICeSugar Pro use a STM32 based programmer that is too slow (It spends more than 1 minute), so it is recomended to use an external JTAG programmer too

The recomended JTAG programmers are:
1) FT2232H
2) FT232H
3) USB-Blaster

My JTAG programmer is the FT2232H   from here --> https://www.aliexpress.com/item/32806818411.html

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/ft2232h_1.png)

Because I use the same programmer in other Xilinx Boards I have applied a mod to this programmer (If you only are going to use for Lattice  ECP5 board you don't need to do it)
The mod is based in change the content of its EPROM , here you have the instructions  -->  https://gist.github.com/rikka0w0/24b58b54473227502fa0334bbe75c3c1

Working in windows you have to install the LibUSBk driver to get the programmer be recognized by the programmer software included in Apio

In the same way of other boards in IceStudio, you can use Zadig to install the LibUsbK driver if you want to use the programmer in IceStudio/Apio.

If you applied the mod of the EPROM in your ft2232H board and you install the Xilinx Drivers, in Zadig you will be the FT2232H board as Digilent Adept USB Device (Interface 0) and you can install the driver libUsbK

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/zadig.png)

But in my case, because I use the board for Lattice ECP5 and for Xilinx boards in ISE/Vivado, I don't use Zadig to install the LibUsbK driver because the FT2232H programmer will not work with Xilinx IDE. So, to recover easily the original driver that works in Xilinx, I use an alternative method.  First, I install the Xilinx driver of the FT2232H board after modifying the EPROM and later I use the alternative method to modify the driver.

**How to install and change the LibUSbK driver (Alternative Method to Zadig. It allows recover the driver easily)**

I use the utility USB Driver Tool, you can download from https://visualgdb.com/UsbDriverTool/  The last version is here --> https://sysprogs.com/getfile/1372/UsbDriverTool-2.1.exe
In case you use the FT2232H JTAG programmer, you will see the "USB Serial Converter A" with VID 0403 and VPI 6010. With FT232H is similar and with USB-Blaster you will see"Altera USB Blaster"

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/USB_Driver_Tool_1.jpg)

So, You have to press right mouse button over it and select " Install Libusb-WinUSB"

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/USB_Driver_Tool_2.jpg)

You will see in the line of "USB Srial Converter A"  in parenthesis Libusb-WinUSB. Now, You have the drivers already installed

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/USB_Driver_Tool_3.jpg)

If you want to revert the original driver of the FT2232H in order to use with Xilinx ISE or Vivado IDE , you only has to press right button over "USB Serial Converter A" again and select "Restore default driver", the driver will be restored to the original.

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/USB_Driver_Tool_4.jpg)

And you will see the original state with the device name without nothing in parenthesis . Now the board has recovered the original Xilinx sriver and I can use it in ISE and Vivado Xilinx IDEs 

In this way you can use the FT2232H JTAG programmer with any board  
The way to install the driver is equivalent for FT232H or USB-Blaster programmers

**Conections for Ft2232h**

Here you have the JTAG connections of the FT2232H board to program the board. Note: It is not necessary connect the VCC connector
If you apply the MOD of the EPROM, you will have an USB-UART converter in the Second port "USB Serial Converter B" and you can use as a traditional USB-UART convertor

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/ft2232h_2.png)

![alt text](https://github.com/benitoss/ColorLight_FPGA_boards/blob/main/images/ft2323h_3.jpg)

