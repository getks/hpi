##### We will provide this service description file with the microservices to enable and run them.
##### This will also have DB_IP and DB_PORT as environment variables:

```sh
[Unit]
Description=S1 micro service
After=network.target

[Service]
Environment="APP_HOST=0.0.0.0"
Environment="APP_PORT=5000"
Environment="DB_HOST=10.0.2.121"
Environment="DB_PORT=5432"
User=root
ExecStart=/opt/venvs/S1/bin/S1
WorkingDirectory=/opt/venvs/S1/
Restart=on-failure
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

To enable the service, use the following commands:
```sh
systemctl daemon-reload
systemctl enable S1.service
systemctl enable S1.service
```
