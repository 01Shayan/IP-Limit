# IP-Limit

Limiting the number of active users with IP
<br>[**Marzban version**](https://github.com/Gozargah/Marzban)
<br>
Supports both IPv4 and IPv6.It also supports Marzban-node<br>

<hr>

# Installation

At first you need add this to your xray config file(If it doesn't exist) :

```json
"log": {
    "loglevel": "info"
},
```

![loglevel](https://raw.githubusercontent.com/01Shayan/IP-Limit/main/img.png)
**then save it**

Attention, this script only supports Python version 3.8 and above. If your Python is old, please update it(you can check your python version with `python3 -V`).

At first update your system and install pip:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip -y
sudo apt install python3-venv -y
```

Then clone the project:

```bash
git clone https://github.com/01Shayan/IP-Limit.git
cd IP-Limit
python3 -m venv venv
source venv/bin/activate
cd IP-Limit
cd core
```

And Then you need install these libraries:

```bash
pip install websockets
pip install requests
pip install pytz
```

After that you need to enter your domain or server IP(and other information) in the [v2iplimit_config.json](v2iplimit_config.json) file

<hr>

## configuration

```bash
nano v2iplimit_config.json
```

You can change [this file](v2iplimit_config.json) according to your needs:

```json
{
  "WRITE_LOGS_TF": "True", // --> write the logs like who disable and how many users are active now and ...
  "SEND_LOGS_TO_TEL": "False", // --> send logs to a telegram bot
  "LIMIT_NUMBER": 2, // --> number of active IPs for all users
  "LOG_FILE_NAME": "log_file_name.log",
  "TELEGRAM_BOT_URL": "https://api.telegram.org/bot[add_your_bot_token_here]/sendMessage", // --> get your token from @BotFather and delete the '[' and ']'
  "CHAT_ID": 111111111, // get from here --> @RawDataBot
  "EXCEPT_USERS": ["Username", "Username2"], // --> Accounts in this list will not be deactivated
  "PANEL_USERNAME": "admin", // --> Add your Marzban username here
  "PANEL_PASSWORD": "admin", // --> Add your Marzban password here
  "PANEL_DOMAIN": "sub.domain.com:443", // --> Add your Marzban domain name with port here
  "TIME_TO_CHECK": 240, // --> Check every x seconds (240 = 4minutes)
  "INACTIVE_DURATION": 210, // --> You can specify how long users should be disabled (in seconds)
  "SPECIAL_LIMIT": [
    ["user1", 4],
    ["user2", 1]
  ], // --> You can apply any number of IP limit per user like this, user1 can have 4 IPs
  "SERVER_NAME": "", // --> Optional, You can give your script a name that will appear in your logs.
  "PRETTY_PRINT": "True" // --> Optional, Logs will be sent to you in Telegram with a better appearance
}
```

<br>
This program is activated every <b>4 minutes (you can change it with <code>TIME_TO_CHECK</code>)</b>, it sends information, and users who have used more than the specified number of IPs are deactivated, and after x minutes(According to <code>INACTIVE_DURATION</code>), all users are activated. And it is checked again if there is a need to deactivate the user in these x minutes, and if so, it will do so.
And again after x minutes all users are activated and...

<b>As a result, users who use more than the specified IP cannot use their account unless they are equal to or less than the IP limit.</b>

<hr>

## Important notes

### screen

As you know, this program must always be running, so there are many ways to do this, but I recommend using the screen command (be sure to read about it so you don't get into trouble.)<br>
First, hit the screen command<br>

```bash
screen
```

On the screen that opens, press the space bar Then run the program.<br>

```bash
python3 v2_ip_limit.py
```

Now you can keep the program running in the background with the combined control A and D. Now if your connection to the server is interrupted, the program will remain running.

<b>To see active screens</b> Run this command<br>

```bash
screen -ls
```

And to go to that screen, this command

```bash
screen -r {id}
```

<hr>

### Tips on location

To change the time of the logs to your local time And considering only the IPs related to your country change line 27 and 28 of the [v2_ip_limit.py](v2_ip_limit.py) file. <sub>(By default they are Iran)</sub>
