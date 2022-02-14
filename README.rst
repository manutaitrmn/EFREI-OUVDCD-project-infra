==================================================================================================================
[VAGRANT][ANSIBLE] Déploiement de 2 serveurs web Apache + Loadbalancer Haproxy avec base de données distante Mysql
==================================================================================================================

Ce projet déploie :

- 1 VM avec une base de données Mysql
- 2 VMs avec deux serveurs web Apache
- 1 VM avec un loadbalancer Haproxy


Requirements
------------

Nécessite l'installation de Vagrant et de Ansible.

.. code:: bash

    $ sudo apt-get update
    $ sudo apt-get install vagrant
    $ sudo apt-get install ansible
    
Nécessite l'installation de Virtualbox.

.. code:: bash

    $ echo "deb http://download.virtualbox.org/virtualbox/debian stretch contrib" >> /etc/apt/sources.list
    $ wget -q -O- https://www.virtualbox.org/download/oracle_vbox_2016.asc | apt-key add
    $ sudo apt-get update
    $ sudo apt-get install virtualbox-5.1

Déploiement
-----------
    
Clonage du repository.

.. code:: bash

    $ git clone https://github.com/jtanph/nowledgeable-project1 && cd nowledgeable-project1

Création des machines virtuelles avec Vagrant puis déploiement avec Ansible.

.. code:: bash

    $ vagrant up

Utilisation
-----------
| Depuis notre navigateur web :
|
| 192.168.56.252 : Loadbalancer
| 192.168.56.253 : Serveur Apache 1
| 192.168.56.254 : Serveur Apache 2
|
| Chaque serveur web peut aussi se connecter à la base de données.
|
| (mot de passe "vagrant")
| Depuis le premier serveur web :
.. code:: bash

    $ vagrant ssh web1
    $ mysql -u web1 -h 192.168.56.251 -p
| Depuis le second serveur web :
.. code:: bash

    $ vagrant ssh web1
    $ mysql -u web2 -h 192.168.56.251 -p

