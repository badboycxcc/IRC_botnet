# IRC_botnet
A simple botnet that propagates via TELNET, controlled via IRC server, can execute shell commands and launch DDoS attacks 

This botnet targets TELNET services with common usernames and passwords and is capable of launch DDoS attacks. 
It handle shell commands too, returning the result via IRC channel.

This botnet is tested only in telnet service implemented by BusyBox linux. There is no guarantee of success in other implementations.

Two types of DDoS is possible UDP flood and TCP SYN flood.

Possible commands that the botmaster can use in IRC channel

  @help : prints help screen directly to the IRC channel
  
  @scan <ip> : make a scanning of the network passed, the scan only test the fourth octet, e.g @scan 172.17.0.0 will scan from 172.17.0.1 to 172.17.0.254. If <ip> is ommited or set to 0, then the bot IP itself is assumed. Let <ip> blank can be useful in compromised networks where bot is sit in
  
  @attack udp <target ip> <number of packets> <source port | 0> <destination port | 0> <rate | 0> <spoof | nospoof> <spoofed ip | 0>  :
  launches DDoS attack of type UDP flood. <target ip> is the ip of the victim. if <source port> or <destination port> is zero they are randomized at every <rate> packets, e.g. @attack 172.17.0.1 1000 22 0 200 nospoof will launch 1000 UDP packets with 5 
 different destination ports i.e 200 packets for every random destination port, source port will be 22 in all packets, unless setted to zero too. <rate> can be setted to zero for default change, wich is 100. spoof or nospoof is used to determine if source IP address of the packets is true or not. <nospoof> will use the bot ip address, <nospoof> will use <spoofed ip> as source address, if <spoofed ip> is zero then source ip is randomized at every <rate> packets.
  
  @attack tcp <target ip> <number of packets> <source port | 0> <destination port | 0>
  same as UDP attack, but source IP is spoofed and random at every packet, same as port, if ports are setted to zero they are randomized at every packet. TCP SYN flood implies spoofed source IP.
  
  @kill destroy bot process
  
  !<shell command> : to execute shell commands just put a ! infront
 

  