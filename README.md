# 03-sysadmin-2

## 1  тип команды cd

	vagrant@ubuntu-20:~$ type cd
	cd is a shell builtin

## 2 альтернатива без pipe команде grep <some_string> <some_file> | wc -l
	grep -с <some_string> <some_file>
	
## 3 процесс с PID 1
	/sbin/init

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

	bash 5>&1 
	cat file 2>&1 >/proc/$$/fd/5
	
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
	
	
