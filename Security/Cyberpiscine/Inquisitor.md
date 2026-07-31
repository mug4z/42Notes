# Informations

## Goal
Perform an ARP poisoning in both direction (full duplex).
When the attack is stopped (CTRL+C), the ARP tables will be restored.
The files name exchange between a client and a FTP server should be displayed in real time.

## Test
You have to prepare a test suite using an FTP connection in addition to the other tests.
## Arguments
 - `<IP-src>`
 - `<MAC-src>`
 - `<IP-target>`
 - `<MAC-target>`
## Libraries
- libpcap: capture, parse and craft network packets. [PcapPlusPlus](https://pcapplusplus.github.io/)
	- For using the C++ variant need the libpcap.
## Searches
- cmake what the fuck ? -> DONE
- ARP poisoning WTF ? -> DONE

### PcapPlusPlus
`pcpp::Ethlayer` `pcpp::ArpLayer`  `pcpp::ArpReply`

`pcpp::Packet::addLayer()`


https://pcapplusplus.github.io/docs/tutorials/intro
https://github.com/seladb/PcapPlusPlus/tree/v25.05/Examples/Tutorials/Tutorial-HelloWorld
https://en.wikipedia.org/wiki/Berkeley_Packet_Filter