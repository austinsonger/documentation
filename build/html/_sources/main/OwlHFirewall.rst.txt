Check your Firewall
---------------------

Please, be sure your firewall is properly set.

When using iptables 
````````````````````

OwlH Master and UI:

::

    * sudo iptables -A INPUT -p tcp --dport 50010:50020 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
    * sudo iptables -A INPUT -p tcp --dport 50001 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
    * sudo iptables -A INPUT -p tcp --dport 8005 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
    * sudo iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
    * sudo iptables-save

OwlH Node:

::

    sudo iptables -A INPUT -p tcp --dport 50010:50020 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 50002 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
    sudo iptables-save


When using firewalld
````````````````````

OwlH Master and UI:

::

    sudo firewall-cmd --zone=public --permanent --add-port=50001/tcp
    sudo firewall-cmd --zone=public --permanent --add-service=https
    sudo firewall-cmd --zone=public --permanent --add-port=50010-50020/tcp
    sudo firewall-cmd --zone=public --permanent --add-port=8005/tcp
    sudo firewall-cmd --reload

OwlH Node:

::

    sudo firewall-cmd --zone=public --permanent --add-port=50010-50020/tcp
    sudo firewall-cmd --zone=public --permanent --add-port=50002/tcp
    sudo firewall-cmd --reload