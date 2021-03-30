![Main workflow](https://github.com/cs481-ekh/s21-team-blue/workflows/Build/badge.svg)


# PiRate
BSU CS481 Capstone Project


### Access
To access the webpage, go to http://192.168.0.202:3000 in any web browser on any device on your LAN, and you should see the homepage.

### DNSmasq Setup
Update the RaspberryPi before moving forward with these terminal commands:

`sudo apt-get update`
`sudo apt-get upgrade`

Install DNSmasq:

`sudo apt install dnsmasq`

Drag and drop (or copy over) the dnsmasq.conf file in /backend from the repository into: /etc on the RaspberryPi
Restart dnsmasq:

`sudo systemctl restart dnsmasq` (if this doesn't work do a: sudo reboot)

Check that DNSmasq is installed and running with:

`sudo systemctl status dnsmasq`
You should get a large print out of information in the terminal with a little green line that should say active (running).

### Install DNSutils for future caching of static addresses:

`sudo apt install dnsutils`

Check that DNSutils is working by running:

`dig <any website here> @localhost`
  
You should get another large printout of information with the response time being around 50-100ms if you pinged google.com
Running the command again you should see that the response time is now at just about 0ms.

### Using auto-start script for program

First: Move the `dhcpcd.conf` file into the /etc/ folder on the Pi, overwrite the old one in the folder

Second: Move the `.bashrc` file into the /home/pi/ folder on the Pi, overwrite the old one in the folder

Third: Move the `serverscript.sh` file into /home/pi/s21-team-blue/backend folder on the Pi, this needs to be the path for the script/project otherwise things break

Fourth: That's it, now whenever you login, boot up the terminal, or ssh into the Pi it should automatically run the script and make sure everything is compiled for the program

Optional: You can edit your hosts file to overwrite the IP for the Pi/Server to just autoconnect on a name like PiRate.net, location is: /etc/hosts for Mac/Linux/OsX, C:/windows/system32/drivers/etc/hosts for Windows.

(Still working on checks to see if all it needs to do is run and not compile and build everything)
