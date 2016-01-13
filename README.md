# omshell-helper

Helper script that outputs valid omshell commands

## Usage

     omshell-helper [option] [object] [value]

### option

Acceptable options are...

`read`, which will display the state of the indicated object.

`set`, which will change the state of the indicated object.

### object

Acceptable objects are...

`control`, which allows you to shut the server down.

`failover-state`, which tracks the state of the failover protocol.

### value

Acceptable values are determined based on the selected object.

A value only needs to be specified if the option is "set". No values are neccesary to read an object.

#### Values applicable to the control object

* 2 -> Shut the DHCP server down. 

#### Values applicable to the failover-state object

* 1   -> startup
* 2   -> normal
* 3   -> communications interrupted
* 4   -> partner down
* 5   -> potential conflict
* 6   -> recover
* 7   -> paused
* 8   -> shutdown
* 9   -> recover done
* 10  -> resolution interrupted
* 11  -> conflict done

### Examples

To read the control object:

     omshell-helper read control | omshell

To set the failover-state to shutdown:

     omshell-helper set failover-state 8 | omshell


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
