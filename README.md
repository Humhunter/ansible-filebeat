ansible-filebeat模块
=========

自动化部署filbeat,并加入service模块,可以自动启停,支持动态升级,以及个性化配置文件

Playbook的编写
------------

filebeat.yml (一般放在playbooks目录)

```
---
  - hosts: all
    remote_user: root
    max_fail_percentage: 35 #有35%的服务器执行失败就终止play
    serial: 2  # 两台主机两台主机都执行

    roles:
         - {role: filebeat, filebeat_service_name: "filebeat"} #自定义可以再files文件夹中存放然后在此处定义变量即可
```

## 执行指令

ansible-playbook -i hosts  filebeat.yaml

```
playbook: filebeat.yaml

  play #1 (all): all	TAGS: []
    tasks:
      filebeat : install | Check if filebeat is already exsit.	TAGS: []
      filebeat : install | ensure dictory app	TAGS: []
      filebeat : install | copy tar	TAGS: []
      filebeat : install | link and chown	TAGS: []
      filebeat : configure | create filebeat dir	TAGS: []
      filebeat : configure | copy conf	TAGS: [reload_filebeat]
      filebeat : configure | Setup filebeat init file.	TAGS: []
      filebeat : configure | Ensure filebeat is started and enabled on boot.	TAGS: []
```