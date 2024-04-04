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

### TCPv4
- again, ask the participants to monitor *eth1*
- on the host, run `./00-v4-tcp-echo-connection -n X`
- explain what can be seen

### TCPv6
- ask participants to click on *restart current capture*
- on the host, run `./00-v6-tcp-echo-connection -n X`
- explain that it is all the same as in v4

### Todo
- icmp
  - ping
  - traceroute

### Web

#### HTTP

- ask everyone to capture on interface `eth0`
- on the host, run `./05-v4-http -n X`
- ask everyone to stop capturing using the red square
- now, how to find something meaningful?
  - enter `http` into the search bar
  - you only see the http connection
  - right-click on the second line
    - follow -> TCP Stream
    - you see the text in a separate window
    - click on close
  - you now see the complete TCP conversation only
    - check the search line

For IPv6:
- you have to add a NAT rule, it is in the file
- execute `./05-v6-http -n X` 
- note that the filter `http` works for v4 and v6

#### HTTPS

- https is encrypted
- lets have a look
- start capturing on `eth0`
- on the host run `./06-v4-https -n X`
- ask to search for "http"
  - no result
- since it is https, we must search for "tls" (no, its not logical)
- do not forget to clear the "http" filter
- right click on the first one, choose "follow TCP stream"
- analyze the client hello packet
  - server name is unencrypted
- to see more we need the key for decryption
- this can be get from the browser or via man in the middle attack
- fortunately, you can setup some browsers to export the key and feed this into wireshark
  - go to "edit"->"preferences"
  - "protocols"->"TLS" (lots of scrolling)
  - click on the "browse" button at "Pre-Master-Secret log filename"
  - go up one directory (green arrow top right)
  - double click on "tlskeys"
  - click on ok
- notice anything changed?
- protocol now shows "http2"
- right click on one of the http2 lines
  - "follow"->"http2 stream"


