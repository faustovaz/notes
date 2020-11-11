# Systemctl

- In general, services are located in `/etc/systemd/system/` and are described in `.services` files.
  To create a new service, follow the steps:

  1. Create a `.service` file, for example `my-app.service`

  2. Add context:

     ```bash
     [service]
     ExecStart=/usr/bin/python3 /opt/code/app.py
     ```

  3. Reload systemctl daemon: `$ systemctl daemon-reload`

  4. Start the new service: `$ systemctl start my-app`

  5. To start a service when the system is booted up:

     ```bash
     [unit]
     Description=My python web app
     
     [service]
     ExecStart=<command>
     ExecStartPre=<command>
     ExecStartPos=<command>
     
     [install]
     WantedBy=multi-user.target
     ```

  6. *TODO* 