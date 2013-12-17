# Github deploy daemon

Github post-receive webhook receiver

## Install

### 1. Copy config file to `/etc/github-deploy.json`

```bash
sudo cp config.example.json /etc/github-deploy.json
```

### 2. Edit config file


### 3. Copy init script

```bash
    sudo cp extra/debian/github-deploy.init /etc/init.d/github-deploy # debian style
    sudo cp extra/centos/github-deploy.init /etc/init.d/github-deploy # redhat style

    sudo chmod +x /etc/init.d/github-deploy
```

### 4. Start deamon

```
    sudo /etc/init.d/github-deamon start
```

### 5. Add to run level


```bash 
sudo update-rc.d add github-deploy defaults # debian style
sudo /sbin/chkconfig --add github-deploy # redhat style
```

## Config file

Config file is JSON stored on `/etc/github-deploy.json`


```json
    {
        "port": 8001,
        "allow_hosts" : ["207.97.227.253", "50.57.128.197", "108.171.174.178", "50.57.231.61"],
        "repositories":
        [{
            "url": "https://github.com/litmisty/github-deploy",
            "path": "/home/jung/tmp/github-deploy",
            "branch": "master",
            "command": "echo deploying"
        }]
    }
```


### port

The service port

### allow_hosts

IPs of github servers

### repositories

Target local repositories.

Daemon will check Url and branch, and checkout source from github to target 'path'

Make sure to check the **url**. 

**Do not enter the git repository url, use the github project url**

'command' will execute after checkout ended

