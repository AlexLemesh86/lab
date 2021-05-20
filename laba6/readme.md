![](RackMultipart20210512-4-yrxry6_html_72193920676a741d.png)

**Лабораторная работа - Внедрение маршрутизации между виртуальными локальными сетями**

# Топология

![image](https://user-images.githubusercontent.com/80053204/118016868-9a2efb00-b35e-11eb-811b-d9c8b4ec1e6e.png)

# Таблица адресации

|

Устройство

 |

Интерфейс

 |

IP-адрес

 |

Маска подсети

 |

Шлюз по умолчанию

 |
| --- | --- | --- | --- | --- |
| R1 | G0/0/1.10 | 192.168.10.1 | 255.255.255.0 | — |
| --- | --- | --- | --- | --- |
| R1 | G0/0/1.20 | 192.168.20.1 | 255.255.255.0 | — |
| R1 | G0/0/1.30 | 192.168.30.1 | 255.255.255.0 | — |
| R1 | G0/0/1.1000 | — | — | — |
| S1 | VLAN 10 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| --- | --- | --- | --- | --- |
| S2 | VLAN 10 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| --- | --- | --- | --- | --- |
| PC-A | NIC | 192.168.20.3 | 255.255.255.0 | 192.168.20.1 |
| --- | --- | --- | --- | --- |
| PC-B | NIC | 192.168.30.3 | 255.255.255.0 | 192.168.30.1 |
| --- | --- | --- | --- | --- |

# Таблица VLAN

![image](https://user-images.githubusercontent.com/80053204/118018356-589f4f80-b360-11eb-8f37-10c1cda93378.png)
c

# Задачи

**Часть 1. Создание сети и настройка основных параметров устройства**

**Часть 2. Создание сетей VLAN и назначение портов коммутатора**

**Часть 3. Настройка транка 802.1Q между коммутаторами.**

**Часть 4. Настройка маршрутизации между сетями VLAN**

**Часть 5. Проверка, что маршрутизация между VLAN работает**

# Общие сведения/сценарий

В целях повышения производительности сети большие широковещательные домены 2-го уровня делят на домены меньшего размера. Для этого современные коммутаторы используют виртуальные локальные сети (VLAN). VLAN также можно использовать в качестве меры безопасности, отделяя конфиденциальный трафик данных от остальной части сети. Сети VLAN облегчают процесс проектирования сети, обеспечивающей помощь в достижении целей организации. Для связи между VLAN требуется устройство, работающее на уровне 3 модели OSI. Добавление маршрутизации между VLAN позволяет организации разделять и разделять широковещательные домены, одновременно позволяя им обмениваться данными друг с другом.

Транковые каналы сети VLAN используются для распространения сетей VLAN по различным устройствам. Транковые каналы разрешают передачу трафика из множества сетей VLAN через один канал, не нанося вред идентификации и сегментации сети VLAN. Особый вид маршрутизации между VLAN, называемый «Router-on-a-Stick», использует магистраль от маршрутизатора к коммутатору, чтобы все VLAN могли переходить к маршрутизатору.

В этой лабораторной работе вы создадите VLAN на обоих коммутаторах в топологии, назначите VLAN для коммутации портов доступа, убедитесь, что VLAN работают должным образом, создадите транки VLAN между двумя коммутаторами и между S1 и R1, и настройте маршрутизацию между VLAN на R1 для разрешения связи между хостами в разных VLAN независимо от подсети, в которой находится хост.

**Примечание** : Маршрутизаторы, используемые в практических лабораторных работах CCNA, - это Cisco 4221 с Cisco IOS XE Release 16.9.4 (образ universalk9). В лабораторных работах используются коммутаторы Cisco Catalyst 2960 с Cisco IOS версии 15.2(2) (образ lanbasek9). Можно использовать другие маршрутизаторы, коммутаторы и версии Cisco IOS. В зависимости от модели устройства и версии Cisco IOS доступные команды и результаты их выполнения могут отличаться от тех, которые показаны в лабораторных работах. Правильные идентификаторы интерфейса см. в сводной таблице по интерфейсам маршрутизаторов в конце лабораторной работы.

**Примечание.** Убедитесь, что у всех маршрутизаторов и коммутаторов была удалена начальная конфигурация. Если вы не уверены в этом, обратитесь к инструктору.

# Необходимые ресурсы

- 1 Маршрутизатор (Cisco 4221 с универсальным образом Cisco IOS XE версии 16.9.4 или аналогичным)
- 2 коммутатора (Cisco 2960 с операционной системой Cisco IOS 15.2(2) (образ lanbasek9) или аналогичная модель)
- 2 ПК (ОС Windows с программой эмуляции терминалов, такой как Tera Term)
- Консольные кабели для настройки устройств Cisco IOS через консольные порты.
- Кабели Ethernet, расположенные в соответствии с топологией

# Инструкции

## Создание сети и настройка основных параметров устройства

В первой части лабораторной работы вам предстоит создать топологию сети и настроить базовые параметры для узлов ПК и коммутаторов.

### Создайте сеть согласно топологии.

Подключите устройства, как показано в топологии, и подсоедините необходимые кабели.

![image](https://user-images.githubusercontent.com/80053204/118016983-b9c62380-b35e-11eb-971d-cd6352140161.png)

### Настройте базовые параметры для маршрутизатора.

      1. Подключитесь к маршрутизатору с помощью консоли и активируйте привилегированный режим EXEC.

Откройте окно конфигурации

      1. Войдите в режим конфигурации.
      2. Назначьте маршрутизатору имя устройства.
      3. Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
      4. Назначьте **class** в качестве зашифрованного пароля привилегированного режима EXEC.
      5. Назначьте **cisco** в качестве пароля консоли и включите вход в систему по паролю.
      6. Установите **cisco** в качестве пароля виртуального терминала и активируйте вход.
      7. Зашифруйте открытые пароли.
      8. Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
      9. Сохраните текущую конфигурацию в файл загрузочной конфигурации.
      10. Настройте на маршрутизаторе время.

Закройте окно настройки.

### Настройте базовые параметры каждого коммутатора.

      1. Присвойте коммутатору имя устройства.
      2. Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
      3. Назначьте **class** в качестве зашифрованного пароля привилегированного режима EXEC.
      4. Назначьте **cisco** в качестве пароля консоли и включите вход в систему по паролю.
      5. Установите **cisco** в качестве пароля виртуального терминала и активируйте вход.
      6. Зашифруйте открытые пароли.
      7. Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
      8. Настройте на коммутаторах время.
      9. Сохранение текущей конфигурации в качестве начальной.

Закройте окно настройки.

### Настройте узлы ПК.

Адреса ПК можно посмотреть в таблице адресации.

## Создание сетей VLAN и назначение портов коммутатора

Во второй части вы создадите VLAN, как указано в таблице выше, на обоих коммутаторах. Затем вы назначите VLAN соответствующему интерфейсу и проверите настройки конфигурации. Выполните следующие задачи на каждом коммутаторе.

### Создайте сети VLAN на коммутаторах.

      1. Создайте и назовите необходимые VLAN на каждом коммутаторе из таблицы выше.

![image](https://user-images.githubusercontent.com/80053204/118017111-e24e1d80-b35e-11eb-9fcf-320ec7c6248b.png)

Откройте окно конфигурации

      1. Настройте интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации.

![image](https://user-images.githubusercontent.com/80053204/118017225-0873bd80-b35f-11eb-9546-e8f141ff6c39.png)


![image](https://user-images.githubusercontent.com/80053204/118017244-0dd10800-b35f-11eb-97ef-3902906deeab.png)

      1. Назначьте все неиспользуемые порты коммутатора VLAN Parking\_Lot, настройте их для статического режима доступа и административно деактивируйте их.

![image](https://user-images.githubusercontent.com/80053204/118017302-1f1a1480-b35f-11eb-8f56-028fd450fc27.png)

![image](https://user-images.githubusercontent.com/80053204/118017338-28a37c80-b35f-11eb-8671-274684a40ae6.png)

### Назначьте сети VLAN соответствующим интерфейсам коммутатора.

      1. Назначьте используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настройте их для режима статического доступа.

![image](https://user-images.githubusercontent.com/80053204/118017399-3e18a680-b35f-11eb-8a64-e1fb7d996dcf.png)

![image](https://user-images.githubusercontent.com/80053204/118017426-453fb480-b35f-11eb-9250-ecc7a0a30b24.png)

Закройте окно настройки.

## Конфигурация магистрального канала стандарта 802.1Q между коммутаторами

В части 3 вы вручную настроите интерфейс F0/1 как транк.

### Вручную настройте магистральный интерфейс F0/1 на коммутаторах S1 и S2.

      1. Настройка статического транкинга на интерфейсе F0/1 для обоих коммутаторов.

Откройтеокноконфигурации

      1. Установите native VLAN 1000 на обоих коммутаторах.

![image](https://user-images.githubusercontent.com/80053204/118017496-5e486580-b35f-11eb-8613-851ccf2488ea.png)

![image](https://user-images.githubusercontent.com/80053204/118017517-656f7380-b35f-11eb-8f58-e965492c3fff.png)

      1. Укажите, что VLAN 10, 20, 30 и 1000 могут проходить по транку.

![image](https://user-images.githubusercontent.com/80053204/118017559-702a0880-b35f-11eb-8716-335969d51a02.png)

![image](https://user-images.githubusercontent.com/80053204/118017580-761fe980-b35f-11eb-805a-8f87d01d5f6d.png)


      1. Проверьте транки, native VLAN и разрешенные VLAN через транк.

![image](https://user-images.githubusercontent.com/80053204/118017618-81731500-b35f-11eb-85d5-5d796fd9adbd.png)


### Вручную настройте магистральный интерфейс F0/5 на коммутаторе S1.

      1. Настройте интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.

![image](https://user-images.githubusercontent.com/80053204/118017675-9354b800-b35f-11eb-9bb5-3a594020428f.png)

      1. Сохраните текущую конфигурацию в файл загрузочной конфигурации.

![image](https://user-images.githubusercontent.com/80053204/118017729-9ea7e380-b35f-11eb-86a3-092de7129080.png)


      1. Проверка транкинга.

#### Вопрос:

Что произойдет, если G0/0/1 на R1 будет отключен?

**Ответ: перестанет работать маршрутизация**

Закройте окно настройки.

## Настройка маршрутизации между сетями VLAN

### Настройте маршрутизатор.

Откройте окно конфигурации

      1. При необходимости активируйте интерфейс G0/0/1 на маршрутизаторе.

![image](https://user-images.githubusercontent.com/80053204/118017809-b3847700-b35f-11eb-95fc-601900d002a2.png)

      1. Настройте подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. Убедитесь, что подинтерфейсу для native VLAN не назначен IP-адрес. Включите описание для каждого подинтерфейса.

![image](https://user-images.githubusercontent.com/80053204/118017853-bf703900-b35f-11eb-89e5-26a773480bc3.png)

      1. Убедитесь, что вспомогательные интерфейсы работают

Закройте окно настройки.

## Проверьте, работает ли маршрутизация между VLAN

### Выполните следующие тесты с PC-A. Все должно быть успешно.

**Примечание.** Возможно, вам придется отключить брандмауэр ПК для работы ping

      1. Отправьте эхо-запрос с PC-A на шлюз по умолчанию.

![image](https://user-images.githubusercontent.com/80053204/118017955-df076180-b35f-11eb-86a6-038f97fb7209.png)

      1. Отправьте эхо-запрос с PC-A на PC-B.

![image](https://user-images.githubusercontent.com/80053204/118017999-e890c980-b35f-11eb-8ce6-487d228ae8c0.png)

      1. Отправьте команду ping с компьютера PC-A на коммутатор S2.

![image](https://user-images.githubusercontent.com/80053204/118018052-f6464f00-b35f-11eb-9a06-9774678c92de.png)


### Пройдите следующий тест с PC-B

В окне командной строки на PC-B выполните команду **tracert** на адрес PC-A.

![image](https://user-images.githubusercontent.com/80053204/118018095-052d0180-b360-11eb-9a44-8af8787f72af.png)

#### Вопрос:

Какие промежуточные IP-адреса отображаются в результатах?

**Ответ**** : **** Адрес виртуального интерфейса 192 ****.168.30.1**

©  2019 г. - гггг Корпорация Cisco и/или ее дочерние компании. Все права защищены. Открытая информация Cisco страница **1**** 7**www.netacad.com