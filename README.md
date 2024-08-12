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

