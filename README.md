**Домашнее задание №2**

**Тема** ***"Автоматизация администрирования. Ansible-1"***

**Задача**
Подготовить стенд на Vagrant как минимум с одним сервером. На этом сервере используя Ansible необходимо развернуть nginx со следующими условиями:

- необходимо использовать модуль yum/apt;
- конфигурационные файлы должны быть взяты из шаблона jinja2 с перемененными;
- после установки nginx должен быть в режиме enabled в systemd;
- должен быть использован notify для старта nginx после установки;
- сайт должен слушать на нестандартном порту - 8080, для этого использовать переменные в Ansible.
---
**Результат выполнения задания**

1. Поднят предоставленный `Vagrantfile`:

```
Last login: Tue Feb 13 12:12:55 2024 from 10.0.2.2
vagrant@nginx:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 02:44:a4:14:45:81 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 metric 100 brd 10.0.2.255 scope global dynamic enp0s3
       valid_lft 83238sec preferred_lft 83238sec
    inet6 fe80::44:a4ff:fe14:4581/64 scope link 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e6:f9:e5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.11.150/24 brd 192.168.11.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fee6:f9e5/64 scope link 
       valid_lft forever preferred_lft forever
vagrant@nginx:~$ 
```

2. На хост установлен пакет Ansible:
```
ansible --version                                                                                                                                                        

ansible 2.10.8
```

3. Созданы inventory, ansible.cfg. Проверен доступ до хоста nginx:


```
ansible nginx -m ping

nginx | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

4. Создан шаблон `nginx.conf.j2`, описывающий конфигурацию веб-сервера nginx
5. Создана роль nginx:
6. Разработаны tasks и handlers, для разворачивания веб-сервера nginx. Запущен playbook:
7. В результате запуска `nginx.yml` развернут сервер веб-сервер nginx:
