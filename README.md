# fllCam
A simple python script that uses the feed of a RaspberryPi Camera and outputs it via HDMI and a simple WebServer (multipart/x-mixed-replace).

This script needs to be run as with sudo because of port 80.

# Run at startup
You can use systemd to run this script on startup like this:

1. Edit the file at `/etc/systemd/system/<your-service-name>.service`
```
[Unit]
Description=RPICAM2 Script to output to HDMI and HTTP
After=multi-user.target

[Service]
Type=idle
ExecStart=sudo /usr/bin/python3 /path/to/your/script.py

[Install]
WantedBy=multi-user.target
```
2. Add en exception for the passwordless execution with sudo:<br>
2.1. `sudo visudo`<br>
2.2. Add the line: `<your-username> ALL=(ALL) NOPASSWD: /usr/bin/python3 /path/to/your/script.py`<br>
4. Enable the service with `sudo systemctl enable <your-service-name>`
5. (Optional) Start it with `sudo systemctl enable <your-service-name`

Now everytime you boot your pi you should see a fullscreen feed of your camera!

<hr>

Please not that for some resolutions you need to adjust the code in lines 98 and 100.
