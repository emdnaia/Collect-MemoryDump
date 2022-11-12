# Collect-MemoryDump
Collect-MemoryDump - Automated Creation of Windows Memory Snapshots for DFIR

Collect-MemoryDump.ps1 is PowerShell script utilized to collect a Memory Snapshot from a live Windows system (in a forensically sound manner).

Features:
* Checks for Hostname and Physical Memory Size before starting memory acquisition
* Checks if you have enough free disk space to save memory dump file
* Collects a Raw Physical Memory Dump w/ DumpIt, Magnet Ram Capture, Belkasoft Live RAM Capturer and WinPMEM
* Collects a Microsoft Crash Dump w/ DumpIt for Comae Beta from Magnet Idea Lab
* Pagefile Collection w/ CyLR - Live Response Collection tool by Alan Orlikoski and Jason Yegge
* Checks for Encrypted Volumes w/ Magnet Forensics Encrypted Disk Detector
* Collects BitLocker Recovery Key
* Checks for installed Endpoint Security Tools (AntiVirus and EDR)
* Enumerates all necessary information from the target host to enrich your DFIR workflow
* Creates a password-protected Secure Archive Container (PW: IncidentResponse)

## First Public Release    
MAGNET Talks - Frankfurt, Germany (July 27, 2022)  
Presentation Title: Modern Digital Forensics and Incident Response Techniques  
https://www.magnetforensics.com/  

## Download  
Download the latest version of **Collect-MemoryDump** from the [Releases](https://github.com/evild3ad/Collect-MemoryDump/releases/latest) section.  

> Note: Collect-MemoryDump does not include all external tools by default.  

You have to download following dependencies:  
* [Belkasoft Live RAM Capturer](https://belkasoft.com/ram-capturer)
* [Comae-Toolkit](https://www.magnetforensics.com/blog/how-to-get-started-with-comae/)
* [MAGNET Encrypted Disk Detector](https://www.magnetforensics.com/resources/encrypted-disk-detector/)
* [MAGNET Ram Capture](https://www.magnetforensics.com/resources/magnet-ram-capture/)

Copy the required files to following file locations:

**Belkasoft Live RAM Capturer**  
`$SCRIPT_DIR\Tools\RamCapturer\x64\msvcp110.dll`  
`$SCRIPT_DIR\Tools\RamCapturer\x64\msvcr110.dll`  
`$SCRIPT_DIR\Tools\RamCapturer\x64\RamCapture64.exe`  
`$SCRIPT_DIR\Tools\RamCapturer\x64\RamCaptureDriver64.sys`  
`$SCRIPT_DIR\Tools\RamCapturer\x86\msvcp110.dll`  
`$SCRIPT_DIR\Tools\RamCapturer\x86\msvcr110.dll`  
`$SCRIPT_DIR\Tools\RamCapturer\x86\RamCapture.exe`  
`$SCRIPT_DIR\Tools\RamCapturer\x86\RamCaptureDriver.sys`  
  
**Comae-Toolkit**  
`$SCRIPT_DIR\Tools\DumpIt\ARM64\DumpIt.exe`  
`$SCRIPT_DIR\Tools\DumpIt\x64\DumpIt.exe`  
`$SCRIPT_DIR\Tools\DumpIt\x86\DumpIt.exe`  
  
**MAGNET Encrypted Disk Detector**  
`$SCRIPT_DIR\Tools\EDD\EDDv310.exe`  

**MAGNET Ram Capture**  
`$SCRIPT_DIR\Tools\MRC\MRCv120.exe`  

Check out: [Wiki: How-to-add-or-update-dependencies](https://github.com/evild3ad/Collect-MemoryDump/wiki/How-to-add-or-update-dependencies)

## Usage  
.\Collect-MemoryDump.ps1 [-Tool] [--Pagefile]

Example 1 - Raw Physical Memory Snapshot  
.\Collect-MemoryDump.ps1 -DumpIt

Example 2 - Microsoft Crash Dump (.zdmp) &#8594; optimized for uploading to [Comae Investigation Platform](https://www.comae.com/)  
.\Collect-MemoryDump.ps1 -Comae  

Note: You can uncompress *.zdmp files generated by DumpIt w/ Z2Dmp (Comae-Toolkit).  

Example 3 - Raw Physical Memory Snapshot and Pagefile Collection  &#8594; [MemProcFS](https://github.com/ufrisk/MemProcFS)  
.\Collect-MemoryDump.ps1 -WinPMEM --Pagefile  
  
![Help-Message](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/01.png)  
**Fig 1:** Help Message  

![AvailableSpace](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/02.png)  
**Fig 2:** Check Available Space

![DumpIt](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/03.png)  
**Fig 3:** Automated Creation of Windows Memory Snapshot w/ DumpIt

![RamCapture](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/04.png)  
**Fig 4:** Automated Creation of Windows Memory Snapshot w/ Magnet RAM Capture

![WinPMEM](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/05.png)  
**Fig 5:** Automated Creation of Windows Memory Snapshot w/ WinPMEM

![Belkasoft](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/06.png)  
**Fig 6:** Automated Creation of Windows Memory Snapshot w/ Belkasoft Live RAM Capturer

![Comae](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/07.png)  
**Fig 7:** Automated Creation of Windows Memory Snapshot w/ DumpIt (Microsoft Crash Dump)

![WinPMEM](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/08.png)  
**Fig 8:** Automated Creation of Windows Memory Snapshot w/ WinPMEM and Pagefile Collection w/ CyLR

![MessageBox](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/09.png)  
**Fig 9:** Message Box

![SecureArchive](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/10.png)  
**Fig 10:** Secure Archive Container (PW: IncidentResponse) and Logfile.txt

![OutputDirectories](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/11.png)  
**Fig 11:** Output Directories

![MemoryDirectories](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/12.png)  
**Fig 12:** Memory Directories (WinPMEM and Pagefile)

![Memory](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/13.png)  
**Fig 13:** Memory Snapshot (in a forensically sound manner)

![Pagefile](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/14.png)  
**Fig 14:** Pagefile Collection

![SystemInfo](https://github.com/evild3ad/Collect-MemoryDump/blob/3aa95e224d0613681d5cd1baaf3e8a22da40bf68/Screenshots/15.png)  
**Fig 15:** Collected System Information

## Dependencies  
7-Zip 22.01 Standalone Console (2022-07-15)  
https://www.7-zip.org/download.html  

Belkasoft Live RAM Capturer (2018-10-22)  
https://belkasoft.com/ram-capturer  

DumpIt 3.6.20220824 (2022-08-24) &#8594; Comae-Toolkit  
https://magnetidealab.com/  
https://beta.comae.tech/   

CyLR 3.0 (2021-02-03)  
https://github.com/orlikoski/CyLR  

Magnet Encrypted Disk Detector v3.1.0 (2022-06-19)  
https://www.magnetforensics.com/resources/encrypted-disk-detector/  
https://support.magnetforensics.com/s/free-tools  

Magnet RAM Capture v1.2.0 (2019-07-24)  
https://www.magnetforensics.com/resources/magnet-ram-capture/  
https://support.magnetforensics.com/s/software-and-downloads?productTag=free-tools  

PsLoggedOn v1.35 (2016-06-29)  
https://docs.microsoft.com/de-de/sysinternals/downloads/psloggedon  

WinPMEM 4.0 RC2 (2020-10-12)  
https://github.com/Velocidex/WinPmem/releases  

## Links
[Belkasoft Live RAM Capturer](https://belkasoft.com/ram-capturer)  
[Comae-Toolkit incl. DumpIt](https://www.magnetforensics.com/blog/how-to-get-started-with-comae/)  
[CyLR - Live Response Collection Tool](https://github.com/orlikoski/CyLR)  
[MAGNET Encrypted Disk Detector](https://www.magnetforensics.com/resources/encrypted-disk-detector/)  
[MAGNET Ram Capture](https://www.magnetforensics.com/resources/magnet-ram-capture/)  
[WinPMEM](https://github.com/Velocidex/WinPmem)  

![Comae](https://www.comae.com/images/MF_Comae_Acquisition_ComaeWebsite2_1200x675.jpg)  
[MAGNET Idea Lab - Apply To Join](https://magnetidealab.com/)
