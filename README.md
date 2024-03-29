# LaTeX

Needs perl so:

``aptitude install perl perl-doc``

Download latest texlive:

``wget "http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz"``

``tar -xzf install-tl-unx.tar.gz``

``cd`` into directory and:

``sudo ./install-tl``

press I to install

Takes hours...

Test with

``PATH=/usr/local/texlive/2020/bin/x86_64-linux:$PATH``

and then:
``pdflatex --version``

If all ok make the path permanent with:

``vim .bashrc``

and add:

``PATH=/usr/local/texlive/2020/bin/x86_64-linux:$PATH``

``MANPATH=/usr/local/texlive/2020/texmf-dist/doc/man``

``INFOPATH=/usr/local/texlive/2019/texmf-dist/doc/info``

Save and exit Vim.

Then so that LaTeX is available to other users on the server:

``vim /etc/bash.bashrc``

and add the same lines here.

# R

``sudo apt-get update``

``sudo R``

``install.packages(c("ggplot2","tidyverse","knitr","ggthemes","scales","ggmap","plotly","ggfortify","leaflet","leaflet.extras","rgdal","forecast","treemapify","dbscan","survival","googleVis","rmarkdown","flexdashboard","highcharter","devtools","maptools","mapview","treemap","networkD3","visNetwork","DiagrammeR","DT","ggcorrplot", "Hmisc", "anomalize", "fpp2", "h2o", "sweep", "timetk", "xgboost", "prophet","survminer","ggwordcloud", "ggsn", "formattable", "IMD", "car", "maps", "this.path", "triangle", "waterfalls") , repo = 'https://mac.R-project.org')``

Correcting errors on install...

also installed rgeos for maptools

prophet required rstan and this required me to first delete the following directory:

``/usr/local/lib/R/site-library/00LOCK-rstan``

We need to use older versions of some packages:

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/nloptr/nloptr_1.2.1.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/pbkrtest/pbkrtest_0.4-7.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/car/car_3.0-2.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

for treemapify:
``packageurl<-"https://cran.r-project.org/src/contrib/Archive/ggfittext/ggfittext_0.6.0.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

for mapview:

``install.packages("satellite")``

``install.packages(c("sf", "svglite", "uuid", "webshot"))``

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/mapview/mapview_2.6.3.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

for Hmisc:

``install.packages("acepack")``

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/latticeExtra/latticeExtra_0.6-28.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/Hmisc/Hmisc_4.1-1.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

For ggpmisc:

``packageurl<-"https://cran.r-project.org/src/contrib/Archive/splus2R/splus2R_1.2-2.tar.gz"``
``install.packages(packageurl, repos=NULL, type="source")``

packageurl<-"https://cran.r-project.org/src/contrib/Archive/ggpmisc/ggpmisc_0.3.4.tar.gz"
``install.packages(packageurl, repos=NULL, type="source")``

**Addendum** Hmmm having trouble with some maps so let's try to upgrade everything instead...

Back out of R and add:

``deb http://cloud.r-project.org/bin/linux/debian buster-cran40/``
 
 to
 
``/etc/apt/sources.list``
then

``apt update``
``apt install -t buster-cran40 r-base``

Then ``sudo R`` again:

``update.packages(lib.loc="/usr/local/lib/R/site-library", ask = FALSE,
  checkBuilt = TRUE, Ncpus = 4)``

(4 processors in my case - use htop to see.)

then had to add

``install.packages("mapproj")``

... which was the issue all along... but at least R is now on version 4.


**Note** 
Subsequently to update to 4.1 a key is now required: http://cloud.r-project.org/bin/linux/debian/:

``apt-key adv --keyserver keyserver.ubuntu.com --recv-key '95C0FAF38DB3CCAD0C080A7BDC78B2DDEABC47B7'``

Then:

``apt update``

``sudo apt upgrade``

The reason for the update was to install IMD.  But while we are at it there are a few additional packages I've added since the initial install:

``install.packages(c("formattable", "IMD", "car"))``

# R studio

``sudo apt-get install gdebi-core``

``wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.3.1093-amd64.deb``

``sudo gdebi rstudio-server-1.3.1093-amd64.deb``

``sudo adduser rstudio``

Since update to R Studio 4.1, an update to R Studio is required:

``sudo apt-get install gdebi-core``

``wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2021.09.2-382-amd64.deb``

``sudo gdebi rstudio-server-2021.09.2-382-amd64.deb``

# Python stuff

``sudo apt install python3-pip``

``sudo apt-get install python3-pandas``

``pip3 install boto3``

``pip3 install msoffcrypto-tool``

# Other

``sudo apt-get install pandoc``

``sudo apt-get install xlsx2csv``

``sudo apt-get install ghostscript``

``sudo apt-get install poppler-utils``

``sudo apt-get install p7zip-full``

``sudo apt-get install mosh``

``sudo apt-get install ncdu``

``sudo apt install neofetch``

``sudo apt install htop``

``sudo apt install rename``

``sudo apt install parallel``

## Setting up git

``sudo apt-get install git``

``su yourname``

``git config --global user.name "John Doe"``

``git config --global user.email john.doe@emailprovider.com``

``ssh-keygen -t rsa -b 4096 -C "john.doe@emailprovider.com"``

``cat ~/.ssh/id_rsa.pub``

add to git settings in web git service.

## Overleaf

Full instructions are here: https://github.com/overleaf/toolkit/blob/master/doc/quick-start-guide.md

In brief:

``sudo apt-get install docker``

``sudo apt-get install docker-compose``

``git clone https://github.com/overleaf/toolkit.git ./overleaf``

``cd overleaf``

``bin/init``

``vim config/overleaf.rc`` and to enable direct access to Overleaf from your server's IP address change the IP address for SHARELATEX_LISTEN to:

``SHARELATEX_LISTEN_IP=0.0.0.0``

bin/up and create admin account by visiting http://your-ip-here/launchpad

exit session and gracefully end Overleaf server with Ctrl-C.

Then to run an unattached session:

``bin/start``

(end with ``bin/stop``)

Chances are a more complete LaTeX installation will be needed, so following https://blog.felixviola.de/overleaf-ce-setup-your-own-latex-server-tutorial/:

``bin/shell``

``wget https://mirror.clientvps.com/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz``

``tar -xf install-tl-unx.tar.gz``

``cd install-tl-*``

``perl install-tl``

Reject using previous config and then press i for full install, which as usual will take a LONG time.

Then ``exit`` out of the shell, ``bin/stop`` and then ``bin/start`` overleaf for good measure.
