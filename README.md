# AASD15A-Servo-Controller-for-Motion-Simrigs

checkout our shop at motion4sim.com for more information

Motion4Sim M4S Controller Firmware

Version v3.30

- factory reset required after flashing!!!
- added Actuator Input Data matrix, 
- so you can use SRS or Simtools Actuator order without reconnecting cables
- edit via Handheld in Actuators menu or use Dashboard in Filter tab
- only for direct mode!
- in position mode you will need still clockwise actuator connection starting with 1 at front left actuator 
- fixed shutdown function torque recognition and not rebooting
- fixed service menu torque recognition

Version 3.29

- added separate fifo for usb motion and data
- in principle, both USB ports can be operated in parallel
  need to test what happens when Motion data is received on both ports
  so be carefull using it
- changed debouncing for killswitch and online switch
- improvement of serial pattern detection
- added SimHub  support

Version 3.28 

- added message crc datachecks to all communication 
- the end chars 0x0a 0x0d are replaced with crc16 checksumm
- still back compatible to 0x0a 0x0d if send to recieve but sends only with crc so older dashboard will not recieve data
- update to Dashboard Version 3.28
- works only full with Dashboard >=v3.28 because crc checks
- fixed motionusb port problems


Version 3.26

- just for testing fw updates with flypt

Version 3.25 fix1

- fixed  short brake release impulse when startup with EM Button engaged
- fixed  online speed set to 50khz only in some conditions


Version 3.25 official

- hardware pulsing is stable now ,just enable, works same, read advice in dashboard
- small change to break release delaytiming
- new spike algorithm is now implemented 
	-> adjust spikwindow for setup from smaller value to higher
	-> read also fw3.15 release note down this list
- old spike is emalp+spike2 option now in filter setting
- changed lowspeed in factory settings
- changed breakdelay to 100ms in factory settings
- @dureiken changed factory setting motionxp for spike to spike2 and cal/lowspeed settings
- no changes to dashboard made same version 

Version 3.24 

- a lot of changes test your rig behaviour before pratical use!!
- added new EM Button debouncing with Software and Hardware
- added prompt ">" for Setup and Configuration values
- fixed flashport at startup wrong config  data transmission 
- added transition to standby with special triple emalp filtering, 
	-> also into motion from standby uses now this transition
	-> setup transition speed for this its in seconds
- maybe for better transition adjust the low speed to 5000*10hz in setup (Speed from/to Standby Position)
	-> this also changes auto homeing speed for belt
- hardcoded service speed set to 1000x10hz before was low speed too
- extra01 pin is now low at startup in case for brake nc use
- controller firmware reset, now only possible in save rig states
- dashboard controls "transmit"  accepted only when restart/offline phase possible
- fixing service menu emergency issues
- changed doubleclick recognition speed a little bit faster 
- fixed belt spike2 problem (no spike calculation for belt)
- removed doubleclick feature in the menu

Version 3.20

-  removed motionsystem introduced in 3.10 -> done by Dashboard now
-  added support for flash-usb port for motion and dashboard use
-> i recommend this port now for all operations
-  added hw pulsing support for pcb version from 1.09 (could double resolution)
-  added option for inoffz. srs supp with native usbport mod
-  added support for new motioncueingsystem included in dashboard now
-  this fw operates only with dashboard version 3.20 
-  added realtime belt retreat modification 
-  added adjust.servobrake switching delay


Version 3.15 

- lcd init problems fixed everything else seems to emi related
- lcd only comes to garbled char when workhour timer is active (normaly deactivated)
- option in menu -> setup -> Mastergain enabl : if set to off Mastergain is fixed on main screen
- long press (>3s) of encoder button does a lcd screen init
- double click feature for encoder button
	-> fast double click switches main screen from 
		gain"100%" -> "Sp Win" Spike Window -> "Belt" retreat -> "Filter" Emalp value back to gain
	-> you can change value with encoder turning left or right
	-> values were not saved to eeprom
	-> for saving go to menu "Save and return"
	-> with double click you can also leave any menu back to main screen with no saving
- new Spike Filter design
	
	defined with 3 Values.
	
		Menu -> Filter 	-> Spike Filter 	
				-> Spike Window
				-> Sp.Filter smooth


	-> Spike Window:  from 1...400% (or more) 100%  is 1/4 actuator range in pulses
    	 	-this means if pulse input is more than say 100% (1/4 of actuator stroke) Spike is detected
		-pulsestrain is cut/limited to Spike window size pulsecount
	-> Spike Filter: 
 		- after Spike detection the Emalp(normal Filter) raises every frame(2ms) Spikestrength value is lowpass over raising emalp	
		-> this means lower value faster growing Filter (after spike slower return to normal motion)
		-> higher value ,lower growing filter ( after spike faster return to normal motion)
	-> Sp. Filter smooth:  when spike is finished (pulsetrain smaller as Spike Window)
		-> dyn Emalp filter decreases(2ms) with  Sp.Filter smooth ( Emalp over decr. value) 
		-> this means higher value slower decrease and slower return to normal motion
		-> and vice versa
	
	//for me follwing values have worked
	//Spikestrength = 20 to 80  (higher means more smooth in spike)
	//Spikewindow from 10%  for racing 20-40 % for flying  (higher means later spike detection)
	//Spike smooth 2-10   (higher means longer of spike smoothing ,do not use 1 never ending spike) 


Version 3.11 release

continueing lcd fixes
watch also 3.10 notice
- long press (5s) of encoder button does a lcd screen init

Version 3.10 release

Pay attention Motioncueingsystem is W.I.P. start with low scale first
Factory Reset is important for Motioncueingsystem to work
please install also latest Dashboard v3.10 for full use of Motioncueingsystem

-added full scripting motioncueing and filtersystem
-added autotuning system to scale the motioncueing profiles
-added system for storing motionprofiles in flash
-added doubleclick feautre for inputsystem
-added function to boot intobootloader in setup menu
-added support for new pcbversion 1.09 hardwaretimers

Version 2.23 release

- added dashboard support for belt configuration
- added working hour meter reset support ( press user button > 15 seconds for reset)
- lcd working now with no problems
- this fw support only until pcb v. 1.08
- last fw for this boards
- some code improvements

Version 2.19 release

- added belt actuator support
- added new emergency mode "keep online"
- added extra01 function send timer signal
- added sineloop for testing actuators
- added working hour meter
- factory reset needed from fw 2.11
- fixed most lcd problems but still not all yet :(
- better code perfomance
- cleanup 

Version 2.11

- added  support for SFX 3 actor  System in position mode
- no factory reset needed
- fixed homing issue with linear systems other then 6dof
- lcd garbage issue still exist _ screen reinit time now is shorter

Version 2.01

-complete rewrite of the motion engine
-now best motion ever 
-some smaler bugfixes (Service Menu)
-led blinking in some states
-code cleanup
-rewrite of serial port code
-rewrite of lcd display routines
-no srs support :)
Attention - for older first series boards there is also necessary to update the bootloader, contact me for this !!!


Version 1.60 Factory reset needed !! storage  changed

- included SFX RIG types in kinematics calculation BETA!
- activatet Native USB Port to work with Dashboard APP and Motiondata ->still not good as it should use MotionData port
- improved interface to Dashboard App
- load and Install also new Dashboard App


Version 1.54

- serial data interface  transfer extended for new Dashboard App
- works only with new DasBoard App correct,please update
- always do a factory reset after flash
- some bugfixes, linear factory reset, and 6dof float mode
- fixed srs

Version 1.51

Attention:	Factory reset needed !! storage  changed

- rewrite of service actuator moving functions
- usersettings moved to internal MCU flash storage  -> factory reset needed ! 
- factory reset possible with on board button (press 4 seconds for rotating Act setting and 8 seconds for linear Act settings)  
- stability of usb for apps improved
- update also to latest apps


Version 1.47

Attention: 	- eeprom data changed  _ after flashing do factory reset !

- fixed some servo7 bugs
- fixed linear actuator safety bug (safety >pitch)
- added function for servobrakes WIP
- added new transition to motion
- added adjustable time for transition to motion
- added offset for linear actuators
- added adjustable Online Position
- added adjustable Maximum Gain
- better actuator check function (also while homing)
- added shutdown function (drives actuators down to homing point and powers servos off; turn left in menu ) 
- smaller changes in menu texts
- some value checks added
- most new settings only from handheld adjustable actually

thanks to Dirty for testing

Version 1.42

Attention: 	- eeprom data changed  _ after flashing do factory reset !
		- save your settings to paper!! remote App changed data completely
		- install new Handheld app version
		- install new config app version

- added fully support for servo 7 ( remove some resistors on board before use)
- added support for infinite actuators
- bug fix of version 1.41_fix1 display stuck after flash
- some bugs fixed in srs autoconnect
- smaller changes in menu texts
- fixed bugs with remote handheld app
- changed actuator check function 


Version 1.41

-added interface for remote handheld app at native usb port
  (u have to wire the native usb port)
- minor code changes
- spikefilter led keeps on bug fixed
- transmit data from app doesnt reboot  fixed
- memory protection feauture inkluded
- updated bootloader for automatic software bootloadermode ( board delivered later as 062821)

Version 1.30

- added few remote commands for remote app testing features
- now fw has support for Sim Racing Studio in amcsd15a mode
- changed filter timing 
- minor bugfixes and code changes

Version 1.20


Attention: 	- eeprom data changed  _ after flashing do factory reset !
		- save your settings to paper remote App changed data completely

- complete new actuator settings, each actuator can be different , special for linear rigs seatmover
- keys and buttons using interrupts now
- native usb port on same70 board only for fw update
- remote app works now only with motion data port on breakout port
- remote app new version release for this firmware
- lcd fps setting now working
- new option for encoder direction

Version 1.19

- new data mode for floating point values from flypt mover
- changed some  motion cueing calculation for linear actuators
- improved 3d calculation to support center of rotation 
- fixed emergency button problems
- factory reset available for linear and rotating actuators
- remote app some minor changes
- fixed bug loading factory data when using remote app before calibrating


Version 1.18

- remote app expanded ,for now function only to native usb port
- native usb port and ftdi usb port working together now
- native usb port not for motiondata due to usb stack problems with pulse engine
- some changes to onboard motion cueing  now xyz koordsystem works like flypt
- motion cueing with linear 6dof rig works thanks to [GER]Basti-Discord

Version 1.17 Beta

- new usb remote configuration interface
- simple gui app  on github
- please check plattform after transmit configuration data controller will reset


Version  1.16 Beta

- change LCD - Display Init
- usb cdc code for target usb port (near ethernet connector) support asyn. cdc transfer
- enter bootloader via emergency-bt online-sw encoder-bt pressed and power on
- modified calculation of rotat. and linear inverse kinematics


W.I.P.
