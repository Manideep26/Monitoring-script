We can track server reboot immediately to the team members by sending an automated email notification. We can achieve this goal by different ways. Simple way isto use the crontab @reboot option, by editing crontab file and adding following line 

@reboot /root/emailnotify.sh

we actually need to write the emailnotify script. This script will send us an email with some basic info when the server is started. The contents of my script are below:

#!/bin/bash

sleep 60

/sbin/service sendmail restart

IP=`hostname -i`
HOSTNAME=`hostname -f`
echo "$HOSTNAME online.  IP address: $IP" > /root/email.txt
echo >> /root/email.txt
date >> /root/email.txt

mail -s "$HOSTNAME online" -r restart@server.domain.tld manideep2601@gmail.com < /root/email.txt

rm -rf /root/email.txt

/sbin/service sendmail restart
