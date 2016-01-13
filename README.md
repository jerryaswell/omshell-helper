# omshell-helper
Helper script that outputs valid omshell commands

## Setup
You will need to create a file called `omshell-helper.conf` in the following format. These variables correspond to the values configured in the dhcpd.conf file. For information about how to configure omapi on dhcp: http://www.jedi.be/blog/2010/12/08/automating-dhcp-management-with-omapi/

omshell-helper.conf

     SERVER="<ip-address>"
     PORT="<port to connect to>"
     KEY="omapiSecretKey"
     NAME="name of omapi profile" 

### omshell-helper.conf example

Consider the following configuration in dhcpd.conf on a dhcp server that has address 192.168.100.10.

     omapi-port 7911;
     omapi-key omapi-key;
     
     key omapi-key {
       algorithm hmac-md5;
       secret ViaRfmptqdHO1KUE3zBhiw==;
     };

The corresponding omshell-helper.conf would be

     SERVER="192.168.100.10"
     PORT="7911"
     KEY="ViaRfmptqdHO1KUE3zBhiw=="
     NAME="dhcp"
