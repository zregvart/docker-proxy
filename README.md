docker-proxy
============

Transparent proxy for docker containers, run in a docker container - https://hub.docker.com/r/silarsis/docker-proxy/

## Instructions for Use

The "run.sh" script will run the container and setup the appropriate iptables
and ip routing rules.

NOTE: This project is _not_ designed to be run with a simple "docker run" - it
requires the "run.sh" script to be run on the docker host, so it can adjust the
routing rules. You will need to check this code out from
https://github.com/silarsis/docker-proxy/
and run the "run.sh" script on the host (for OS X, that's on your boot2docker or
similar host).

## Overview

The run.sh script will fire up a docker container running squid, with
appropriate iptables rules in place for transparent proxying. It will also
configure port-based routing on the main host such that any traffic from a
docker container to port 80 routes via the transparent proxy container.

The run.sh script is designed to run in the foreground, because when the
container terminates it needs to remove the rules that were redirecting the
traffic.

If you want to see squid in operation, you can (in another terminal) attach
to the squid container - it is tailing the access log, so will show a record
of requests made.

## Notes

* This script assumes you have "sudo" access to perform the iptables changes

* the format of the run.sh script is a bit strange - that's because it's also used as part of a larger framework on my own machine.

* There exists a real possibility this script will break your iptables or ip rules in some unexpected way. I've tried to be reasonably tidy and careful, but be aware that if things go wrong, the potential exists for all containers to lose the ability to download anything.
