# Wireshark in Docker

## Preparation

- set the number of participants with `export Participants=8``
  - alternatively you can define that in `~/.bashrc`

## Setup

- use `make` to create the client directories and docker compose file
- use `docker compose up` to start the containers

Wireshark seats for participants are now via https on port 7001++

## Troubleshooting

- Restarting a container: `docker container restart rXX`, participant then reloads the browser window

## Experiments

### UDP v4

- Participants access their Wireshark containers
- Explain the start screen
- double-click on the *eth1* interface
  - if someone clicked wrong interface:
    - click on the red square
    - click on *File* -> *close*
- on the host, start script `./00-v4-send-udp-echo-packet -n X`
- explain what is visible
  - top window
  - bottom left window
    - you can click on items
    - items clicked on are hightlighted in the bottom right window
  - bottom right window
    - notice that you can scroll right and see it in ascii
- click on the green icon with the circular arrow to clear the screen

### UDPv6

- on the host, start script `./00-v6-send-udp-echo-packet -n X``
- looks similar, only with IPv6
- now both, start `./00-v4-send-udp-echo-packet -n X` again
- if there is too much on the screen, you can *filter*
  - type `ipv6` into the filter line
  - line turns green means its a valid filter
  - now change it to `!ipv6`
  - logical expressions are possible

### Web / HTTP

