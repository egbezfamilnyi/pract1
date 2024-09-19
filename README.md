# Практическое занятие №1.
## Задача 1. Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).
```
localhost:~# cut -d: -f1 /etc/passwd | sort

```
<img width="1159" alt="Снимок экрана 2024-09-19 в 20 08 07" src="https://github.com/user-attachments/assets/61eacc6f-3b45-41f6-9e68-44ce4289db2d">

## Задача 2. Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере.

```
localhost:~# cat /etc/protocols | awk '{print $2, $1}' | sort -n -r | head -n 5
```
<img width="711" alt="Снимок экрана 2024-09-19 в 20 14 01" src="https://github.com/user-attachments/assets/782a4d4c-8a6b-48d6-9ad7-ce54c16cc8cf">

## Задача 3.Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!).

```
nano banner.sh                                          
#!/bin/bash
text=$1
length=${#text}
line="+-"
for ((i=0;i<length;i++))
do
line+="-"
done
line+="-+"
echo $line
echo "|" $text "|"
echo $line

localhost:~# chmod +x banner.sh

localhost:~# ./banner.sh "Hello from RTU MIREA!"
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
```
<img width="1318" alt="Снимок экрана 2024-09-19 в 20 29 53" src="https://github.com/user-attachments/assets/aa444b46-6cab-40f7-957f-3ca21e9608c2">

## Задача 4. Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

```
localhost:~# grep -oE '\b[a-zA-Z_][a-zA-Z0-9_]*\b' hello.c | grep -vE '\b(int|void|return|if|else|for|while|include|stdio)\b' | sort | uniq
```
<img width="1311" alt="Снимок экрана 2024-09-19 в 20 38 06" src="https://github.com/user-attachments/assets/f4ad30cf-116f-4a95-8d98-ebd9f860e6c2">

## Задача 5. Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

```
#!/bin/bash
chmod u+rwx $1
cp $1 /usr/local/bin


localhost:~# sudo ./regger.sh mama.sh
localhost:~# cd /usr/local/bin
localhost:/usr/local/bin# ls
```
![IMAGE 2024-09-19 21:19:06](https://github.com/user-attachments/assets/22db56ad-bc49-4fd2-8487-cebc3c26b930)
![IMAGE 2024-09-19 21:19:00](https://github.com/user-attachments/assets/9f77b5c1-21f5-4ae8-8d46-11d2897ef823)

## Задача 6. Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.
```
#!/bin/bash
line=$(head -1 $1)
if [[$line == "//"* ]] || [[$line == "#"* ]]; then
echo "First line have comment"
else
echo "First line dont have comment"
fi
```
![367580492-d1457d26-5bb6-4685-91a8-b8a7ecdbcc00-1](https://github.com/user-attachments/assets/5dd12aa6-5a4b-44c0-8cea-2c33475f3424)
![367580462-24b5a33b-ca09-43cd-9fc5-19e9e8c484cf](https://github.com/user-attachments/assets/e67f7d8d-8217-4973-9809-3a87806cae9d)
![367580597-01f2c3dd-71b6-44db-b128-7cbf9d77aef7](https://github.com/user-attachments/assets/1f9b5c74-5348-4d0f-bf08-19ea419b8b99)
![367580606-06976972-00f8-451c-b36e-6793d7f6804a](https://github.com/user-attachments/assets/12e0851b-9119-4c4b-a231-bc89cde1286a)
## Задача 7. Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).
```
#!/bin/bash
if [ $# -ne 1 ]; then
    echo "Использование: $0 <Путь к каталогу>"
    exit 1
fi
directory="$1"
 
find "$directory" -type f -print0 | xargs -0 md5sum | sort | uniq -d -w 32 | se>
    echo "Дубликат: $duplicate"
done
```
![367581430-7442a48a-87e3-43e0-a636-d7fca572df30](https://github.com/user-attachments/assets/38ae3313-48cf-4749-93f3-e7d3b6e3f946)
![367583038-0a6ef384-9be2-4759-979c-e0923397be06](https://github.com/user-attachments/assets/2a29863c-6803-4359-95e8-5e431bf1b618)

## Задача 8. Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.
![367581838-bbe434d7-7765-496d-aab1-dbe10ed7a150](https://github.com/user-attachments/assets/3a5678c1-7258-44ba-a874-9720f9e93765)

## Задача 9. Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.
```
#!/bin/bash
input_file="$1"
output_file="$2"
 
sed 's/ /\t/g' "$input_file" > "$output_file"
echo "Замена завершена. Результат сохранен в $output_file."
```
![367582313-13c4472f-b913-4e68-824f-7b956ace2e39](https://github.com/user-attachments/assets/e8bb25b2-12ad-4081-a355-d650182b5c50)
![367582347-894746bb-b643-4d11-8179-3d5c3f4a62ff](https://github.com/user-attachments/assets/fd85b5cf-6a17-4bc7-bcaa-d81bbb4651c4)
![367582400-9611b8d6-2569-457e-882a-08191686d649](https://github.com/user-attachments/assets/815ff6a6-78be-4ec6-b313-a31c3ddda810)
![367582290-f41db448-a3c0-4270-a115-0c7e2e3b5db8](https://github.com/user-attachments/assets/c3c7515b-d41d-4408-91e2-f1bf5dba8420)

## Задача 10. Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром.

```
#!/bin/bash
directory="$1"
find $1 -type f -size 0 -maxdepth 1
```
![367583374-b7f215b7-b0ba-4154-9c49-3c419363e276](https://github.com/user-attachments/assets/bee3ddbc-9906-4d2c-8c0e-1464cfbf342b)

![367583351-c84c845e-791a-4350-933b-654de8ae4d1d](https://github.com/user-attachments/assets/c24d7124-656e-4f6e-845a-a263a2ca8711)
