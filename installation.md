
  
# *Installation*

Installation of the Snappy Frontend is done via a chroot container.

Download the latest version from the repo:  [https://github.com/att/snappy-chroot-frontend](https://github.com/att/snappy-chroot-frontend)

Unpack the .tgz file:
```
tar xzvf snappy-fe-chroot-vx.y.z.tgz
```
<br>
Before starting the Frontend, two steps need to be taken:

(1) Edit the environment variables file:

```
srv/snappyfe/bin/edit_env_vars
```

(2) Edit the tables for the sources, targets and tenants:
```
/srv/snappyfe/bin/edit_tables
```
Details on these steps are in the **Setup** section


To *start* the Frontend service: ```srv/snappyfe/bin/start [port_number]  ```

To *stop* the Frontend service: ```srv/snappyfe/bin/stop```

By default the Frontend will run on port 8080.  Use the *port_number* option to to change it.


