---
bg: "linux.jpg"
layout: post
comments: true
title:  "Understanding Computer Hardware"
crawlertitle: "Understanding Computer Hardware"
summary: "Понимание компьютерного оборудования"
date:   2017-11-07 17:15:00 +0300
categories: posts
tags: ['linux']
author: DenIvTea
---

<p>One of the many advantages of having so many different Linux distributions is that some of them are designed to run on specific hardware platforms.  In fact, there is a Linux distribution specifically designed for just about all modern hardware platforms.</p>

<p>Each of these hardware platforms has a great deal of variety in the hardware components that are available.  In addition to several different types of hard drives, there are many different monitors and printers.  With the popularity of USB devices, such as USB storage devices, cameras and cell phones, the number of available devices numbers in the thousands.</p>

<p>In some cases, this poses problems as these hardware devices typically need some sort of software (called drivers or modules) that allows them to communicate with the installed operating system.  Hardware manufactures often provide this software, but typically for Microsoft Windows, not Linux.  The Linux mascot, <strong>Tux</strong>, is however starting to appear more often on hardware products, indicating Linux support.</p>

<p>In addition to vendor support, there is a great deal of community support that strives to provide drivers for Linux systems.  Although not all hardware has the necessary drivers,  there is a good amount that does, making the challenge for Linux users and administrators to either find the correct drivers or choose hardware that has some level of support in Linux.</p>

<p>In this chapter, you will learn about core hardware devices, including how to use Linux commands to display vital hardware device information.</p>

Навигация по статье:

* <a href="#2">1.1 Processors</a>
* <a href="#3">1.2 Motherboards and Buses</a>
* <a href="#4">1.2.1 dmidecode</a>
* <a href="#5">1.2.2 Random Access Memory</a>
* <a href="#6">1.2.3 Peripheral Devices</a>
* <a href="#7">1.2.4 Universal Serial Bus Devices</a>
* <a href="#8">1.3 Hardware Abstraction Layer</a>
* <a href="#9">1.4 Disk Devices</a>
* <a href="#10">1.5 Optical Disks</a>
* <a href="#11">1.6 Video Display Devices</a>
* <a href="#12">1.7 Managing Devices</a>
* <a href="#13">1.8 Power Supplies</a>

<h2><a name="2">1.1 Processors</a></h2>
<p>A <var>Central Processing Unit</var> (CPU or processor) is one of the most important hardware components of a computer.  It performs the decision making as well as the calculations that need to be performed to properly run an operating system.  The processor is essentially a computer chip.</p>

<p>The processor is connected to the other hardware via a <var>motherboard</var>, also known as the system board.  Motherboards are designed to work with specific types of processors.</p>

<p>If a hardware system has more than one processor, the system is referred to as a <var>multiprocessor</var>.  If more than one processor is combined into a single processor chip, then it is called <var>multi-core</var>.</p>

<p>Although support is available for more types of processors in Linux than any other operating system, there are primarily just two types of processors used on desktop and server computers: x86 and x86_64.  On an x86 system, the system processes data 32 bits at a time; on a x86_64 the system processes data 64 bits at a time.  A x86_64 system is also capable of also processing data 32 bits at a time in a backward compatible mode.  One of the main advantages to a 64 bit system is that the system is able to work with more memory.</p>

<p>The x86 family of processors was originated by Intel in 1978 with the release of the 8086 processor.  Since that time, <strong>Intel</strong> has produced many other processors that are improvements to the original 8086; they are known generically as x86 processors.  These processors include the 80386 (also known as the i386), 80486 (i486),  the Pentium series (i586) and the Pentium Pro series ( i686).  In addition to Intel,  other companies like <strong>AMD</strong> and Cyrix have also produced x86 compatible processors.  While Linux is capable of supporting processors back to the i386 generation, many distributions limit their support to i686 or later.</p>

<p>The x86_64 family of processors, including the 64 bit processors from Intel and AMD,  have been in production since around the year 2000.  As a result, most of the modern processors built today are x86_64.  While the hardware has been available for over a decade now, the software to support this family of processors has been much slower to develop.  Even as of 2013, there are many software packages that are available for the x86 architecture, but not the x86_64.</p>
 
<p>You can see the family your CPU belongs to, using the <code>arch</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> arch                                                    
x86_64                                                                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>Another command you can use to identify the type of CPU in your system is the <code>lscpu</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>  lscpu                                                  
<span class="attention"><span class="ansi-red">Architecture:          x86_64</span></span>                                              
<span class="attention"><span class="ansi-red">CPU op-mode(s):        32-bit, 64-bit</span></span>                                       
Byte Order:            Little Endian                                          
CPU(s):                4                                                      
On-line CPU(s) list:   0-3                                                    
Thread(s) per core:    1                                                      
Core(s) per socket:    4                                                      
Socket(s):             1                                                      
NUMA node(s):          1                                                      
Vendor ID:             GenuineIntel                                           
CPU family:            6                                                      
Model:                 44                                                     
Stepping:              2                                                      
CPU MHz:               2394.000                                               
BogoMIPS:              4788.00                                              
Virtualization:        VT-x                                                   
Hypervisor vendor:     VMware                                                 
Virtualization type:   full                                                   
L1d cache:             32K                  
L1i cache:             32K                                                    
L2 cache:              256K                                                   
L3 cache:              12288K                                                 
NUMA node0 CPU(s):     0-3                                                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> </pre>




<p>The first line of this output shows that the CPU is being used in a 32 bit mode, as the architecture reported is x86_64.  The second line of output shows that the CPU is capable of operating in either a 32 or 64 bit mode, therefore it is actually a 64 bit CPU. </p>
 
<p>The most detailed way of displaying information about your CPU(s) is viewing the <code class="console">/proc/cpuinfo</code> file with the <code>cat</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat /proc/cpuinfo                                       
processor       : 0                                                           
vendor_id       : GenuineIntel                                                
cpu family      : 6                                                           
model           : 44                                                          
model name      : Intel(R) Xeon(R) CPU           E5620  @ 2.40GHz             
stepping        : 2                                                           
microcode       : 0x15                                                        
cpu MHz         : 2394.000                                                    
cache size      : 12288 KB                                                    
physical id     : 0                                                           
siblings        : 4                                                           
core id         : 0                                                           
cpu cores       : 4                                                           
apicid          : 0                                                           
initial apicid  : 0                                                           
fpu             : yes                                                         
fpu_exception   : yes                                                         
cpuid level     : 11                                                          
wp              : yes                                                         
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov
pat pse36 clflush dts mmx fxsr sse sse2 ss ht syscall nx rdtscp <span class="attention"><span class="ansi-red">lm</span></span> constant_ts
arch_perfmon pebs bts nopl xtopology tsc_reliable nonstop_tsc aperfmperf pni pcl mulqdq vmx ssse3 cx16 sse4_1 sse4_2 x2apic popcnt aes hypervisor lahf_lm ida arat dtherm tpr_shadow vnmi ept vpid</pre> 

<p>While much of the output of the <code>lscpu</code> and the contents of the <code class="console">/proc/cpuinfo</code> file appears to be the same, one benefit to viewing the <code class="console">/proc/cpuinfo</code> file is that the <code class="console">flags</code> of the CPU are displayed.  The <code class="console">flags</code> of a CPU  are a very important component, since they indicate which features the CPU supports and the  capabilities of the CPU.</p>

<p>For example, the output from the previous example contains the flag <code class="console">lm</code> (long mode), indicating that this CPU is 64-bit capable.  There are also <code class="console">flags</code> that indicated if the CPU is capable of supporting virtual machines (the ability to have multiple operating systems on a single computer).</p>


<h2><a name="3">1.2 Motherboards and Buses</a></h2>
<p>The <var>motherboard</var>, or system board, is the main hardware board in the computer through which the CPU, Random Access Memory (RAM) and other components are all connected together.  Some devices are attached directly to the motherboard, while other devices are connected via a <var>bus</var> to the motherboard.</p>

<h2><a name="4">1.2.1 dmidecode</a></h2>
<p>The system board of many computers contains what is known as <var>Basic Input and Output System (BIOS)</var>.  <var>System Management BIOS (SMBIOS)</var> is the standard that defines the data structures and how to communicate information about computer hardware.  The <code>dmidecode</code> command is able to read and display the information from SMBIOS. </p>

<p>For devices directly attached to the motherboard, an administrator can use the <code>dmidecode</code> command to view them.  There is a great deal of information provided by the output of this command. </p> 

<div class="alert alert-info">The examples below provide you with a few ideas of what you can learn from the output of the <code>dmidecode</code> command.  This command is not available within the virtual machine environment of this course.</div>

<p>In the first example, you can see that the BIOS supports booting directly from the CD-ROM.  This is important since operating system installs are often done by booting directly from the install CD:</p>

<pre class="content_terminal"># dmidecode 2.11
SMBIOS 2.4 present.
364 structures occupying 16040 bytes.
Table at 0x000E0010

Handle 0x0000, DMI type 0, 24 bytes
<span class="attention"><span class="ansi-red">BIOS Information</span></span>
	Vendor: Phoenix Technologies LTD
	Version: 6.00
	Release Date: 06/22/2012
	Address: 0xEA0C0
	Runtime Size: 89920 bytes
	ROM Size: 64 kB
	<span class="attention"><span class="ansi-red">Characteristics:</span></span> 
		ISA is supported
		PCI is supported
		PC Card (PCMCIA) is supported
		PNP is supported
		APM is supported
		BIOS is upgradeable
		BIOS shadowing is allowed
		ESCD support is available
		<span class="attention"><span class="ansi-red">Boot from CD is supported</span></span>
<code class="input">--More--</code></pre>

<p>In the next example, you can see that a total of 2048 (about 2GB) of RAM is installed on the system:</p>

<pre class="content_terminal">Socket Designation: RAM socket #0
Bank Connections: None
Current Speed: Unknown
Type: EDO DIMM
<span class="attention"><span class="ansi-red">Installed Size: 2048 MB</span></span> (Single-bank Connection)
Enabled Size: 2048 MB (Single-bank Connection)
Error Status: OK</pre>


<h2><a name="5">1.2.2 Random Access Memory</a></h2>
<p>The motherboard normally has slots where <var>Random Access Memory (RAM)</var> can be connected to the system.  32 bit architecture systems can use up to 4 gigabytes (GB) of RAM, while 64 bit architectures are capable of addressing and using far more RAM.</p>

<p>In some cases, the RAM your system has might not be enough to handle all of the operating system requirements.  Each program needs to store data in RAM and the programs themselves are loaded into RAM when they execute.</p>

<p>To avoid having the system fail due to a lack of RAM, <var>virtual RAM</var> (or <var>swap space</var>) is utilized.  Virtual RAM is hard drive space that is used to temporarily store RAM data when the system is running out of RAM.  Data that is stored in RAM and that has not been used recently is copied on to the hard drive so currently active programs can use the RAM.  If needed, this swapped data can be stored back into RAM at a later time.</p>

<p>To view the amount of RAM in your system, including the virtual RAM, execute the <code>free</code> command.  The <code>free</code> command has a <code>-m</code> option to force the output to be rounded to the nearest megabyte and a <code>-g</code> option to force the output to be rounded to the nearest gigabyte:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> free -m                                                
             total       used       free     shared    buffers     cached     
<span class="attention"><span class="ansi-red">Mem:          1894        356</span></span>       1537          0          25       177     
-/+ buffers/cache:        153       1741                                      
<span class="attention"><span class="ansi-red">Swap:         4063          0</span></span>       4063                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
                         

<p>The output of executing this <code>free</code> command shows that the system it was executed on a system has a total of 1,894 megabytes and is currently using 356 megabytes.</p>

<p>The amount of swap appears to be approximately 4 gigabytes, although none of it appears to be in use.  This makes sense because so much of the physical RAM is free, so there is no need at this time for virtual RAM to be used.</p>


<h2><a name="6">1.2.3 Peripheral Devices</a></h2>
<p>The motherboard has buses that allow for multiple devices to connect to the system, including the Peripheral Component Interconnect (PCI) and Universal Serial Bus (USB).  The motherboard also has connectors for monitors, keyboards and mice. </p>

<p>In order to view all of the devices connected by the PCI bus, execute the <code>lspci</code> command.  The following is a sample output of this command.  As you can see below in the highlighted sections, this system has a VGA controller (a monitor connector), a SCSI storage controller (a type of hard drive) and an Ethernet controller (a network connector):</p>

<div class="alert alert-info">The graphics below provide examples of using the <code>lspci</code> command.  This command is not available within the virtual machine environment of this course.</div>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> lspci                                                   
00:00.0 Host bridge: Intel Corporation 440BX/ZX/DX - 82443BX/ZX/DX Host bridge (rev 01)                                                                      
00:01.0 PCI bridge: Intel Corporation 440BX/ZX/DX - 82443BX/ZX/DX AGP bridge (rev 01)                                                                        
00:07.0 ISA bridge: Intel Corporation 82371AB/EB/MB PIIX4 ISA (rev 08)        
00:07.1 IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)     
00:07.3 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 08)           
00:07.7 System peripheral: VMware Virtual Machine Communication Interface (rev 10)                                                                           
00:0f.0 <span class="attention"><span class="ansi-red">VGA compatible controller</span></span>: VMware SVGA II Adapter     
03:00.0 <span class="attention"><span class="ansi-red">Serial Attached SCSI controller</span></span>: VMware PVSCSI SCSI Controller (rev 02
0b:00.0 <span class="attention"><span class="ansi-red">Ethernet controller</span></span>: VMware VMXNET3 Ethernet Controller (rev 01)</pre>  

<p>Executing the <code>lspci</code> command with the <code>-nn</code> option shows both a numeric identifier for each device, as well as the original text description:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> lspci -nn                                             
00:00.0 Host bridge [0600]: Intel Corporation 440BX/ZX/DX - 82443BX/ZX/DX Host bridge [8086:7190] (rev 01)                                               
00:01.0 PCI bridge [0604]: Intel Corporation 440BX/ZX/DX - 82443BX/ZX/DX AGP bridge [8086:7191] (rev 01)                                                 
00:07.0 ISA bridge [0601]: Intel Corporation 82371AB/EB/MB PIIX4 ISA [8086:7110](rev 08)                                                                 
00:07.1 IDE interface [0101]: Intel Corporation 82371AB/EB/MB PIIX4 IDE [8086:7111] (rev 01)                                                             
00:07.3 Bridge [0680]: Intel Corporation 82371AB/EB/MB PIIX4 ACPI [8086:7113](rev 08)                                                                   
00:07.7 System peripheral [0880]: VMware Virtual Machine Communication Interface [15ad:0740] (rev 10)                                                    
00:0f.0 VGA compatible controller [0300]: VMware SVGA II Adapter [15ad:0405]
03:00.0 Serial Attached SCSI controller [0107]: VMware PVSCSI SCSI Controller
[15ad:07c0] (rev 02)                                                        
0b:00.0 Ethernet controller [0200]: VMware VMXNET3 Ethernet Controller 
<span class="attention"><span class="ansi-red">[15ad:07b0]</span></span> (rev 01)</pre>   

<p>The highlighted section, <code class="console">[15ad:07b0]</code>, is referred to as the <code class="console">[<var>vendor</var>:<var>device</var>]</code> section.</p>
 
<p>Using the <code class="console">[<var>vendor</var>:<var>device</var>]</code> information can be useful for displaying detailed information about a specific device.  By using the <code>-d <var>vendor</var>:<var>device</var></code> option, you can select to view information about just one device.  </p>

<p>You can also view more detailed information by using either the <code>-v</code>, <code>-vv</code> or <code>-vvv</code> option.  The more <code class="console">v</code> characters, the more verbose the output will be.  For example:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> lspci -d 15ad:07b0 -vvv                                
0b:00.0 Ethernet controller: VMware VMXNET3 Ethernet Controller (rev 01)    
        Subsystem: VMware VMXNET3 Ethernet Controller                       
        Physical Slot: 192                                                   
        Control: I/O+ Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Step
ping- SERR- FastB2B- DisINTx+                                                   
        Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast &gt;TAbort- &lt;TAbort- 
&lt;MAbort- &gt;SERR- &lt;PERR- INTx-                                                    
        Latency: 0, Cache Line Size: 32 bytes                                   
        Interrupt: pin A routed to IRQ 19                                       
        Region 0: Memory at fd4fb000 (32-bit, non-prefetchable) [size=4K]       
        Region 1: Memory at fd4fc000 (32-bit, non-prefetchable) [size=4K]       
        Region 2: Memory at fd4fe000 (32-bit, non-prefetchable) [size=8K]       
        Region 3: I/O ports at 5000 [size=16]                                   
        [virtual] Expansion ROM at fd400000 [disabled] [size=64K]               
        Capabilities: &lt;access denied&gt;                                           
        <span class="attention"><span class="ansi-red">Kernel driver in use: vmxnet3</span></span>     
        <span class="attention"><span class="ansi-red">Kernel modules: vmxnet3</span></span>
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                           
       

<p>The <code>lspci</code> command shows detailed information about devices connected to the system via the PCI bus.  This information can be helpful to determine if the device is supported by the system, as indicated by a <var>Kernel driver</var> or <var>Kernel module</var> in use, as shown in the last couple of lines of output above.</p>



<h2><a name="7">1.2.4 Universal Serial Bus Devices</a></h2>
<p>While the PCI bus is used for many internal devices such as sound and network cards, many external devices (or <var>peripherals</var>) are connected to the computer via USB.  Devices connected internally are usually <var>cold-plug</var>, meaning the system must be shut down in order to connect or disconnect a device.  USB devices are <var>hot-plug</var>, meaning they can be connected or disconnected while the system is running.</p>

<div class="alert alert-info">
<strong>Note:</strong> The graphics below provide examples of using the <code>lsusb</code> command.  This command is not available within the virtual machine environment of this course.</div>

<p>To display the devices connected to the system via USB, execute the <code>lsusb</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> lsusb
Bus 001 Device 001: ID 1d6b:0001  Linux Foundation 1.1 root hub
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>The verbose option, <code>-v</code>,  for the <code>lsusb</code> command shows a great amount of detail about each device:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> lsusb -v

Bus 001 Device 001: ID 1d6b:0001  Linux Foundation 1.1 root hub
Couldn’t open device, some information will be missing 
Device Descriptor:
        bLength		       18
	bDescriptorType	 	1
	bcdUSB		     1.10
	bDeviceClass		9 Hub
	bDeviceSubClass		0 Unused
	bDeviceProtocol		0 Full speed (or root) hub
	bMaxPacketSize0	       64
	idVendor	   0x1d6b Linux Foundation
	idProduct	   0x0001 1.1 Linux Foundation
	bcDevice	     2.06
	iManufacturer		3
	iProduct		2
	iSerial			1
	…</pre> 	


<h2><a name="8">1.3 Hardware Abstraction Layer</a></h2>
<p>HAL is the <var>Hardware Abstraction Layer</var>.  The daemon for HAL is <code>hald</code>, a process that gathers information about all devices connected to the system.  When events occur that change the state of the connected devices, such as when a USB device is attached to the system, then <code>hald</code> broadcasts this new information to any processes that have registered to be notified about new events.</p>

<div class="alert alert-info">
<strong>Note:</strong> The graphic below provides an example of using the <code>lshal</code> command.  This command is not available within the virtual machine environment of this course.</div>

<p>The <code>lshal</code> command allows you to view the devices detected by HAL.  This command produces a huge amount of output; the following provides a small sample:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/10.5_1.png"></div>


<h2><a name="9">1.4 Disk Devices</a></h2>
<p><var>Disk devices</var> (AKA, hard drives) may be attached to the system in a number of ways; the controller may be integrated into the motherboard, on a PCI (Peripheral Component Interconnect) card or a USB device.  </p>

<p>Hard drives are divided into <var>partitions</var>.  A partition is a logical division of a hard drive, designed to take a large amount of available storage space and break it up into smaller "chunks".  While it is common on Microsoft Windows to have a single partition for each hard drive, on Linux distributions, multiple partitions per hard drive is common.</p>

<p>Some hard drives make use of a partitioning technology called <strong>Master Boot Record</strong> (MBR) while others make use of a partitioning type called <strong>GUID Partitioning Table</strong> (GPT).  The MBR type of partitioning has been used since the early days of the Personal Computer (PC) and the GPT type has been available since the year 2000. </p>

<p>An old term used to describe an internal hard disk is "fixed disk", as the disk is fixed (not removable).  This term gave rise to several command names: the <code>fdisk</code>, <code>cfdisk</code> and <code>sfdisk</code> commands, which are tools for working with the MBR partitioned disks. </p>

<p>The GPT disks use a newer type of partitioning, which allows the user to divide the disk into more partitions than what MBR supports.  GPT also allows having partitions which can be larger than two terabytes (MBR does not).  The tools for managing GPT disks are named similar to the <code>fdisk</code> counterparts: <code>gdisk</code>, <code>cgdisk</code>, and <code>sgdisk</code>.   </p>

<p>There is also a family of tools that attempts to support both MBR and GPT type disks.  This set of tools includes the <code>parted</code> command and the graphical <code>gparted</code> tool. </p>

<p>Hard drives are associated with file names (called <var>device files</var>) that are stored in the <code class="console">/dev</code> directory.  Different types of hard drives are given slightly different names: <var>hd</var> for IDE (Intelligent Drive Electronics) hard drives and <var>sd</var> for USB, SATA (Serial Advanced Technology Attachment) and SCSI (Small Computer System <strong>Interface</strong>) hard drives.</p>

<p>Each hard drive is assigned a letter, for example, the first IDE hard drive would have a device file name of <code class="console">/dev/hda</code> and the second IDE hard drive would have be associated with the <code class="console">/dev/hdb</code> device file.</p>

<p>Partitions are given unique numbers for each device.  For example, if a USB hard drive had two partitions, they could be associated with the <code class="console">/dev/sda1</code> and <code class="console">/dev/sda2</code> device files.</p>

<p>In the following output, you can see that this system has three <code class="console">sd</code> devices: <code class="console">/dev/sda</code>, <code class="console">/dev/sdb</code> and <code class="console">/dev/sdc</code>.  Also, you can see there are two partitions on the first device (as evidenced by the <code class="console">/dev/sda1</code> and <code class="console">/dev/sda2</code> files) and one partition on the second device (as evidenced by the <code class="console">/dev/sdb1</code> file):</p>

<pre class="content_terminal"><strong><span class="ansi-green">root@localhost</span>:<span class="ansi-blue">~</span>$</strong>  ls /dev/sd*                                               
<strong><span class="ansi-yellow">/dev/sda /dev/sda1  /dev/sda2  /dev/sdb  /dev/sdb1  /dev/sdc</span></strong>                
<strong><span class="ansi-green">root@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>       

<p>In the following example, the <code>fdisk</code> command is used to display partition information on the first <code class="console">sd</code> device.</p>

<div class="alert alert-info">
<strong>Note:</strong>  The following command requires root access</div>

<pre class="content_terminal"><strong><span class="ansi-green">root@localhost</span>:<span class="ansi-blue">~</span>#</strong> fdisk -l /dev/sda                                             
Disk /dev/sda: 21.5 GB, 21474836480 bytes                                       
255 heads, 63 sectors/track, 2610 cylinders, total 41943040 sectors             
Units = sectors of 1 * 512 = 512 bytes                                          
Sector size (logical/physical): 512 bytes / 512 bytes                           
I/O size (minimum/optimal): 512 bytes / 512 bytes                               
Disk identifier: 0x000571a2                                                     
                                                                                
   Device Boot      Start         End      Blocks   Id  System                  
/dev/sda1   *        2048    39845887    19921920   83  Linux                   
/dev/sda2        39847934    41940991     1046529    5  Extended                
/dev/sda5        39847936    41940991     1046528   82  Linux swap / Solaris    
<strong><span class="ansi-green">root@localhost</span>:<span class="ansi-blue">~</span>#</strong></pre>                                                               
                                                                                
                                                                          
                             

<div class="alert alert-info">Creating and modifying partitions is beyond the scope of this course.</div>


<h2><a name="10">1.5 Optical Disks</a></h2>
<p>Optical disks, often referred to as CD-ROMs, DVDs, or Blue-Ray are removable storage media.  While some devices used with optical disks are read-only, others are capable of burning (writing to) disks, when using a writable type of disk.  There are various standards for writable and rewritable disks, such as CD-R, CD+R, DVD+RW, and DVD-RW.  These media standards go beyond the scope of the curriculum.</p>

<p>Where these removable disks are mounted in the file system is an important consideration for a Linux administrator.  Modern distributions often mount the disks under the <code class="console">/media</code> folder, while older distributions typically mount them under the <code class="console">/mnt</code> folder.</p>

<p>Upon mounting, most GUI interfaces will prompt the user to take an action, such as open the contents of the disk in a file browser or start a media program.  When the user is finished using the disk, it is prudent to unmount it using a menu or the <code>eject</code> command.  While pressing the <strong>eject</strong> button will open the disk tray, some programs will not realize that the disk is no longer mounted on the filesystem.</p>

<h2><a name="11">1.6 Video Display Devices</a></h2>
<p>In order to display video (output to the monitor), the computer system must have a video display device (AKA, <var>video card</var>) and a monitor.  Video display devices are often directly attached to the motherboard, although they can also be connected through the PCI bus slots on the motherboard.  </p>

<p>Unfortunately, since the early days of the PC, no video standard has been approved by the major vendors, so each video display device usually requires a proprietary driver provided by the vendor.  Drivers are software programs that allow the operating system to communicate with the device.  </p>

<p>Drivers must be written for the specific operating system, something that is commonly done for Microsoft Windows, but not always for Linux.  Fortunately, the three largest video display vendors all now provide at least some level of Linux support.    </p>

<p>There are two types of video cables commonly used: the analog 15 pin <strong>Video Graphics Array (VGA)</strong> cable and the 29 pin <strong>Digital Visual Interface (DVI)</strong>.</p>

<p>In order for monitors to work properly with video display devices, they must be able to support the same resolution as the video display device.  Normally, the software driving the video display device (commonly the X.org server) will normally be able to automatically detect the maximum resolution that the video display and monitor can both support and set the screen resolution to that value. </p>

<p>Graphical tools are normally provided to change your resolution, as well as the maximum number of colors that can be displayed (known as the <var>color depth</var>) with your Linux distribution.  For distributions using the X.org server, the <code class="console">/etc/X11/xorg.conf</code> file can be used to change resolution, color depth and other settings.</p>


<h2><a name="12">1.7 Managing Devices</a></h2>
<p>In order for a device to be used in Linux, there may be several different kinds of software required.  First of all there is the driver software.  The driver could be compiled as part of the Linux kernel, loaded into the kernel as a module or loaded by a user command or application.  Most devices have the driver either built-in to the kernel or have it loaded into the kernel, as the driver may require the low-level kind of access that the kernel has with devices.</p>

<p>External devices, like scanners and printers, typically have their drivers loaded by an application and these drivers in turn communicate through the device via the kernel through an interface such as USB.</p>

<p>In order to be successful in enabling devices in Linux, it is best to check the Linux distribution to see if the device is certified to work with that distribution.  Commercial distributions like Red Hat and SUSE have web pages dedicated to listing hardware that is certified or approved to work with their software.  </p>

<p>Additional tips on being successful with connecting your devices: avoid brand new or highly specialized devices and check with the vendor of the device to see if they support Linux before making a purchase.</p>

<h2><a name="13">1.8 Power Supplies</a></h2>
<p>Power supplies are the devices that convert alternating current (120v, 240v) into direct current, which the computer uses at various voltages (3.3v, 5v, 12v, etc.).  Power supplies are generally not programmable, however their proper function has a major impact on the rest of the system. </p> 

<p>Although they are not surge suppressors, these devices often protect the computer from fluctuations in voltage coming from the power source.  It is wise for a network administrator to choose a power supply based on quality rather than price, since a failing power supply can result in major destruction to a computer system.</p>
