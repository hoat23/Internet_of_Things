# Industrial Internet of Things
Documentation about me experience connecting a PLC to cloud (OT/IT).

# Achitecture


The Siemens IOT2040 module is the one that allows to link the industrial plant to the cloud, for security reasons it will only send data to the cloud, but it will leave the control of the industrial processes to the internal PLC.

Elasticsearch is a non-relational database, which will store the data sent from the industrial plant. 

<div align="center">
<img src="https://github.com/hoat23/IndustrialInternetOfThings/blob/master/img/architecture_ITOT.png" width="600" align="center"/>
</div>

Kibana or Power BI is used to generate reports, some examples of generated dashboards are:


<div align="center">
<img src="https://github.com/hoat23/IndustrialInternetOfThings/blob/master/img/iiot-canvas-dashboards-blog.gif" width="600" align="center"/>
</div>

# Software

## Node-Red

### Installing in Windows 

* Download and install nodejs from: https://nodejs.org/en/
* Check version using this command: node -v
* Install node-red: sudo npm install -g --unsafe-perm node-red

### Remove from windows
* Run this command: npm cache clean --force
* Uninstall from Programs & Features with the uninstaller.
* Reboot (or you probably can get away with killing all node-related processes from Task Manager). Look for these folders and remove them (and their contents) if any still exist. Depending on the version you installed, UAC settings, and CPU architecture, these may or may not exist:
  * C:\Program Files (x86)\Nodejs
  * C:\Program Files\Nodejs
  * C:\Users\{User}\AppData\Roaming\npm (or %appdata%\npm)
  * C:\Users\{User}\AppData\Roaming\npm-cache (or %appdata%\npm-cache)
  * C:\Users\{User}\.npmrc (and possibly check for that without the . prefix too)
  * C:\Users\{User}\AppData\Local\Temp\npm-*
  * Check your %PATH% environment variable to ensure no references to Nodejs or npm exist.
* If it's still not uninstalled, type where node at the command prompt and you'll see where it resides -- delete that (and probably the parent directory) too.
* Reboot, for good measure.

# Hardware

## Simatic S7-1200

### Some Details

- RAM memory 100 [kB] (work)
- ROM memory 4 [MB]
- Remmant memory 10 [kB]
- E/S local integrated 14E/10S (Discret)
- 2E/2S (Analog)
- Image memory of process 1024 [bytes]
- Labels area 8192 [bytes]
- Ampliation Slots of signals module 8
- Ampliation Slots of comunication module 3
- High counters (HSC) 6
- Pulse generators 4
- PROFINET ports 2 (Ethernet)

## Simatic IOT2000

### Some Details

- MicroSD card is needed for the operating system with a minimun of 2GBytes.
- Connection for the power supply (24 V).
- COM interfaces (RS232/422/485)
- Ethernet interface 10/100 Mbps.
- USB type Micro-B.
- USB type A.

### Hardware and software required

* Engineering Station: Requirements are hardware and operating system (for additional information, see Readme on the TIA Portal Installation DVDs)
* SIMATIC STEP 7 Professional software in TIA Portal V15 or higher
* Software for writing the example image on the SD card, e.g. Win32 Disk Imager
* Software for SSH access, e.g. PuTTY
* Software for SFTP/SCP file transfer, e.g. WinSCP
* SIMATIC IOT2000 controller, e.g. IOT2040 with MicroSD Card and IO-Shield https://support.industry.siemens.com/cs/document/109741799/imagen-ejemplo-para-la-sd-card-de-un-simatic-iot2020-iot2040?dti=0&lc=es-AR.
* Ethernet connection between the engineering station and controller
* SIMATIC IOT2000EDU Software Controller executable on IOT2020 and IOT2040


# Reference

- Siemens-IOT2000 configuration: https://www.automation.siemens.com/sce-static/learning-training-documents/tia-portal/hw-config-iot2000/sce-014-101-hardware-configuration-iot2000edu-r1806-en.pdf
- https://www.elastic.co/es/blog/industrial-internet-of-things-iiot-with-the-elastic-stack
- https://github.com/apache/plc4x
