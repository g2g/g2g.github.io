---
title: Remind Urgent Tasks
date: 2020-10-11T05:18:49+01:00
---
... with desktop notifications from Taskwarrior

## Script it ##

* send only **`tasks with high priority`** list as desktop notification

#### **`task_notify_send.sh`**
```bash
#!/usr/bin/env bash

export DBUS_SESSION_BUS_ADDRESS="unix:path=/run/user/$EUID/bus"
notify-send -u critical  "$(for ID in $(task priority:V _ids); do echo [$ID]$(task $ID export | jq -r '.[].description') ; done)"
```

## Schedule it ##

* schedule **`task notification`** as systray message every 20 minutes in Crontab

```bash
# crontab -l
/20 * * * * ~/.local/bin/task_notify_send.sh
```

## Sources ##

* <https://www.sudipbhandari.wtf/task-warrior-reminder/>
* <https://eshapard.github.io/export-taskwarrior-dates-to-remind.html>

