# +++++ ANSIBLE  INSTALLATION +++++

#### Update Ubuntu packages
```
$ apt-get update
```

<br />

#### Change hostname
```
$ hostnamectl set-hostname ansible
$ bash
$ hostname
```

<br />


#### Check Ansible version exist or not ?
```
$ ansible --version
```

<br />

#### Install Ansible
```
$ apt install ansible
```

<br />

#### Now check Ansible version
```
$ ansible --version
```

#### Check Ansible client connectivity from Ansible-Master
```
$ ansible -m ping 172.31.86.251


[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match
'all'
[WARNING]: Could not match supplied host pattern, ignoring: 172.31.86.251
```

#### So will add remote host ip to inventory file.
```
$ vim /etc/ansible/hosts

[web]
172.31.86.251
```

#### Check again
```
$ ansible -m ping 172.31.86.251


The authenticity of host '172.31.86.251 (172.31.86.251)' can't be established.
ECDSA key fingerprint is SHA256:3jHr9/45oo/DZ+J0oEXOKCDllhskq9ziYwVaunUExYc.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
172.31.86.251 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '172.31.86.251' (ECDSA) to the list of known hosts.\r\nroot@172.31.86.251: Permission denied (publickey).",
    "unreachable": true
}
```


## ++++++++++++++++++++++++ Remote Host ++++++++++++++++++++++++++

#### Change hostname
```
$ hostnamectl set-hostname client
$ bash
$ hostname
```


#### Enable password Authentication
```
$ cp /etc/ssh/sshd_config /tmp/
$ vim /etc/ssh/sshd_config

PermitRootLogin yes
PasswordAuthentication yes
```

#### Set root user password
```
$ passwd root
```

## ++++++++++++++++++++++++ Ansible Host ++++++++++++++++++++++++++

#### Key generate
```
$ ssh-keygen
```

#### Copy id
```
$ ssh-copy-id root@172.31.86.251
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@172.31.86.251's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@172.31.86.251'"
and check to make sure that only the key(s) you wanted were added.
```

#### Check again, now it should be work.
```
$ ansible -m ping 172.31.86.251


172.31.86.251 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## `*************************   EOF   *************************`
