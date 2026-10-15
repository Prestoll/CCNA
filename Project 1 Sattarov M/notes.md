P1\_SOHO\_Саттаров

│

├── P1\_SOHO\_Саттаров.pkt

├── README.docx

├── Addressing.xlsx

├── R1\_config.txt

└── S1\_config.txt



**Этап 1. Проектирование**



IPv4:

192.168.10.0/27



Маска:

255.255.255.224



Шлюз:

192.168.10.1



Диапазон:

192.168.10.1 - 192.168.10.30



Broadcast:

192.168.10.31



Причина:

/27 дает 30 рабочих адресов, что достаточно для 25 ПК.



**Этап 2. Базовая настройка R**1



Hostname:

R1



DNS lookup:

Отключен



Команды:

enable

configure terminal

hostname R1

no ip domain-lookup



Router: Cisco 1941



Hostname:

R1



DNS lookup:

Disabled



Пользовательская сеть:

192.168.10.0/27



Шлюз:

192.168.10.1



**Этап 3. Настройка интерфейса LAN**



Интерфейс:

GigabitEthernet0/0



Описание:

LAN\_to\_Switch



IP адрес:

192.168.10.1



Маска:

255.255.255.224 (/27)



Назначение:

Шлюз пользовательской сети



Команды:

interface g0/0

description LAN\_to\_Switch

ip address 192.168.10.1 255.255.255.224

no shutdown



**Этап 4. Базовая настройка S1**



Hostname:

S1



DNS lookup:

Отключен



**Этап 5. Подготовка SSH**



enable secret настроен

локальный пользователь создан

domain-name настроен

RSA ключи созданы



**Этап 6. Настройка SSH доступа**



Domain Name:

soho.local



RSA Key:

1024 bit



SSH Version:

2



VTY Lines:

0-4



Аутентификация:

login local



Разрешенный протокол:

SSH



Запрещенный протокол:

Telnet



Команды:

line vty 0 4

login local

transport input ssh



ip ssh version 2

**Этап 7. Настройка IPv6**



R1:



ipv6 unicast-routing



interface g0/0

ipv6 address 2001:DB8:10::1/64



PC0:



IPv6: 2001:DB8:10::2/64

Gateway: 2001:DB8:10::1



PC1:



IPv6: 2001:DB8:10::3/64

Gateway: 2001:DB8:10::1

**Дополнительно**



На этапе проектирования рассматривался вариант использования VLSM с разделением сети на пользовательскую и management-подсеть.



Пример:



Users:

192.168.10.0/27



Management:

192.168.10.32/29



Для упрощения реализации в рамках первого проекта была использована единая пользовательская подсеть 192.168.10.0/27.



