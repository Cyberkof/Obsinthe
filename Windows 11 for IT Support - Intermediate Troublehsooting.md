Working with the Reliability Monitor
Control Panel -> System and Security -> System and Maintenance -> Reliability Monitor
- test the reliability of a system

Using the Steps Recorder
-start -> all apps -> windows tool -> steps recorder
- for each step there is add comment button
- scroll down more for additional detail button

Using windows security console
start - settings -0 privacy and security - windows security
- app & browser control

event viewer
start - all apps - event viewer
- application logs
- security logs
- set up logs
- system logs
- forwarded events

informational entries, warnings, errors
- double click on event and it will provide details

Remote Troubleshooting
using remote assistance
* quick assist*
* search remote assistance -> allow remote assistance -> (within control panel allow remote assistance)
For allowing remote assistance
- search -> remote assistance -> invite someone to connect to your PC or offer for help -> save invitation as a file -> enter code for helping PC password -> allow remote connection -> click on request control on top right control -> allow to share control of machine

Configuring the RDP client
Remote Desktop Connection
- search - windows tools - > double click on remote desktop connection -> enter computer IP address
- bottom left click show options allows you to save an RDP connection
- display allows for resolution, configuration, colors, slower connection best to opt for lower resolution
- experience tab helps weith connection speed
- advanced tab allows you to ocnfigure server atuthentication

Establishing a remote desktop session
- right click start ->  system -> advanced system settings - > remote tab -> down at bottom remote tesktop click allow remote connections to this computer -> allow connections only from compyuter runnign remote destkop with network level authentitcation -> select users -> add user
add an execption for windows firewal
- control panel -> system and security -> windows defender firewall allow apps to communication through windows defender firewall ->

Questions. 
What firewall port must ge open in ordfer to use an RDP session?
- 3389

Even atfeter connection, a helper cannot control the remot e system without specific permission beign given.
- true

Wghich of the tabs within the Windows Remote Desktop Connection tool allows you to save the RDP configuration to an RDP file?
- General

Trouble SHooting System Services

Chekcing ro stopped services

righ clik start button - click run - ltype services.msc - opens up service control manager

for specific service
right click on the service -> properties - check the general description -> startup type -> start/stop -> ok

common causes of service failure
right clic on the service -> properties -> log on tab ->

- one potential cause i s that the underlying executable fiel is either missing or damaged
- another cause is failed depency
	- Dependency tab

Using Powershell to start failed services
- terminal
- type get-service
- type get-service BITS 
- type get-services BITS | Select-Object *
- type Get-Service | Where-Object {$_.StartType -eq 'Automatic'}
- Get-Service | Where-Object {$_.StartType -eq 'Automatic' -And $_._Status -eq 'Stopped'}
- Start-Service BITS

Trouble Shooting Devices
Using Device Manager to find failed devices
- right click start -> device manager
- select device - > right c lick properties
Disabling failed devices
- right click start -> device manager
- locate failing device -> expand category -> right click on device -> click disable device
Updating device drivers
- right click start -> device manager -> right click device -> update driver -> search automatically for drivers


The Windows Command Line

Addressing access-denied issues
- windows tool -> command prompt -> riught lcick run as administartor
- - type sfc -> enter

Using Windows terminal
- search terminal
- right click tabs - change color/rename
- Get-ChildItem
- right click on tab -> find

System Integrity

Running chkdsk
- windows tools - command prompt -> run as administrator
- chkdsk c:
- chkdsk c: /f -> y -> enter

usign the system file checker
- sfc /scannow

restoring a system's health
command promt- Run as administrator
- dism.exe /online /cleanup-image /restorehealth


Performance Troubleshooting
Using the task amnager for performance assessments
- right click start button -> run - >taskmgr
- tsk manager -> more icon -> resource monitor
- click on memory tab
using the   perfomrance monitor
- windows tools -> eprfomance monmitor -> performance montior tab

Using Pweroshesll to track rwesdource usage
- Get-Process
- Get-Process | Sort-Object -Property CPU
- Get-Process | Sort-Object -Property CPU -Descending
- Get-Process | Sort-Object -Property CPU -Descending | Select- Object -First 5
- Get-Process | Sort-Object -Property CPU -Descending | Select-Object Name, CPU, WS -First 5