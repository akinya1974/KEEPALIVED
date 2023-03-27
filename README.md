# Домашнее задание к занятию 10.1 «Keepalived/vrrp» - `Акиньшин С.Г.`


## Задание 1

1. `Запустил сервис на двух нодах`

### Конфиг на мастер ноде:

```sh
vrrp_instance failover_test {
    state MASTER
    interface enp0s8
    virtual_router_id 10
    priority 110
    advert_int 4
    authentication {
    auth_type PASS
    auth_pass 1111
    }
    unicast_peer {
    192.168.0.1
    }
        virtual_ipaddress {
        192.168.1.50 dev enp0s8 label enp0s8:vip
    }
    }
```

### Конфиг на Backup ноде:

```sh
vrrp_instance failover_test {
    state BACKUP
    interface enp0s8
    virtual_router_id 10
    priority 110
    advert_int 4
    authentication {
    auth_type PASS
    auth_pass 1111
    }
    unicast_peer {
    192.168.0.2
    }
        virtual_ipaddress {
        192.168.1.50 dev enp0s8 label enp0s8:vip
    }
    }

```


![Status](https://github.com/akinya1974/KEEPALIVED/blob/main/JPG/STATUS.jpg)


## Задание 2

1. `Пользоваться Wireshark пока не научился, но сделал тест, который нашел на просторах нета, попеременно выключал и включал сеть в нодах и на оставшейся в сети ноде появлялся вип адрес! Пингуются как вип адрес, созданный  Keepalived так и адрес хоста! Прикольная штука)))`


1. `Вырубил сеть у Мастер ноды (prometheus) вип адресс перешел на Бекап ноду (exporter)`

![JPG](https://github.com/akinya1974/KEEPALIVED/blob/main/JPG/Вырубил%20сеть%20у%20Мастер%20ноды%20(prometheus)%20вип%20адресс%20перешел%20на%20Бекап%20ноду%20(exporter).jpg)


2. `Вырубил сеть у Бекап ноды (exporter) вип адресс перешел на Мастер ноду (prometheus)`

![JPG](https://github.com/akinya1974/KEEPALIVED/blob/main/JPG/Вырубил%20сеть%20у%20букап%20ноды%20(exporter)%20вип%20адресс%20перешел%20на%20Мастер%20ноду%20(prometheus).jpg)