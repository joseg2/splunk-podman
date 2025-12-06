

# build image

```
podman build -t spk:9.4.7 .
```

# run container

```
podman run -p 8000:8000 -p 8089:8089 -v /var/log:/opt/data -e "SPLUNK_PASSWORD=ChangeThisForReal" -e "SPLUNK_START_ARGS=--accept-license" -e SPLUNK_GENERAL_TERMS=--accept-sgt-current-at-splunk-com -it --name splunkpodman localhost/spk:9.4.7
```


# Field extraction transform

Fields » Field extractions » ryzen : EXTRACT-edge_temp,mem_temp_crit,junction_temp,junction_temp_crit,mem_temp

```
^(?:[^=\n]*=){6}\+(?P<edge_temp>\d+\.\d+)[^\+\n]*\+(?P<mem_temp_crit>\d+\.\d+)(?:[^\+\n]*\+){2}(?P<junction_temp>\d+\.\d+)[^\+\n]*\+(?P<junction_temp_crit>\d+\.\d+)(?:[^=\n]*=){3}\+(?P<mem_temp>\d+\.\d+)
```


# The install directory contains the .deb file with the splunk package and files for the search app for monitoring sensor data

```
 .
 ├── Dockerfile
 ├── install
 │   ├── search
 │   │   └── local
 │   │       ├── data
 │   │       │   └── ui
 │   │       │       └── views
 │   │       │           └── amd_ryzen.xml
 │   │       ├── inputs.conf
 │   │       └── props.conf
 │   ├── splunk-9.4.7-2a9293b80994-linux-amd64.deb
 │   └── user-seed.conf
 └── README.md
```

