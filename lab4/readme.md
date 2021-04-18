![](RackMultipart20210418-4-adk3n9_html_72193920676a741d.png)

**Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах**

# Топология

![](RackMultipart20210418-4-adk3n9_html_9cb25354934b6ea1.png)

# Таблица адресации

| Устройство | Интерфейс | IPv6-адрес | Длина префикса | Шлюз по умолчанию |
| --- | --- | --- | --- | --- |
| R1 | G0/0/0 | 2001:db8:acad:a::1 | 64 | — |
| --- | --- | --- | --- | --- |
| R1 | G0/0/1 | 2001:db8:acad:1::1 | 64 | — |
| S1 | VLAN 1 | 2001:db8:acad:1::b | 64 | — |
| --- | --- | --- | --- | --- |
| PC-A | NIC | 2001:db8:acad:1::3 | 64 | fe80::1 |
| --- | --- | --- | --- | --- |
| PC-B | NIC | 2001:db8:acad:a::3 | 64 | fe80::1 |
| --- | --- | --- | --- | --- |

### Настройте маршрутизатор.

Назначьте имя хоста и настройте основные параметры устройства.

**R1#show running-config**

**Building configuration...**

**Current configuration : 756 bytes**

**version 15.4**

**no service timestamps log datetime msec**

**no service timestamps debug datetime msec**

**service password-encryption**

**hostname R1**

**enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1**

**ip cef**

**no ipv6 cef**

**no ip domain-lookup**

**spanning-tree mode pvst**

**interface GigabitEthernet0/0/0**

**no ip address**

**duplex auto**

**speed auto**

**shutdown**

**interface GigabitEthernet0/0/1**

**no ip address**

**duplex auto**

**speed auto**

**shutdown**

**interface Vlan1**

**no ip address**

**shutdown**

**ip classless**

**ip flow-export version 9**

**banner motd ^Cwarning dager^C**

**line con 0**

**password 7 0822455D0A16**

**login**

**line aux 0**

**line vty 0 4**

**password 7 0822455D0A16**

**login**

**line vty 5 15**

**password 7 0822455D0A16**

**login**

**end**

### Настройте коммутатор.

Назначьте имя хоста и настройте основные параметры устройства.

**Current configuration : 1232 bytes**

**version 15.0**

**no service timestamps log datetime msec**

**no service timestamps debug datetime msec**

**service password-encryption**

**hostname S1**

**enable secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0**

**spanning-tree mode pvst**

**spanning-tree extend system-id**

**interface FastEthernet0/1**

**interface FastEthernet0/2**

**interface FastEthernet0/3**

**interface FastEthernet0/4**

**interface FastEthernet0/5**

**interface FastEthernet0/6**

**interface FastEthernet0/7**

**interface FastEthernet0/8**

**interface FastEthernet0/9**

**interface FastEthernet0/10**

**interface FastEthernet0/11**

**interface FastEthernet0/12**

**interface FastEthernet0/13**

**interface FastEthernet0/14**

**interface FastEthernet0/15**

**interface FastEthernet0/16**

**interface FastEthernet0/17**

**interface FastEthernet0/18**

**interface FastEthernet0/19**

**interface FastEthernet0/20**

**interface FastEthernet0/21**

**interface FastEthernet0/22**

**interface FastEthernet0/23**

**interface FastEthernet0/24**

**interface GigabitEthernet0/1**

**interface GigabitEthernet0/2**

**interface Vlan1**

**no ip address**

**shutdown**

**banner motd ^Cprived danger^C**

**line con 0**

**password 7 0822404F1A0A**

**login**

**line vty 0 4**

**password 7 0822404F1A0A**

**login**

**line vty 5 15**

**password 7 0822404F1A0A**

**login**

**end**

## Ручная настройка IPv6-адресов

### Назначьте IPv6-адреса интерфейсам Ethernet на R1.

      1. Назначьте глобальные индивидуальные IPv6-адреса, указанные в таблице адресации обоим интерфейсам Ethernet на R1.

Откройте окно конфигурации

      1. Введите команду show ipv6 interface brief, чтобы проверить, назначен ли каждому интерфейсу корректный индивидуальный IPv6-адрес.

**R1#show ipv6 interface brief**

**GigabitEthernet0/0/0 [up/up]**

**FE80::202:17FF:FEA3:9C01**

**2001:DB8:ACAD:A::1**

**GigabitEthernet0/0/1 [up/up]**

**FE80::202:17FF:FEA3:9C02**

**2001:DB8:ACAD:1::1**

Примечание **. Отображаемый локальный адрес канала основан на адресации EUI-64, которая автоматически использует MAC-адрес интерфейса для создания 128-битного локального IPv6-адреса канала.**

      1. Чтобы обеспечить соответствие локальных адресов канала индивидуальному адресу, вручную введите локальные адреса канала на каждом интерфейсе Ethernet на R1.

**Примечание**. Каждый интерфейс маршрутизатора относится к отдельной сети. Пакеты с локальным адресом канала никогда не выходят за пределы локальной сети, а значит, для обоих интерфейсов можно указывать один и тот же локальный адрес канала.

      1. Используйте выбранную команду, чтобы убедиться, что локальный адрес связи изменен на fe80::1.

**R1#show ipv6 interface brief**

**GigabitEthernet0/0/0 [up/up]**

**FE80::1**

**2001:DB8:ACAD:A::1**

**GigabitEthernet0/0/1 [up/up]**

**FE80::1**

**2001:DB8:ACAD:1::1**

Закройте окно настройки.

#### Вопрос:

Какие группы многоадресной рассылки назначены интерфейсу G0/0?

**Ответ**** : Global unicast address(es):**

**2001:DB8:ACAD:A::1, subnet is 2001:DB8:ACAD:A::/64**

    1.
### Активируйте IPv6-маршрутизацию на R1.

     
    1. В командной строке на PC-B введите команду **ipconfig** , чтобы получить данные IPv6-адреса, назначенного интерфейсу ПК.

**FastEthernet0 Connection:(default port)**
**Connection-specific DNS Suffix..:**
**Link-local IPv6 Address.........: FE80::2D0:FFFF:FEAB:EE8A**
**IPv6 Address....................: ::**
**IPv4 Address....................: 0.0.0.0**
**Subnet Mask.....................: 0.0.0.0**
**Default Gateway.................: ::**
**0.0.0.0**

#### Вопрос:

Назначен ли индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) на PC-B?

**Ответ**** : **** нет не назначен**

      1. Активируйте IPv6-маршрутизацию на R1 с помощью команды **IPv6 unicast-routing**.

, чтобы убедиться, что новая многоадресная группа назначена интерфейсу G0/0/0. Обратите внимание, что в списке групп для интерфейса G0/0 отображается группа многоадресной рассылки всех маршрутизаторов (FF02::2).

**Примечание**. Это позволит компьютерам получать IP-адреса и данные шлюза по умолчанию с помощью функции SLAAC (Stateless Address Autoconfiguration (Автоконфигурация без сохранения состояния адреса)).

      1. Теперь, когда R1 входит в группу многоадресной рассылки всех маршрутизаторов, еще раз введите команду **ipconfig** на PC-B. Проверьте данные IPv6-адреса.

 C:\ipconfig**

**FastEthernet0 Connection:(default port)**

**Connection-specific DNS Suffix..:**

**Link-local IPv6 Address.........: FE80::2D0:FFFF:FEAB:EE8A**

**IPv6 Address....................: 2001:DB8:ACAD:A:2D0:FFFF:FEAB:EE8A**

**IPv4 Address....................: 0.0.0.0**

** ubnet Mask.....................: 0.0.0.0**

**Default Gateway.................: FE80::1**

**0.0.0.0**

#### Вопрос:

Почему PC-B получил глобальный префикс маршрутизации и идентификатор подсети, которые вы настроили на R1?

**Ответ: Компьютер входит в группу многоадресной рассылки**

    1.
### Назначьте IPv6-адреса интерфейсу управления (SVI) на S1.

      1. Назначьте адрес IPv6 для S1. Также назначьте этому интерфейсу локальный адрес канала.
      2. Проверьте правильность назначения IPv6-адресов интерфейсу управления с помощью команды show ipv6 interface vlan1.

**Vlan1 is administratively down, line protocol is down**

**IPv6 is tentative, link-local address is FE80::1 [TEN]**

**No Virtual link-local address(es):**

**Global unicast address(es):**

**2001:DB8:ACAD:1::B, subnet is 2001:DB8:ACAD:1::/64 [TEN]**

**Joined group address(es):**

**FF02::1**

**MTU is 1500 bytes**

**ICMP error messages limited to one every 100 milliseconds**

**ICMP redirects are enabled**

**ICMP unreachables are sent**

**Output features: Check hwidb**

**ND DAD is enabled, number of DAD attempts: 1**

**ND reachable time is 30000 milliseconds**

**ND NS retransmit interval is 1000 milliseconds**

Закройте окно настройки.

### Назначьте компьютерам статические IPv6-адреса.

      1. Откройте окно Свойства Ethernet для каждого ПК и назначьте адресацию IPv6.
      2. Убедитесь, что оба компьютера имеют правильную информацию адреса IPv6. Каждый компьютер должен иметь два глобальных адреса IPv6: один статический и один SLACC

## Проверка сквозного подключения

С PC-A отправьте эхо-запрос на **FE80::1**. Это локальный адрес канала, назначенный G0/1 на R1.

![image](https://user-images.githubusercontent.com/80053204/115149473-0030a700-a06d-11eb-934d-0b0f433d5363.png)

Отправьте эхо-запрос на интерфейс управления S1 с PC-A.

![image](https://user-images.githubusercontent.com/80053204/115149482-0de62c80-a06d-11eb-9f6c-9b069f978c46.png)

Введите команду **tracert** на PC-A, чтобы проверить наличие сквозного подключения к PC-B.

![image](https://user-images.githubusercontent.com/80053204/115149504-1fc7cf80-a06d-11eb-9d97-0214810c75a3.png)

С PC-B отправьте эхо-запрос на PC-A.

![image](https://user-images.githubusercontent.com/80053204/115149514-29e9ce00-a06d-11eb-9c00-a8d687d1b37c.png)

С PC-B отправьте эхо-запрос на локальный адрес канала G0/0 на R1.

![image](https://user-images.githubusercontent.com/80053204/115149844-8dc0c680-a06e-11eb-981d-6ea885a3293e.png)

**Примечание.** В случае отсутствия сквозного подключения проверьте, правильно ли указаны IPv6-адреса на всех устройствах.

# Вопросы для повторения

  1. Почему обоим интерфейсам Ethernet на R1 можно назначить один и тот же локальный адрес канала — FE80::1?

**Ответ:**  **Каждый**  **интерфейс маршрутизатора находится в отдельной сети. Пакеты с локальным адресом канала никогда не покидают локальную сеть, а значит, для обоих интерфейсов можно указывать один и тот же локальный адрес канала**

  1. Какой идентификатор подсети в индивидуальном IPv6-адресе 2001:db8:acad::aaaa:1234/64?

**Ответ**** : **** 2001:db8:acad**

©  2013 г. - гггг Корпорация Cisco и/или ее дочерние компании. Все права защищены. Открытая информация Cisco страница **1**** 11**www.netacad.com
