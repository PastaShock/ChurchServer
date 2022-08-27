Notes on Setting up the HP Proliant dl360 with HP p420i RAID controller

George 1/23/21
I have set up and got many of the necessary system components operational. I have set up a work environment in TMUX to monitor incoming connections as well as active processes.
I still need to find out why I can't see the two 600GB drives as regular sdx or sgx drives in /dev/
	I can see them using sudo smartctl -a /dev/sda -d cciss,2 and cciss,3 as they are the third and fourth physical drives in the system.
	fdisk -l doesn't show those drives along with the second 146GB drive which I believe is cciss,1.
	I have some HP specific software I downloaded from the HP specific repos that I added.
	Based on HP's hpssacli ctrl all show config I can see that we have one p420i on slot 0
	with all drives showing. the two 600GB drives are stting unassigned. I likely need to 
	use one of the hpssacli commands to assign them and set them up as a RAID array

George 1/24/21
I have created the raid array and the partition.
the partition is /dev/sdb and is formatted ext4.
The partition is mounted to /share and has been chmod 775 and then chmod ugo+wx for read/write permissions for all users
the next step is to create a samba share in the /share directory for local network availablility.
The samba share is running and set up. It uses user accounts and passwords that are manually set up.
To access the server from windows you can type in the address bar '\\ubuntu-server\media' and log in using system creds.
all that is left to get the barebones system operational is the front-end hosting and FTP hosting.	

George 9/26/22
The server has been down for the most part, but i have no issues connecting to the smb share when the server is powered up. 
I got Oles to figure out the VPN for the UI USG, but I am in a different subnet when I connect, and I'm having issues connecting to the ILO interface.
When I'm on the LOVpublic network, 192.168.1.0 subnet, I can connect to the ILO at 192.168.1.194:443 and the server via ssh at 192.168.1.21.
Oles or I need to figure out how to connect to the ILO via VPN. Leaving the port exposed is not safe.
