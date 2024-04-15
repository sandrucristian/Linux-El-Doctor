
 ![TypingCodeGIF](https://github.com/sandrucristian/Linux-El-Doctor/assets/149951695/5ebe0f4c-5287-452e-bb1f-f6728f810a0c)
# Introduction


In this project I will only use the terminal programs from Ubuntu Server that are already installed to monitor the 
services that are running. We will create a file with reports about the users who are connected to the server. 
Script about the memory status. We will create a script that checks if a service is 
running normally in memory and if it is disabled or if it stopped due to some problem then that script will restart it.

In this example I will use a script to create an alias to find the IP address of the server, in this way we will gather information 
about users, processes, HDD space and other information.
```
alias my-pc-ip="echo $(ifconfig | grep broadcast | awk '{print $2}')"
```
As you can see, grep search for the paragraph containing the word "broadcast" and awk choose the second word, and this is the IP address.

Here’s an example of a simple Bash script that you can use to automate the monitoring of disk space on a Linux system. 
This script will check the available disk space and send an alert if it falls below a certain threshold.

```
#!/bin/bash

# Set the threshold percentage (e.g., 20%)
THRESHOLD=20

# Set the email address for alerts
EMAIL="your-email@example.com"

# Check each mounted filesystem
while read line; do
  # Get the use percentage and remove the '%'
  usep=$(echo $line | awk '{ print $5}' | tr -d '%')
  partition=$(echo $line | awk '{ print $1}' )

  # Check if the use percentage is greater than or equal to the threshold
  if [ $usep -ge $THRESHOLD ]; then
    echo "Running out of space \"$partition ($usep%)\" on $(hostname) as on $(date)" |
     mail -s "Alert: Almost out of disk space $usep%" $EMAIL
  fi
done < <(df -H | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{print $1 " " $5}')
```
Make sure to replace "your-email@example.com" with your actual email address. You can also adjust the THRESHOLD value to the percentage of disk space usage that you consider critical.
To automate the execution of this script, you can add it to your crontab to run at regular intervals. For example, to run the script every day at midnight, you would add the following line to your crontab:
0 0 * * * /path/to/your/script.sh
Remember to give the script execution permissions with chmod +x /path/to/your/script.sh.
This script is a basic example to get you started. Depending on your needs, you might want to monitor other aspects of 
your system, such as CPU load or memory usage. You can find more complex and comprehensive scripts online, or you can extend 
this script to include additional checks.

![HealthDoctorGIF](https://github.com/sandrucristian/Linux-El-Doctor/assets/149951695/6f6c5673-891d-44ee-88b1-e62a89a0e7b9)
