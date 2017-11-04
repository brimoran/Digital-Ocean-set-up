# Digital-Ocean-set-up

How I set up Digital Ocean for R, R Studio and Shiny, primarily to see if I could use on a Chromebook but I will probably roll-out to work for others...

## 1. Create Ubuntu server

Head to https://www.digitalocean.com/ and create and account.

Create a droplet:

- Ubuntu 16.04
- $10/mo option is fine
- 1GB/1CPU
- 30GB disk

### Generate SSH keys on Mac with:

`ssh-keygen -t rsa`

Password protected with strong password

Copy two files that are output over to Chromebook.  Paste public key into box on Digital Ocean and then create the server.

Login to server using SSH - on Chromebook use Secure Shell app (excellent!) and import private ssh key as part of this.

## 2. Create users

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04

`adduser brian`

`usermod -aG sudo brian`

That's enough as root for now:

`su brian`

## 3. Install R

https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-16-04-2

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9`

`sudo apt-get update`

`sudo apt-get install r-base`

## 4. Install some standard R packages

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

Exit R:

`quit()`

## 5. Install RServer

https://www.digitalocean.com/community/tutorials/how-to-set-up-rstudio-on-an-ubuntu-cloud-server

https://www.rstudio.com/products/shiny/download-server/

`sudo apt-get install libapparmor1 gdebi-core`

`sudo wget https://download2.rstudio.org/rstudio-server-1.1.383-amd64.deb`

`sudo gdebi rstudio-server-1.1.383-amd64.deb`

create another user for rstudio (if need be):

`sudo adduser rstudio`

Check its up and running by accessing at IP address of Droplet (you'll find this on the dashboard in Digital Ocean) on port 8787:

http://DIGITALOCEANDROPLETIPADDRESSHERE:8787/auth-sign-in

Configure sweave settings in Global Options in R to select knitr and XeLaTeX.

## 6. Set up shiny server

https://www.digitalocean.com/community/tutorials/how-to-set-up-shiny-server-on-ubuntu-16-04

https://deanattali.com/2015/05/09/setup-rstudio-shiny-server-digital-ocean/#install-shiny

`sudo wget https://download3.rstudio.org/ubuntu-12.04/x86_64/shiny-server-1.5.5.872-amd64.deb`

`sudo md5sum shiny-server-1.5.5.872-amd64.deb`

`sudo gdebi shiny-server-1.5.5.872-amd64.deb`

Check it's running: `sudo netstat -plunt | grep -i shiny`

Change firewall to allow port 3838: `sudo ufw allow 3838`

Test at port 3838:

http://DIGITALOCEANDROPLETIPADDRESSHERE:3838/

## 7. Install LaTeX

For automated corporate reports in knitr:

`sudo apt-get install texlive-full`

Make a cup of tea.

## 8. Test SFTP

Cyberduck works on Mac ok.

**Note: Files seem to become read only after SFTP (maybe because I am doing something wrong... maybe SFTPing as root but in R Studio as brian)**

To correct navigate to the folder as the user who needs access (example brian):

If currntly root:

`su brian`

And then:

`sudo chmod 777 * -R`

All files and sub folders will be corrected.

## 9. General server admin

To get updates in Ubuntu:

`sudo apt-get upgrade`

To shut down the server from command line (advised to do so on Digital Ocean website rather than just pressing the off button):

`sudo shutdown -h now`

Take a snapshot to save money :) or to share set up.

Cost is only 5 cents per GB per month.  Snapshot size is c. 10 GB so only c. 50 cents or so to keep per month.

And hen to restore...

In Digital Ocean:

- Navigate to images
- Click on the more down arrow on the snapshot
- Select create droplet
- Remember to tick the box for the ssh key again
- Takes 30 seconds or so.
