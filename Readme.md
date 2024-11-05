<h1>Getting Started Walk-through for IT Pros and System Administrators</h1>


<h2>Basics</h2>

<h3>1.0 Running your first container</h3>
Выполнемая команда:
docker container run hello-world
Результат в консоли:


![Screenshot 2024-11-04 at 22 06 42](https://github.com/user-attachments/assets/75866b01-30e3-4973-a007-9b42ba5c3000)


при запуске движок докера попытался осуществить поиск требуемого образа локально. После того,как движок не нашел образ докера локально, произошел поиск в Докер-регистре по умолчанию, которм вляется Докер хаб.


<h3>1.1 Docker images</h3>


В данной работе производится загрузка докер-образа linux alpine с Docker Hub. выполняемые команды:


docker image pull alpine
docker image ls


Реультат выполнения команд в консоли:


![Screenshot 2024-11-04 at 22 17 01](https://github.com/user-attachments/assets/ffbf4d3c-6cae-4603-a503-ae2217669de1)


<p>Так, образ linux alpine был успешно загружен  с Docker Hub</p>
<p><h3>1.1 Docker container run</h3></p>
<p>В данном задании изучается запуск контейнера</p>
<p>Выполним команду: </p>
docker container run alpine ls -l
<p>Результат выполнения команды</p>


![Screenshot 2024-11-04 at 22 27 06](https://github.com/user-attachments/assets/6c5366b6-4841-40df-b8cc-6232e6e6ac47)


<p> В результате выполнения комманды из ране згруженного образа linux alpine был запущен 
Docker контейнер, а также внутри линукс контейнера был запрошен список дииректорий, который был успшно выведен</p>
<p>Выполним следующую команду:</p>
<p>docker container run alpine echo "hello from alpine"</p>
<p>Результат выполнения команды:</p>


![Screenshot 2024-11-04 at 23 19 47](https://github.com/user-attachments/assets/f255edfc-8e3d-4ecc-91fb-53b334c5f784)

<p>Как можем наблюдать команда echo успешно выполнилась внутри контейнера с alpine, при этом команда echo была запущена в отдельном инстансе контейнера.Попробуем запустить другую команду:</p>
docker container run alpine /bin/sh 
<p>Результат выполнения комманды</p>


![Screenshot 2024-11-04 at 23 27 58](https://github.com/user-attachments/assets/7e50b2ec-88cd-49fa-8ca7-76276c2a8fd5)


<p>В результате выполнения команды  был запущен отдельный инстанс с образом alpine, внутри которого был запущен shell и сразу же произошел выход из shell и затем  из контейнера. Попробуем запустить данную программу немного иначе, воспользуемся флагами:</p>

 docker container run -it alpine /bin/sh

 <p>В результате выполнения коанды получим переход в режим консолии внутри контейнера с образом alpine, который был запущен в третьем инстансе:</p>

![Screenshot 2024-11-04 at 23 31 22](https://github.com/user-attachments/assets/9174b009-676f-4ec0-b56b-c187e050ebc7)

<p>Чтобы убедиться в том, что запущены различные инстансы докер контейнера с alpine образом, запросим список всех контейнеров, для этого воспользуемся командой docker ls -a (по умолчанию выводятся только запущенные контейнеры)</p>

![Screenshot 2024-11-04 at 23 37 58](https://github.com/user-attachments/assets/5fc9067e-cea5-45d4-bcf4-f7bd202bbe1f)

<h3>1.2 Container isolation</h3>

<p>Разберемся подробнее с концепциией изоляции контейнеров. Для этого выполним следующие команды:</p>
docker container run -it alpine /bin/ash

<p>Внутри контейнра выполним следующие команды:</p>
echo "hello world" > hello.txt
 ls
<p>Убедимся в том, что файл hello.txt был создан:</p>

![Screenshot 2024-11-04 at 23 52 01](https://github.com/user-attachments/assets/192e18ad-f804-4654-856d-b43b9e7397ed)


<p>Выполниим снова команду docker container run alpine ls, как результат, файл hello.txt не найден, поскольку данная команда была запущена  в отдельном контейнере, который не связан с предыдущим, это и есть демманстация концепции изоляции:</p>

![Screenshot 2024-11-04 at 23 56 30](https://github.com/user-attachments/assets/5c2e4790-d830-4766-a5a5-9ecc8f78cb46)


<p>Для того, чтобы получить доступ к контейнеру, в котором был создан файл hello.txt необходимо узнать ID контейнера, для этого выведем список  всех контейнеров, найдем среди списка нужный контейнер, командой docker container ls -a, затем запустим останоленный контейнер и выведем список созданных файлов при помощи команд:</p>

docker container start <container ID>
docker container exec <container ID> ls

Как результат увидим искомый файл среди спииска файлов:
 
![Screenshot 2024-11-05 at 00 04 47](https://github.com/user-attachments/assets/08a3f0f7-11b9-4c58-9265-33b899eda51d)

<h2>Customizing Docker images</h2>
<h3>Image creation from a container</h3>
В данном подразделе будет создан простой образ из контейнера. Для того, чтобы создать контейнер, загрузим образ ubuntu из Docker hub и запустим командой run:
docker container run -it --network=host ubuntu bash


![Screenshot 2024-11-05 at 23 05 45](https://github.com/user-attachments/assets/5149c983-7097-403d-a06d-a049ca0abc90)


<p>Образ ubuntu загружен и запущен контейнер на его основе.</p>
<p>Кастомизируем наш контейнер, для этого выполним команды:</p>
* apt-get update
* apt-get install -y figlet
* figlet "hello docker"
<p>Как результат видим Hello docker большими символами Ascii в консоли:</p>

![Screenshot 2024-11-05 at 23 06 17](https://github.com/user-attachments/assets/b2d05fb1-ffe6-4839-bf09-9a31b7b31220)

<p>выйдем из контейнера командой exit:</p>

![Screenshot 2024-11-05 at 23 10 18](https://github.com/user-attachments/assets/6d99f961-3423-4fb3-84aa-01c6ea12af5b)

<p>Для того, чтобы зафиксировать изменения в котейнере необходимо знать его ID, выведем список всех контейнеров командой docker container ls -a. Как результат видим созданный ранее контейнер: </p>

![Screenshot 2024-11-05 at 23 24 38](https://github.com/user-attachments/assets/aeb502d6-c2ff-4812-8f40-a86f81d5662d)

<p>Существует также возможность просмотра внесенных в контейнер изменений командой docker container diff <container id></p>
 
![Screenshot 2024-11-05 at 23 25 35](https://github.com/user-attachments/assets/7bbc44ed-7533-46de-8967-8bdf18fdb1ce)

<p>Зафиксируем изменения контейнера в коммите, получаем новый образ, переименуем его для удобства, проверим работоспособность образа. Для выполнения даных действий понадобилось выполнить следующие команды:</p>

+ docker container commit Container_ID
+ docker image ls
+ docker image tag Image_ID Image_name
+ docker container run ourfiglet figlet hello

<p>Как резальтат видим успешный запуск образа</p>

![Screenshot 2024-11-05 at 23 26 09](https://github.com/user-attachments/assets/6adf9c0e-b75d-4ed0-a535-1957cdf78229)



