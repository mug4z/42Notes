#  Informations
## Goal
Create a static web page accessible from Tor.

## What to config
- [ ] torrc
- [ ] nginx
- [x] index.html ✅ 2026-05-27

## TODO
- [x] SSH ✅ 2026-05-29


### server ssh

copy the pulic content to the .ssh/authorized_keys file
### Client connection

Install tor, and ssh.
create key 
upload the public key on the server and the private on the client.
ssh add the key
use torsocks to use ssh over tor and connect to the .onion website.
## Sources
https://community.torproject.org/onion-services/setup/
https://2019.www.torproject.org/docs/tor-manual.html.en
[Tor code sources](https://gitlab.torproject.org/tpo/core/tor)
[Tor- torrc sample](https://gitlab.torproject.org/tpo/core/tor/-/blob/HEAD/src/config/torrc.sample.in)
[Tor socks](https://gitlab.torproject.org/tpo/core/torsocks/)
