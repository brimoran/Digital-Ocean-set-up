# Digital-Ocean-set-up

How I set up Digital Ocean for R, R Studio and Shiny, primarily to see if I could use on a stock Chromebook but I will probably roll-out to work for others...

## 1. Create Ubuntu server

Head to https://www.digitalocean.com/ and create an account.

Create a droplet:

- Ubuntu 16.04
- $10/mo option is fine
- 1GB/1CPU
- 30GB disk

### Generate SSH keys on Mac with:

`ssh-keygen -t rsa`

(I think I could have done this on the Chromebook with the Termux android app but hey, the Mac was just sitting there.)

When prompted, password protect private key with a strong password.

Copy two files that are output over to Chromebook.  Paste public key into box on Digital Ocean and then follow the simple steps on DO to create the server.

Login to server using SSH - on Chromebook use Secure Shell app (excellent!) and import private ssh key as part of this. **Don't forget to `exit` at the end of a session.**

## 2. Create users

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04

`adduser brian`

`usermod -aG sudo brian`

That's enough as root for now:

`su brian`

## 3. Install stuff that R packages need

`sudo apt-get install curl libcurl4-openssl-dev libxml2-dev libssl-dev libgdal1-dev libproj-dev r-cran-rgl`

## 4. Install R

https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-16-04-2

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9`

`sudo apt-get update`

`sudo apt-get install r-base`

For RGL to install:
`sudo apt-get install xorg'

`sudo apt-get install libx11-dev'

`sudo apt-get install libglu1-mesa-dev' 


## 5. Install some standard R packages

Doing with admin powers so they will be available to all users:

`sudo -i R`

Now inside R:

`install.packages('ggplot2')`

And repeat for all of these favourite packages: 

- knitr

- ggthemes

- scales

- ggmap

- plotly

- htmlwidgets

- rstudioapi

- plyr

- dplyr

- ggfortify

- leaflet

- leaflet.extras

- rgdal

- forecast

- prophet

- shiny

- treemapify

- data.table

- dbscan

- survival

- MASS

- googleVis

- rmarkdown

- reshape2

- flexdashboard

- highcharter

- arules

- devtools

- tidyverse

- maptools

- highcharter

- treemap

- networkD3

- visNetwork

- DiagrammeR

Exit R:

`quit()`

## 6. Install RServer

https://www.digitalocean.com/community/tutorials/how-to-set-up-rstudio-on-an-ubuntu-cloud-server

https://www.rstudio.com/products/shiny/download-server/

`sudo apt-get install libapparmor1 gdebi-core`

`sudo wget https://download2.rstudio.org/rstudio-server-1.1.383-amd64.deb`

`sudo gdebi rstudio-server-1.1.383-amd64.deb`

create another user for rstudio (if need be):

`sudo adduser rstudio`

Check it’s up and running by accessing at IP address of Droplet (you'll find this on the dashboard in Digital Ocean) on port 8787:

http://DIGITALOCEANDROPLETIPADDRESSHERE:8787/auth-sign-in

Configure sweave settings in Global Options in RStudio GUI to select knitr and XeLaTeX.

## 7. Set up shiny server

https://www.digitalocean.com/community/tutorials/how-to-set-up-shiny-server-on-ubuntu-16-04

https://deanattali.com/2015/05/09/setup-rstudio-shiny-server-digital-ocean/#install-shiny

`sudo wget https://download3.rstudio.org/ubuntu-12.04/x86_64/shiny-server-1.5.5.872-amd64.deb`

`sudo md5sum shiny-server-1.5.5.872-amd64.deb`

`sudo gdebi shiny-server-1.5.5.872-amd64.deb`

Check it's running: `sudo netstat -plunt | grep -i shiny`

Change firewall to allow port 3838: `sudo ufw allow 3838`

Test at port 3838:

http://DIGITALOCEANDROPLETIPADDRESSHERE:3838/

## 8. Install LaTeX

For automated corporate reports in knitr:

`sudo apt-get install texlive-full`

Make a cup of tea.

## 9. Install Pandoc

To be able to do most of my writing in Markdown but easily share in other formats:

`sudo apt-get install pandoc`

## 10. Test SFTP

If you just need to access one folder, 
on Chromebook ‘Add new services’ in the Files app to mount the folder using Secure Shell. Just use your existing connection to the server but give the New Connection a new name and don’t forget to add the port as 22.

For more flexibility to navigate around folders, Cyberduck works on Mac ok as does FTPManager on iOS.

**Note: When I used Cyberduck or FTPManager, the permissions on uploaded files became borked (because I am SFTPing as root but accessing R Studio as a normal user)**

To correct navigate to the folder and then:

Check file ownership and permissions with:

`ls -la`

Change with:

`sudo chmod 777 * -R`

Alternatively:

`sudo chmod 777 -R /PATHTOYOURSFTPFOLDER`

All files and sub folders in PATHTOYOURSFTPFOLDER will be given full read / write access.

**Be careful with this, it gives ANY user the right to access and delete files which generally you would not want to do.  The -R stands for recursive so it will apply to any sub folders from where the command is run.  Make sure you only run the command on the files you intended to!**

## 11. Install Mosh (optional)

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-mosh-on-a-vps

For more persistent connections:

`sudo apt-get install python-software-properties`

`sudo add-apt-repository ppa:keithw/mosh`

`sudo apt-get update`

`sudo apt-get install mosh`

## 12. General server admin

To get updates in Ubuntu:

`sudo apt-get upgrade`

To shut down the server from command line (advised to do so on Digital Ocean website rather than just pressing the off button):

`sudo shutdown -h now`

Take a snapshot to save money :) or to share set up.

Cost is only 5 cents per GB per month.  Snapshot size is c. 10 GB so only c. 50 cents or so to keep per month.

And then to restore...

In Digital Ocean:

- Navigate to images
- Click on the more down arrow on the snapshot
- Select create droplet
- Remember to tick the box for the ssh key again
- Takes 30 seconds or so.
