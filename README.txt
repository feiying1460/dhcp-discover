                  Welcome to the world of dhcp-discover!

dhcp-discover is a very simple cmdline utility that sends out a dhcp request and
shows what replies it get. It is useful when you want to error search why a target
doesn't boot via dhcp and you want to view the target side of the story, just use
this utility (remember to change mac address then to the one your target have,
do this via the -e option, so that the dhcp request sent out by this tool looks
like the one coming from target). Of course, tools like wireshark could also be
used but this is a quick way to get some info.


Howto build:

Follow this little guide, if it is not obvious already:

  1. Install dependencies, which is packages libnet-devel and libpcap-devel.
  2. Download dhcp-discover from sourceforge.net
  3. Unpack tarball
  4. make

You should now have a app called dhcp-discover where you did make.


Howto run:

Running "dhcp-discover --help" will show the available options.
It is needed to run dhcp-discover as root, so that it can put
the network interface into promiscous etc for listen on the replies.

Running "dhcp-discover" alone, will use a default mac addr and default
interface to send out on.

Running "dhcp-discover -e <some mac address> -i <some eth interface>",
will use the specified mac addr and send out a dhcp request for it on
the specified eth interface.

The dhcp request as well as eventual replies will be displayed:

$ sudo ./dhcp-discover -e 00:90:0B:1D:FD:82 -i eth1
Ethernet hw addr to do discovery on : 00:90:0b:1d:fd:82

 - beginning of dump -
DHCP operation          : request
Hardware type           : ethernet
Hardware address length : 6 bytes
Hop count               : 0
Transaction ID          : 0xdeadbeef
Number of seconds       : 0
Flags                   : 0x8000
Client IP               : 0.0.0.0
Your IP                 : 0.0.0.0
Server IP               : 0.0.0.0
Gateway IP              : 0.0.0.0
Client hw addr          : 00:90:0b:1d:fd:82
Server hostname         : 
Boot filename           : 
Options
  Magic header          : 0x63825363 (OK)
  Message type          : discover
  Option 0x37           : len 7
 - end of dump -

 - beginning of dump -
DHCP operation          : reply
Hardware type           : ethernet
Hardware address length : 6 bytes
Hop count               : 0
Transaction ID          : 0xdeadbeef
Number of seconds       : 0
Flags                   : 0x8000
Client IP               : 0.0.0.0
Your IP                 : 192.168.10.105
Server IP               : 192.168.10.101
Gateway IP              : 0.0.0.0
Client hw addr          : 00:90:0b:1d:fd:82
Server hostname         : 
Boot filename           : pxelinux.0
Options
  Magic header          : 0x63825363 (OK)
  Message type          : offer
  SERVIDENT             : 192.168.10.112
  LEASETIME             : 3600 seconds
  SUBNETMASK            : 255.255.255.0
  ROUTER                : 192.168.10.1
 - end of dump -
$
