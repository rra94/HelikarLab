# HelikarLab

Helikar Lab GSoC application

##RApache Setup
Follow these steps to setup RApache:

1. First Install the following dependencies for Ubuntu:

  ```
    sudo apt-get install g++
    sudo apt-get install libpng-dev libX11-dev libXt-dev
    sudo apt-get install apache2 apache2-mpm-prefork apache2-prefork-dev
  ```
2. Install R:

  ```
    sudo apt-get install r-base-dev
   ```
3. Install the follwing R packages. Make sure that the you install them in the root library. 

  ```
    install.packages(c("brew", "XML", "rjson", "RMySQL", "RJDBC", "rJava","Cairo", "Hmisc"))
   ```
4. Install R apache (VERSION here is 1.2.5)

  ```
    Download the RApache tarball from http://rapache.net/downloads.html
    tar xzvf rapache-VERSION.tar.gz 
    cd rapache-VERSION
    ./configure
    make
    sudo make install
   ```
5. After the installation is complete, you have to create the follwing two files:
 
  r.conf in /etc/apache2/mods-available/r.conf :
   Add the following lines of code in it:
    ```
    <Location /R>
    ROutputErrors
    SetHandler r-script
    RHandler sys.source
    </Location>
   
    <Location /RApacheInfo>
    SetHandler r-info
    </Location>
    
    <Directory /var/www/brew>
  	SetHandler r-script
  	RHandler brew::brew
    </Directory>
    ```

  Now all files in /R are assumed to be R-scripts, in /RApacheInfo you’ll find some information about your installation and   all files under /var/www/brew is passed through the function brew located in the package brew.

  The second file r.load in /etc/apache2/mods-available/r.load :
  
   ```
    LoadModule R_module /usr/lib/apache2/modules/mod_R.so
   ```
6. Now restart the server

  ```  
    sudo a2enmod r
    /etc/init.d/apache2 restart
  ```
##DemoBrew Setup

A simple app that takes in 3 numbers from the user and returns a descriptive summary.
This is built using brew and runs on RApache.
To get this working:

1. Setup RApache.

2. Create a folder called "brew" in your /war/www/

3. Copy this file in the folder.

4. Make sure you have added the required handler (see RApache Setup). 

5. Start RApache and open this file from your browser.

##OpenCPU Demo
A simple app that takes in 3 numbers from the user and returns the mean. This demo uses the OpenCPU library.

Working demo can be found at:
http://home.iitk.ac.in/~rrishav/demo2.html

