# codespaces
Codespaces Learning Curve - Test Driving Ansible and kicking the tires. 

# WARNING Public Repo 


# Ansible Example two servers
server-1: 34.211.146.158  
server-2: 52.41.107.116

## SSH Setup - make sure you have valid keys
Server (here for this example)
```
ssh-keygen -t rsa -b 4096
ls -l ~/.ssh/id_*.pub
```
Copy keys to servers - password will be asked 
```
ssh-copy-id -i ~/.ssh/id_rsa.pub cloud_user@34.211.146.158
ssh-copy-id -i ~/.ssh/id_rsa.pub cloud_user@52.41.107.116
result: Number of key(s) added: 1
```
Test SSH login with keys, this should login directly without password
```
ssh cloud_user@34.211.146.158
ssh cloud_user@52.41.107.116
```
Other commands 
```
ssh-add -l
eval "$(ssh-agent -s)"
```

## Ping test via Anisble - without playbook
```
ansible all -m ping -v -i ansible/hosts -u cloud_user
```
## Ping test via Anisble - with playbook
```
ansible-playbook ./ansible/nginx.yml -i ansible/hosts -u cloud_user
```

output without playbook
```
34.211.146.158 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
...
52.41.107.116 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```
output with playbook
```
PLAY [ping] ***************************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************************
[DEPRECATION WARNING]: Distribution ubuntu 20.04 on host 52.41.107.116 should use /usr/bin/python3, but is 
ok: [52.41.107.116]
[DEPRECATION WARNING]: Distribution ubuntu 20.04 on host 34.211.146.158 should use /usr/bin/python3, but 
ok: [34.211.146.158]
PLAY RECAP ****************************************************************************************************************
34.211.146.158             : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
52.41.107.116              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```


