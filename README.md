# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - Мельник Юрий Александрович

## Подготовка к выполнению заданий


## Задание 1
Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.  

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.  

Просканируйте эту виртуальную машину, используя nmap. 

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.  

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.  

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.  

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

Приведите ответ в свободной форме.

 
## Решение 1 
 
адаптируем Metasploitable для virtual box по инструкции

https://www.cyberithub.com/how-to-install-metasploitable-2-in-virtualbox-using-4-easy-steps/

запускаем
```
nmap -sv -O 192.168.4.78
```
![рис 1](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_1.jpg)
![рис 1](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_2.jpg)

977 портов закрыты - 23 открыты

Службы - ftp, ssh, telnet, smtp, domain, http, rpcbind, netbios-ssn, exec, login,
 tcpwrapped, java-rmi, bindshell, nfs, ftp, mysql, postgresql, vnc, X11, irc, ajp13, http
```
 https://www.exploit-db.com/exploits/17491
 https://www.exploit-db.com/exploits/16922
 https://www.exploit-db.com/exploits/29724
```

## Задание 2
Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.  

Запишите сеансы сканирования в Wireshark.  

Ответьте на следующие вопросы:  

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

Приведите ответ в свободной форме



## Решение 2

1. sudo nmap -sS 192.168.4.78


SYN - Nmap посылает SYN-пакет, как бы намереваясь открыть настоящее соединение, и ожидает ответ. Наличие флагов SYN|ACK в ответе указывает на то, что порт удаленной машины открыт и прослушивается. Флаг RST в ответе означает обратное. Если Nmap принял пакет SYN|ACK, то в ответ немедленно отправляет RST-пакет для сброса еще не установленного соединения

nmap -sS <ip> - TCP SYN сканирование. SYN это используемый по умолчанию и наиболее популярный тип сканирования. 



![рис 3](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_3.jpg)

![рис 4](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_4.jpg)


[Запись сканирования sudo nmap -sS 192.168.4.78](https://github.com/ysatii/attacks-on-is/blob/main/wareshark/1.pcapng)

2. sudo nmap -sF 192.168.4.78
FIN - Nmap посылает FIN-пакет, в TCP заголовок ставится флаг FIN. Согласно RFC 793, на прибывший FIN-пакет на закрытый порт сервер должен ответить пакетом RST. FIN-пакеты на открытые порты должны игнорироваться сервером. По этому различию становится возможным отличить закрытый порт от открытого.

nmap -sF <ip> - FIN сканирование. Устанавливается только TCP FIN бит.

![рис 5](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_5.jpg)

![рис 6](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_6.jpg)


[Запись сканирования sudo nmap -sF 192.168.4.78](https://github.com/ysatii/attacks-on-is/blob/main/wareshark/2.pcapng)


3. sudo nmap -sX 192.168.4.78
Xmas - Устанавливаются FIN, PSH и URG флаги. Если в результате FIN-сканирования мы получили список открытых портов, то это не Windows. Если же все эти методы выдали результат, что все порты закрыты, а SYN-сканирование обнаружило открытые порты, то мы скорей всего имеете дело с ОС Windows, Cisco, BSDI, IRIX, HP/UX и MVS. Все эти ОС не отправляют RST-пакеты.

nmap -sX <ip> - Xmas сканирование. Устанавливаются FIN, PSH и URG флаги.

![рис 7](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_7.jpg)

![рис 8](https://github.com/ysatii/attacks-on-is/blob/main/img/image1_7.jpg)


[Запись сканирования sudo nmap -sX 192.168.4.78](https://github.com/ysatii/attacks-on-is/blob/main/wareshark/3.pcapng)

