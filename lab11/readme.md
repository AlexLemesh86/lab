

Лабораторная работа - Конфигурация безопасности коммутатора

# Топология

![image](https://user-images.githubusercontent.com/80053204/124435800-0259f600-dd7e-11eb-9d80-e03a584cb816.png)

# Таблица адресации

| Устройство | interface/vlan | IP-адрес | Маска подсети |
| --- | --- | --- | --- |
| R1 | G0/0/1 | 192.168.10.1 | 255.255.255.0 |
| --- | --- | --- | --- |
| R1 | Loopback 0 | 10.10.1.1 | 255.255.255.0 |
| S1 | VLAN 10 | 192.168.10.201 | 255.255.255.0 |
| --- | --- | --- | --- |
| S2 | VLAN 10 | 192.168.10.202 | 255.255.255.0 |
| --- | --- | --- | --- |
| PC A | NIC | DHCP | 255.255.255.0 |
| --- | --- | --- | --- |
| PC B | NIC | DHCP | 255.255.255.0 |
| --- | --- | --- | --- |

# Цели

**Часть 1. Настройка основного сетевого устройства**

- Создайте сеть.
- Настройте маршрутизатор R1.
- Настройка и проверка основных параметров коммутатора

**Часть 2. Настройка сетей VLAN**

- Сконфигруриуйте VLAN 10.
- Сконфигруриуйте SVI для VLAN 10.
- Настройте VLAN 333 с именем Native на S1 и S2.
- Настройте VLAN 999 с именем ParkingLot на S1 и S2.

**Часть 3: Настройки безопасности коммутатора.**

- Реализация магистральных соединений 802.1Q.
- Настройка портов доступа
- Безопасность неиспользуемых портов коммутатора
- Документирование и реализация функций безопасности порта.
- Реализовать безопасность DHCP snooping .
- Реализация PortFast и BPDU Guard
- Проверка сквозной связанности.

# Общие сведения и сценарий

Это комплексная лабораторная работа, нацеленная на повторение ранее изученных функций безопасности уровня 2.

**Примечание** : Маршрутизаторы, используемые в практических лабораторных работах CCNA, - это Cisco 4221 с Cisco IOS XE Release 16.9.3 (образ universalk9). В лабораторных работах используются коммутаторы Cisco Catalyst 2960 с Cisco IOS версии 15.0(2) (образ lanbasek9). Можно использовать другие маршрутизаторы, коммутаторы и версии Cisco IOS. В зависимости от модели устройства и версии Cisco IOS доступные команды и результаты их выполнения могут отличаться от тех, которые показаны в лабораторных работах. Правильные идентификаторы интерфейса см. в сводной таблице по интерфейсам маршрутизаторов в конце лабораторной работы.

**Примечание** : Убедитесь, что все настройки коммутатора удалены и загрузочная конфигурация отсутствует. Если вы не уверены, обратитесь к инструктору.

# Необходимые ресурсы

- 1 Маршрутизатор (Cisco 4221 с универсальным образом Cisco IOS XE версии 16.9.3 или аналогичным)
- 2 коммутатора (Cisco 2960 с операционной системой Cisco IOS 15.0(2) (образ lanbasek9) или аналогичная модель)
- 2 ПК (ОС Windows с программой эмуляции терминалов, такой как Tera Term)
- Консольные кабели для настройки устройств Cisco IOS через консольные порты.
- Кабели Ethernet, расположенные в соответствии с топологией

# Инструкции

## Настройка основного сетевого устройства

### Создайте сеть.

1. Создайте сеть согласно топологии.
2. Инициализация устройств

### Настройте маршрутизатор R1.

      1. Загрузите следующий конфигурационный скрипт на R1.

Откройтеокноконфигурации

![image](https://user-images.githubusercontent.com/80053204/124435971-33d2c180-dd7e-11eb-9482-b6d3fe67121b.png)

![image](https://user-images.githubusercontent.com/80053204/124436015-3b926600-dd7e-11eb-9899-51e5c2953cec.png)

Проверьте текущую конфигурацию на R1, используя следующую команду:

R1# **show**** ip ****interface**** brief**

1. Убедитесь, что IP-адресация и интерфейсы находятся в состоянии up / up (при необходимости устраните неполадки).

![image](https://user-images.githubusercontent.com/80053204/124436049-43eaa100-dd7e-11eb-9486-165845e96dca.png)

Закройте окно настройки.

### Настройка и проверка основных параметров коммутатора

      1. Настройте имя хоста для коммутаторов S1 и S2.

![image](https://user-images.githubusercontent.com/80053204/124436183-67ade700-dd7e-11eb-86eb-85ffc327001a.png)

![image](https://user-images.githubusercontent.com/80053204/124436239-709eb880-dd7e-11eb-872e-a3c178d1d1df.png)

Откройте окно конфигурации

      1. Запретите нежелательный поиск в DNS.

![image](https://user-images.githubusercontent.com/80053204/124436280-78f6f380-dd7e-11eb-8d62-7f12c7a6caea.png)

![image](https://user-images.githubusercontent.com/80053204/124436323-8318f200-dd7e-11eb-8543-ad0a9bbff1b5.png)

      1. Настройте описания интерфейса для портов, которые используются в S1 и S2.

![image](https://user-images.githubusercontent.com/80053204/124436374-8d3af080-dd7e-11eb-9699-412c1601d5b9.png)

![image](https://user-images.githubusercontent.com/80053204/124436395-9330d180-dd7e-11eb-94f2-11c160a3758a.png)

      1. Установите для шлюза по умолчанию для VLAN управления значение 192.168.10.1 на обоих коммутаторах.

![image](https://user-images.githubusercontent.com/80053204/124436430-9d52d000-dd7e-11eb-8e6f-be1b0bcde14a.png)

![image](https://user-images.githubusercontent.com/80053204/124436457-a5ab0b00-dd7e-11eb-8d54-93e5eaf8ec9b.png)

## Настройка сетей VLAN на коммутаторах.

### Сконфигруриуйте VLAN 10.

Добавьте VLAN 10 на S1 и S2 и назовите VLAN - **Management.**

![image](https://user-images.githubusercontent.com/80053204/124436513-b78cae00-dd7e-11eb-86bf-6ff6a1897045.png)

![image](https://user-images.githubusercontent.com/80053204/124436535-bce9f880-dd7e-11eb-934a-a90dacdb4d3f.png)

### Сконфигруриуйте SVI для VLAN 10.

Настройте IP-адрес в соответствии с таблицей адресации для SVI для VLAN 10 на S1 и S2. Включите интерфейсы SVI и предоставьте описание для интерфейса.

![image](https://user-images.githubusercontent.com/80053204/124436612-cecb9b80-dd7e-11eb-96f4-baae96fad38c.png)

![image](https://user-images.githubusercontent.com/80053204/124436714-eefb5a80-dd7e-11eb-9555-6bf4242828d9.png)


### Настройте VLAN 333 с именем Native на S1 и S2.

![image](https://user-images.githubusercontent.com/80053204/124436754-fc184980-dd7e-11eb-9bd5-445d119ac399.png)

![image](https://user-images.githubusercontent.com/80053204/124436779-02a6c100-dd7f-11eb-8d61-d608d40e3559.png)

### Настройте VLAN 999 с именем ParkingLot на S1 и S2.

![image](https://user-images.githubusercontent.com/80053204/124436812-0cc8bf80-dd7f-11eb-9dd3-d0eee2a29505.png)

![image](https://user-images.githubusercontent.com/80053204/124436829-13efcd80-dd7f-11eb-8fa5-6c856a9ae1b4.png)

## Настройки безопасности коммутатора.

### Релизация магистральных соединений 802.1Q.

      1. Настройте все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.

![image](https://user-images.githubusercontent.com/80053204/124436907-28cc6100-dd7f-11eb-8800-8cbe10db7e33.png)

![image](https://user-images.githubusercontent.com/80053204/124436920-2d911500-dd7f-11eb-9e65-4bab10aa97a6.png)

      1. Убедитесь, что режим транкинга успешно настроен на всех коммутаторах.

![image](https://user-images.githubusercontent.com/80053204/124436955-37b31380-dd7f-11eb-9110-d01649d94231.png)

![image](https://user-images.githubusercontent.com/80053204/124436997-43063f00-dd7f-11eb-8a31-ec8449b41737.png)

      1. Отключить согласование DTP F0/1 на S1 и S2.

![image](https://user-images.githubusercontent.com/80053204/124437035-4e596a80-dd7f-11eb-8f98-2f55d53b2fb6.png)

![image](https://user-images.githubusercontent.com/80053204/124437057-544f4b80-dd7f-11eb-8644-61f5cbd0881c.png)

      1. Проверьте с помощью команды **show interfaces**.

![image](https://user-images.githubusercontent.com/80053204/124437436-bc059680-dd7f-11eb-9c02-adfcc8c19ff1.png)

### Настройка портов доступа

      1. На S1 настройте F0/5 и F0/6 в качестве портов доступа и свяжите их с VLAN 10.

![image](https://user-images.githubusercontent.com/80053204/124437507-ce7fd000-dd7f-11eb-8792-ff5ac99747d6.png)

      1. На S2 настройте порт доступа Fa0/18 и свяжите его с VLAN 10.

![image](https://user-images.githubusercontent.com/80053204/124437532-d5a6de00-dd7f-11eb-91c1-5118335bfdd5.png)

### Безопасность неиспользуемых портов коммутатора

      1. На S1 и S2 переместите неиспользуемые порты из VLAN 1 в VLAN 999 и отключите неиспользуемые порты.

![image](https://user-images.githubusercontent.com/80053204/124437593-e35c6380-dd7f-11eb-92f6-8516fc07d5ac.png)

![image](https://user-images.githubusercontent.com/80053204/124437616-e9524480-dd7f-11eb-84ce-2527e27661fe.png)

      1. Убедитесь, что неиспользуемые порты отключены и связаны с VLAN 999, введя команду **show**.

![image](https://user-images.githubusercontent.com/80053204/124437659-f3744300-dd7f-11eb-8112-192b60177b69.png)

![image](https://user-images.githubusercontent.com/80053204/124437689-fb33e780-dd7f-11eb-92ec-1a80071e4d88.png)

### Документирование и реализация функций безопасности порта.

Интерфейсы F0/6 на S1 и F0/18 на S2 настроены как порты доступа. На этом шаге вы также настроите безопасность портов на этих двух портах доступа.

      1. На S1, введите команду **show port-security interface f0/6** для отображения настроек по умолчанию безопасности порта для интерфейса F0/6. Запишите свои ответы ниже.

|

Конфигурация безопасности порта по умолчанию

 |
| --- |
|

Функция

 |

Настройка по умолчанию

 |
| --- | --- |
| Защита портов | Disabled |
| --- | --- |
| Максимальное количество записей MAC-адресов | 1 |
| Режим проверки на нарушение безопасности | Shutdown |
| Aging Time | 0 mins |
| Aging Type | Absolute |
| Secure Static Address Aging | Disabled |
| Sticky MAC Address | 0 |

      1. На S1 включите защиту порта на F0 / 6 со следующими настройками:

- Максимальное количество записей MAC-адресов: **3**
- Режим безопасности: **restrict**
- Aging time: **60 мин.**
- Aging type: **неактивный**

      1. Verify port security on S1 F0/6.

![image](https://user-images.githubusercontent.com/80053204/124437873-30d8d080-dd80-11eb-8dac-52d6ce0008fa.png)

![image](https://user-images.githubusercontent.com/80053204/124437893-36361b00-dd80-11eb-97f1-6fd8982d303b.png)

      1. Включите безопасность порта для F0 / 18 на S2. Настройте каждый активный порт доступа таким образом, чтобы он автоматически добавлял адреса МАС, изученные на этом порту, в текущую конфигурацию.

![image](https://user-images.githubusercontent.com/80053204/124437923-3e8e5600-dd80-11eb-9dd1-d479a2b162cd.png)

      1. Настройте следующие параметры безопасности порта на S2 F / 18:

- Максимальное количество записей MAC-адресов: **2**
- Тип безопасности: **Protect**
- Aging time: **60 мин.**

![image](https://user-images.githubusercontent.com/80053204/124437975-4cdc7200-dd80-11eb-91e2-967921469448.png)

      1. Проверка функции безопасности портов на S2 F0/18.

![image](https://user-images.githubusercontent.com/80053204/124438001-5534ad00-dd80-11eb-8445-518ffd77939c.png)

![image](https://user-images.githubusercontent.com/80053204/124438116-77c6c600-dd80-11eb-9278-8319c4acc591.png)


Реализовать безопасность DHCP snooping.

      1. На S2 включите DHCP snooping и настройте DHCP snooping во VLAN 10.

![image](https://user-images.githubusercontent.com/80053204/124438157-83b28800-dd80-11eb-9f81-2c05b096faf1.png)

      1. Настройте магистральные порты на S2 как доверенные порты.

![image](https://user-images.githubusercontent.com/80053204/124438174-89a86900-dd80-11eb-8c4f-da333bea4f48.png)

      1. Ограничьте ненадежный порт Fa0/18 на S2 пятью DHCP-пакетами в секунду.

![image](https://user-images.githubusercontent.com/80053204/124438191-8f05b380-dd80-11eb-9e92-0489025b3dfa.png)

      1. Проверка DHCP Snooping на S2.

![image](https://user-images.githubusercontent.com/80053204/124438229-9927b200-dd80-11eb-884c-0a98acc769e9.png)

      1. В командной строке на PC-B освободите, а затем обновите IP-адрес.

C:\Users\Student\&gt; **ipconfig /release**

C:\Users\Student\&gt; **ipconfig /renew**

      1. Проверьтепривязкуотслеживания DHCP спомощьюкоманды **show ip dhcp snooping binding**.

![image](https://user-images.githubusercontent.com/80053204/124438256-a3e24700-dd80-11eb-803f-dc03fa465c0b.png)

### Реализация PortFast и BPDU Guard

      1. Настройте PortFast на всех портах доступа, которые используются на обоих коммутаторах.

![image](https://user-images.githubusercontent.com/80053204/124438305-b0ff3600-dd80-11eb-8212-5d05ab368d3a.png)

![image](https://user-images.githubusercontent.com/80053204/124438318-b65c8080-dd80-11eb-81f9-b0a5100b4271.png)

      1. Включите защиту BPDU на портах доступа VLAN 10 S1 и S2, подключенных к PC-A и PC-B.

![image](https://user-images.githubusercontent.com/80053204/124438435-dab85d00-dd80-11eb-8d23-538bd4b03c53.png)

![image](https://user-images.githubusercontent.com/80053204/124438460-e3a92e80-dd80-11eb-9ab7-0b1a1f15eeb2.png)

      1. Убедитесь, что защита BPDU и PortFast включены на соответствующих портах.

![image](https://user-images.githubusercontent.com/80053204/124438494-edcb2d00-dd80-11eb-87d0-8716ed4c4bb5.png)

### Проверьте наличие сквозного ⁪подключения.

Проверьте PING свзяь между всеми устройствами в таблице IP-адресации. В случае сбоя проверки связи может потребоваться отключить брандмауэр на хостах.

![image](https://user-images.githubusercontent.com/80053204/124438530-f885c200-dd80-11eb-9800-2925ec8d6c29.png)

![image](https://user-images.githubusercontent.com/80053204/124438563-02a7c080-dd81-11eb-8224-fa5b2a9b786b.png)

Закройте окно настройки.

