# Wireshark in Docker

## Preparation

- set the number of participants with `export Participants=8``
  - alternatively you can define that in `~/.bashrc`

## Setup

- `cd networking-basics-lab/wireshark-lab`
- use `make` to create the client directories and docker compose file
- use `docker compose up` to start the containers

Wireshark seats for participants are now via https on port 7001++

## Troubleshooting

- Restarting a container: `docker container restart rXX`, participant then reloads the browser window

## Introduction to Wirkeshark

### Connecting with your browser

All modern browsers should work. Please check that no "Zoom" is enabled - this makes the fonts look uggly. 

### Capture Window

When Wireshark opens, we start with the "Capture" window. Here we can select from which source packets are to be caputured. For the most experiments we will select the `eth1` interface. Please wait until I tell you from which interface we capture.

You can also enter a *capture filter* on top. Only packets matching this filter will be captured (this is different to a display filter (we learn about this later) which works on already captured packets).

You can capture on:

- physical interfaces (like `eth0` or `eth1`)
- remote systems using a number of helpers
- you can also read in a capture from a file (using File-Open)

Now double click on `eth1`.

Presenter: Wait until everyone is connected then run `./00-v4-send-udp-echo-packet -a`

### Main Window

The main window has the following sections:

- main toolbar
- filter toolbar
- packet list
- packet details
- packet bytes
- packet diagram (not visible per default)
- status bar (bottom)

To change panes:

- Edit -> Preferences -> Appearance -> Layout
  - we have space for three panes
  - we have four different panes
  - select what you want to see
  - now select "Packet Diagram" for Pane 3 and click "ok"

There are a lot of options. Feel free to play around later.

#### Main Toolbar

The main toolbar contains buttons for the most used functions:

- Four buttons to control capturing of packets
- Four buttons to work with capture files
- Some buttons to find packets and to jump around
- A button to toggle auto scroll when life capturing
- A button to toggle colorization of packets
- Four buttons to control size of text and columns

### Filter Toolbar

The filter toolbar controls what is visible (not what is captured!). Note that capturing continues unless you explicitly stop it.

Start typing in a filter:

- Try "ip". See that you get suggestions on how to complete
- Now try "arp"

See that the filter toolbar changes color once a filter is syntactically correct?

On the very right is a small down-arrow. Click it. The filter toolbar remembers past filters.

See the small "x" on the right? Click it. It clears the filter. Now click on it.



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

### ICMPv4 and ICMPv6 UDP

- ask participants to click on *restart current capture*
- ask to filter for `ip or ipv6` to filter out ARP messages
- on the host, run `./00-v4-icmp-portunreach -a`
- point and explain ICMP message
- on the host, run `./00-v6-icmp-portunreach -a`
- point out differences, ICMP codes

### Port unreach in TCP

- ask participants to click on *restart current capture*
- ask to filter for `tcp or icmp`


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


