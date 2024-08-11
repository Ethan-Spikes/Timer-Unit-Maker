#!/bin/bash

#the previous timer unit maker would fill in variables and make the documents for you.

#I want this one to make a document and format it for me, then tell me how to fill out the document

#I want it to fill out the .timer file and the .service file

#I want it to check the file after I edit it

#I want there to be seamless transitions between executing the script, naming the file, editing the file, checking the file, and moving on to the next file or timer unit

#I want it to check for root first of course

#version: 2.0

path2timers=/etc/systemd/system/
name=''




Root_Check() { #good

	user=$(whoami)
	if [ $user != root ]; then
		echo 'Permission denied.'
		echo ' '
		exit
	fi

}

Name_File() {

	echo "What do you want the name of your timer to be?"
	read name
	service_file=$path2timers$name.service
	timer_file=$path2timers$name.timer
	verify=$path2timers$name.*

}

Generate_Service() {

	echo "[Unit]
Description=User made timer

[Service]
ExecStart="" #full path to executed script"  > $service_file #to make service file

}
Edit_Service() {

	sudo vim $service_file

}

Generate_Timer() {

	echo "[Unit]
Description=User made timer

[Timer]
OnBootSec=1min
OnUnitActiveSec=1min
Unit=$name.service

[Install]
WantedBy=multi-user.target" > $timer_file #to make timer file

}

Edit_Timer() {

	sudo vim $timer_file

}
Check_Timer() {

	sudo systemd-analyze verify $verify #to verify timer unit formatted correctly

}

Enable_Timer_Unit() {

	sudo systemctl start $name.timer #to activate timer for current session only

	sudo systemctl enable $name.timer #to enable timer to activate on boot

}

Main() {

	Root_Check
	Name_File
	Generate_Service
	Edit_Service
	Generate_Timer
	Edit_Timer
	Check_Timer
	Enable_Timer_Unit
	
	echo "Script complete"
	exit
	
}

Main
