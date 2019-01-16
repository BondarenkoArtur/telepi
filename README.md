TelePi - remote streaming for your Raspberry Pi

TelePi is an attempt to build a better remote desktop solution for the Raspberry Pi by utilising the features of the platform. Dispmanx is used to capture the exactly what appears on screen and the hardware H.264 encoder to used to compress the video in real-time to allow for a smoother, higher framerate experience compared to traditional solutions such as VNC and remote X windows. It also brings the benefit of being compatible with all Raspberry Pi applications including Minecraft.

In addition to the streaming feature, TelePi can record the raw H.264 stream to a file making it useful for recording videos for tutorials and demostrations without the need for external hardware.

Note: This project is currently in a proof of concept phase and isn't very usable for general use, particularly as there are some latency issues to solve for streaming. Please feel free to try the project and contribute towards the development.

Usage:
Record to file: ./telepi <filename.h264>
Output to stdout: ./telepi <filename.h264>

## Stream to a remote computer using netcat ##

On the Raspberry Pi:
./telepi - | netcat <remote_ip> 5001

View on Windows:
ncat.exe -l -p 5001 | mplayer.exe -fps 31 -cache 512 -

OR





## Stream as a HTTP server ##

On the Raspberry Pi:
./telepi - | cvlc -vvv stream:///dev/stdin --sout '#standard{access=http,mux=ts,dst=:8090}' :demux=h264

View with VLC:
vlc http://raspberrypi.lan:8089/

# Stream as tcp server #
On the Raspberry Pi using netcat:
./telepi - | netcat -lkv4 8080

# On VLC #

tcp/h264://ip:port

# Example: #
File -> Open Network:  tcp/h264://192.168.0.1:8080


## Compile: ##

You will need to compile the ilclient library first.

cd /opt/vc/src/hello_pi/libs/ilclient
make

Go in the telepi folder and run
make

