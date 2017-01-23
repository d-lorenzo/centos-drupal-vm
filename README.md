# centos-drupal-vm

### Recommended Vagrant v1.9.0

## Installation

  + Install Virtualbox
    + Make sure to install "host-only network adapter" with it
  + Install Vagrant
  + Open terminal
  + Run `vagrant plugin install vagrant-vbguest`
  + Run `vagrant plugin install vagrant-winnfsd`
  + cd to vm root directory
  + Run `vagrant up`
    + If any errors show up, retry with `vagrant reload --provision`
  + If everything went ok, the vm is ready for use
    + To stop the vm, issue `vagrant halt`
    + To resume using it: `vagrant up`
  + **Details:**
    + URL: http://10.0.0.10/
    + SSH:
      + Host: 127.0.0.1
      + Port: 2222
      + User: vagrant
      + Password: vagrant
    + MariadDB:
      + User: root
      + Pass: toor
      + Adminer in http://10.0.0.10/adminer.php
    + Mailhog:
      + Server: localhost
      + Port: 1025