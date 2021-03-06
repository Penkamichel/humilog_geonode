Humilog_Geonode
========================

You should write some docs, it's good for the soul.

Installation
------------

Install the native dependencies for your platform.

Install virtualenv and virtualenvwrapper, Create a local virtual environment for your project and install Django into it.::

    $ mkvirtualenv my_geonode
    $ pip install Django==1.8.12

Create a new template based on the geonode example project.::
    
    $ django-admin.py startproject my_geonode --template=https://github.com/GeoNode/geonode-project/archive/master.zip -epy,rst,yml -n Vagrantfile

.. note:: You should NOT use the name geonode for your project as it will conflict with the default geonode package name.

Install the dependencies for your geonode project into your local virtual environment::

    $ pip install -e my_geonode

Install and Configure GeoServer

.. note:: At this point, you should put your project under version control using Git or similar.

Using ansible for Automated Deploys
-----------------------------------

In order to install for production on a remote machine or to a local VM for development, you will need to install ansible::

     $ sudo pip install ansible

Note: It is advisable to install ansible system wide using sudo

Next, you will need to install the ansible role for geonode::

     $ ansible-galaxy install ortelius.geonode

Setting up a vagrant box
-------------------------

Setup VirtualBox and install vagrant, then setup your virtual machine with::

    $ vagrant up

Note: the vagrant installation uses Ansible, so you will need to follow the steps in the previous section.

Usage in production
-------------------

Update /etc/ansible/hosts to include your webservers host or dns entry::

    [webservers]
    ###.###.###.###

Then you can run the playbook to install the humilog_geonode  project::

    $ ansible-playbook playbook.yml

Basic Usage
-----------

Setup the database::

    $ python manage.py syncdb

.. note:: You will be asked to provide credentials for the superuser account.

Start the development server::

    $ python manage.py runserver
