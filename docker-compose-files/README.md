# Note about native SSL

This branch is a quick and dirty (well, definitely dirty) way to get a WebConnector with SSL using the las2peer.dbis.rwth-aachen.de SSL certificate without touching las2peer’s code.
There are definitely other ways to achieve this (by changing the way las2peer treats / checks the certificate).

(The best way would be to circumvent the problem altogether by using a proxy or something to apply SSL, outside of this entire thing.)

This is how it works:

* The las2peer bootstrap container is given a hostname of `las2peer.dbis.rwth-aachen.de` (yes, as hostname!). Now las2peer accepts the certificate. However, since the hostname is now a valid domain name, the other containers can no longer reach it via the hostname.
* The las2peer bootstrap container is given a fixed IP (in the Docker network, 172.18.0.10 or something — look at the config). Since Docker Compose v3 does not support this, we specify a 2.x version in the config file.
* The other containers use that fixed IP to reach the las2peer bootstrap container.
