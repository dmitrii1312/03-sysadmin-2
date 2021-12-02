# 03-sysadmin-2

## 1  тип команды cd

	vagrant@ubuntu-20:~$ type cd
	cd is a shell builtin

## 2 альтернатива без pipe команде grep <some_string> <some_file> | wc -l
	grep -с <some_string> <some_file>
	
## 3 процесс с PID 1

В виртуальной машине Ubuntu 20.04:
	vagrant@ubuntu-20:~$ ps -axo ppid,pid,cmd|awk '$1=="1" || $2=="1" {print $0}'
	      0       1 /sbin/init
	      1     410 /lib/systemd/systemd-journald
	      1     434 /lib/systemd/systemd-udevd
	      1     435 /lib/systemd/systemd-networkd
	      1     478 /usr/lib/linux-tools/5.4.0-37-generic/hv_kvp_daemon -n
	      1     581 /sbin/multipathd -d -s
	      1     668 /lib/systemd/systemd-resolved
	      1     671 /usr/lib/accountsservice/accounts-daemon
	      1     672 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
	      1     679 /usr/lib/linux-tools/5.4.0-37-generic/hv_vss_daemon -n
	      1     684 /usr/sbin/irqbalance --foreground
	      1     688 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
	      1     690 /usr/sbin/rsyslogd -n -iNONE
	      1     695 /lib/systemd/systemd-logind
	      1     740 /usr/lib/policykit-1/polkitd --no-debug
	      1     782 /usr/sbin/cron -f
	      1     785 /usr/sbin/atd -f
	      1     793 /usr/sbin/ntpd -p /var/run/ntpd.pid -g -u 111:118
	      1     798 /sbin/agetty -o -p -- \u --noclear tty1 linux
	      1     799 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
	      1    1461 /lib/systemd/systemd --user

## 4 команда, которая перенаправит вывод stderr ls на другую сессию терминала?
	ls 2> /dev/pts/x
	
## 5 одновременно передать команде файл на stdin и вывести ее stdout в другой файл
Получится:
	
	grep string < filein > fileout
	
## 6 Получится ли находясь в графическом режиме, вывести данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?

Получится под root. Наблюдать можно, только на активном.

## 7 Выполните команду bash 5>&1. К чему она приведет? Что будет, если вы выполните echo netology > /proc/$$/fd/5? Почему так происходит?

Дескриптор с номером 5 будет перенаправлен на stdout. Следующая команда выведет netology на stdout

## 8 Получится ли в качестве входного потока для pipe использовать только stderr команды, не потеряв при этом отображение stdout на pty?

 	cat file 3>&1 1>&2 2>&3 3>&-
	
## 9 Что выведет команда cat /proc/$$/environ? Как еще можно получить аналогичный по содержанию вывод?

Выведутся переменные окружения. Аналогично: export

## 10 Используя man, опишите что доступно по адресам /proc/<PID>/cmdline, /proc/<PID>/exe

	/proc/<PID>/cmdline - This read-only file holds the complete command line for the process, unless the process  is  a  zombie.
	
	/proc/<PID>/exe - this file is a symbolic link containing the actual pathname of the executed command.


## 11 Узнайте, какую наиболее старшую версию набора инструкций SSE поддерживает ваш процессор


SSE4_2

## 12 Почитайте, почему так происходит, и как изменить поведение
	
Так происходит, потому что ssh не создает новый pty. Чтобы изменить поведение нужно добавить ключ -t
	
## 13 
	
	screen
	reptyr <PID>
	
## 14 Узнайте что делает команда tee и почему в отличие от sudo echo команда с sudo tee будет работать.

Команда будет работать, потому что сама утилита tee запущена от root и пишет в файл, доступ к которому есть у пользователя root.
	
	
