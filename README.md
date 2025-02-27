![Main workflow](https://github.com/7CLewis/PiRate/workflows/Build/badge.svg)


# PiRate
PiRate is standalone security software designed to allow researchers, engineers, and pentesters the ability to use a fully customizable vulnerability testing framework. The software is designed to come fully configured on a Raspberry Pi 3 device, so that users will simply be able to connect the Pi to their PC, turn the Pi on, and run tests. The instructions below are for anyone who would like to manually install and configure the PiRate software on their own Raspberry Pi device.

### Dependencies

`sudo apt-get install python3-nmap`

## Running Angular App with Node Express
### Installation
To run the Angular App with the Node Express Server, you need to install NodeJS, NPM, and the Angular CLI (Command-Line Interface). [Here](https://nodejs.org/en/) is a link to download NodeJS, which also installs npm. 

Once NodeJS and npm are installed on your machine, open a terminal and run the following command (in any directory):
`npm install -g @angular/cli`

### Compiling the Angular App
Now that all 3 components are download, open a terminal and navigate to `[this_project_root]/web-app`. From this directory, execute the following 2 commands:

`npm ci` (Installs the required modules for the program)

`npm run pro-build` (Builds the production version of the Angular app, and stores the files in `./backend/dist/web-app`)

### Running the Node Express Server
To start the Node Express Server, navigate to `./backend/`. You should now see a directory called `/dist/web-app/` with the web app's production files that were just generated. From this directory, execute the following 2 commands:

`npm ci` (Installs the required modules for the program)
`npm start` (Starts the Node Express Server)

### Access
To access the webpage, go to http://localhost:3000 in any web browser, and you should see the homepage.

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

### Plugin API

To create a test plugin, all you need to do is create a python class for it. Create a python file called `test-name.py`
where `test-name` is the name of your plugin e.g. 'Eternal Blue'. In this python file you'll create a class called
`test-name`. This class needs four things.

  1. A field called `name` which is a string containing the name of the test.
  2. A field called `desc` which is a short description of the test.
  3. A field called `oses` which is a list of Operating Systems the test supports.
  4. A method called `scan()` which accepts a single argument, the host_ip to scan in the form of a string, and returns
     a two-tuple containing the status of the result (success or failure) and a longform description of the result.

After you've created this python file, place it in the `controller/tests` directory of the Pirate installation. The 
controller will automatically detect it and you'll be able to select and run it through the web API.
