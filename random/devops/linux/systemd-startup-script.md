# Systemd Startup Script

In this post, we will see how to run our bash script during startup like apache , mysql and other services using `systemd`

#### **First, we need to create our bash script that we want to run on startup.**

For this example, we have script to mount shared folder of host to virtual machine. Save the following script as `/home/userName/scirpt/shared.sh`

```bash
#!/bin/bash
#"password" is your password to run sudo cmd
echo "password" | sudo mount -t vboxsf Shared-Name /home/userName/Shared-location/;
```

we also want it to be executable so we can give it permission to execute using following cmd:&#x20;

```bash
chmod 774 shared.sh
```

#### **Next, we need to create systemd start up script.**

Create systemd startup script like `systemdStartUpScript.service` then place it at `/etc/systemd/system` _****_&#x20;

systemd script has basic structure like given below:

```bash
[Unit]
After=mysql.service

[Service]
ExecStart=/home/userName/shared.sh

[Install]
WantedBy=default.target
```

* `After`: Instructs systemd on when the script should be run. In our case the script will run after mysql.service has started.
* `ExecStart`: Need to provide full path to the script we created earlier
* `WantedBy`: Into what boot target the systemd unit should be installed

#### **Install systemd script and enable it to execute at boot time**

Next we want the systemd script, we created earlier to be able to read by systemd so we can give it permission to read using following command.

```bash
chmod 664 to /etc/systemd/system/systemdStartUpScript.service
```

Then install systemd service unit and enable it so it will be executed at the boot time:

```bash
systemctl daemon-reload
systemctl enable systemdStartUpScript.service
```

Finally, reboot your system to see the script execute and aromatically mount the shared folder to virtual machine in this case.\
