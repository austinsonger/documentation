Download and prepare OwlH Installer 
````````````````````````````````````

.. table:: OwlH Installer downloads
   :widths: auto
   :align: center

===========================  =============================================================
OS version                   URL
===========================  =============================================================
CentOS 7                     wget http://repo.owlh.net/current-centos/owlhinstaller.tar.gz
Ubuntu                       wget http://repo.owlh.net/current-debian/owlhinstaller.tar.gz
Raspbian                     wget http://repo.owlh.net/current-arm/owlhinstaller.tar.gz
===========================  =============================================================

Now let's install it. 

:: 

  # mkdir /tmp/owlhinstaller
  # tar -C /tmp/owlhinstaller -xvf owlhinstaller.tar.gz

We are almost done. In order to allow OwlH installer to do its work, we need to tell it what is/are out target/s for this box. A target is an OwlH component that must be installed or updated. All this info is provided in the config.json file included in the owlhinstaller folder

