Автор: Мурзин Михаил группа 4207

Данный репозторий предназначен для отчета по выполнению тренировочных заданий https://training.play-with-docker.com/

## Содержание
[1. Getting Started Walk-through for IT Pros and System Administrators](#1.Getting-Started-Walk-through-for-IT-Pros-and-System-Administrators)


[2. Getting Started Walk-through for Developers](#Getting-Started-Walk-through-for-Developers)

# 1.Getting Started Walk-through for IT Pros and System Administrators


## 1.1 Basics

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

<h3>Image creation using a Dockerfile</h3>
<p>В данном подразделе рассмтаривается создание докер контейнера с помощью Dockerfile. Создадим файл index.js, содержащий вывод в консоль имя пользователя, а также Dockerfile, содержащий требуемую последовательность действий для запуска контейнера, в том числе базовый образ linux alpine, установку обновлений, копирование файлов локальной папки в папку внутри образа, а также команду, которую необходимо выполнить при запуске контейнера (CMD). Используемые файлы представлены в директории IT_pros_system_admins/The_basics/Customising_docker_images . Для сборки контейнера необходимо выполнить команду: </p>
<p>docker image build --network=host -t hello:v0.1 .</p>
<p>После того, как контейнер собран, его необходимо запустить командой: docker container run hello:v0.1</p>

В результате выполнения даных действий получим:

![Screenshot 2024-11-06 at 00 03 11](https://github.com/user-attachments/assets/c7ade275-74bd-43bf-8fd5-e0f04b532141)

<h3>Image layers</h3>
<p>Разберемся в ее одном понятии - слой, используемое при построении образа. Образы собираются самостоятельно внутри слоев, разберемся подробнее в данной концепции. Просмотрим историю построения предыдущего простроенного образас помощью команды docker docker image history image_ID:</p>

![Screenshot 2024-11-06 at 00 14 24](https://github.com/user-attachments/assets/26293626-c578-4635-81aa-6f460448aec5)

<p>В результате выполнения получен набор слоев, которые последовательно создавались при сборке образа. Данная концепция позволяет изменять только один слой, если существует необходимость скорректировать приложение, вместо того, чтобы заново пересобирать весь образ, продемонстрируем это. Добавим в файл index.js дополнительную строку командой</p>
<p> echo "console.log(\"this is v0.2\");" >> index.js</p>
<p>Соберем контейнер командой docker image build --network=host -t hello:v0.2 . В результате получим:</p>

![Screenshot 2024-11-06 at 00 22 50](https://github.com/user-attachments/assets/324b42fb-299c-4578-bd1e-940b5cc586a3)

![Screenshot 2024-11-06 at 00 23 09](https://github.com/user-attachments/assets/75bd7426-a249-498e-90f8-66a783176197)

<p> Замечаем, что при выполнении некоторых команд возникает пометка <b>Cached</b>, Docker узнал, что подобные слои уже были построены и переиспользовал их. </p>
<h3>Image inspection</h3>
<p>Существует также возможность узнавать из чего состоит контейнер при помощт команды inspect. Рассмотрим примеры.Загрузим образ alpine из DockerHub, изучим из чего он состоит, воспользуемся командой <b>docker image inspect Container_ID_Name</b></p>

![Screenshot 2024-11-06 at 00 31 47](https://github.com/user-attachments/assets/d5c1be4b-37b3-47b6-aac2-6b2f69b1fa36)

<p> В результате вызова команды получили достаточно много сведений, в том числе о том из каких слоев состоит образ, какая архитектура операционной системы используется, а также метаданные образа. 
Ограичим информацию тлько описанием слоев <b>docker image inspect --format "{{ json .RootFS.Layers }}" alpine</b></p>

![Screenshot 2024-11-06 at 00 35 45](https://github.com/user-attachments/assets/bfa7bc37-f3a2-4e6b-a455-5073507c1fd6)

<p>Видим, что образ linux alpine состоит только из одного слоя, сравинм с образом hello, построенного ранее на основе alpine:</p>

![Screenshot 2024-11-06 at 00 37 10](https://github.com/user-attachments/assets/d2cfdc3c-8584-484d-acfc-078ddb17f1e3)

<p>Для образа hello наблюдаем уже три слоя: один из слоев это образ alpine (можно наблюдать как sha256 совпадают с образом alpine), далее есть слой Run для установки необходимых пакетов, а также слой содержащий копирование файла index.js с локальной машины в контейнер. Также стоит отметить, что все слои кроме последнего являются неизменяемыми</p>
<h3>Swarm Mode Introduction for IT Pros</h3>
<h3>Initialize your swarm</h3>
<p>Swarm режим сообщает докеру о том, что необходимо запустить несколько Docker движков и мы хотим иметь возможность управлять ими всеми. Для того, чтобы инициировать swarm режим воспользуемся командой <b>docker swarm init --advertise-addr $(hostname -i)</b>. В результате выполнения программы получим:</p>

![Screenshot 2024-11-06 at 00 57 20](https://github.com/user-attachments/assets/c9c92196-2d2e-4b35-a4b5-7a50f52ae6fe)

<p>В данном сообщении содержится информация о том как добавить новый узел - обработчик, а также о том, как добавить узел менеджер, добавим еще один узел обработчик командой <b>docker swarm join -token SWMTKN</b>:</p>

![Screenshot 2024-11-06 at 00 58 19](https://github.com/user-attachments/assets/a855eb1b-d14c-48cc-aeec-664c0ee24175)

<h3>Show Swarm Members</h3>

<p>Убедимся в том, что второй узел успешно добавлен, для этого выполним команду <b>docker node ls</b>. В списке узлов видим два узла, один из которых является управляющим (Leader)</p>

![Screenshot 2024-11-06 at 01 00 20](https://github.com/user-attachments/assets/cbd35436-2c5e-4c5d-b5a8-011ee9df217b)

<h3>Clone the Voting App</h3>
<p>Изучим пример кода с приложением голосования, для этого выполним команды:</p>

+ git clone https://github.com/docker/example-voting-app
+ cd example-voting-app

![Screenshot 2024-11-06 at 01 05 25](https://github.com/user-attachments/assets/dcfa0ef7-0aea-407a-8461-3b58bd158b47)

<h3>Deploy a Stack</h3>

<p>После клонирования обртим внимание на файл docker-stack.yml, который содержит информацию о архитектуре сервисов, количестве экземпляров, как все соединено, как обрабатывать обновления для каждого сервиса</p>

![Screenshot 2024-11-06 at 01 09 26](https://github.com/user-attachments/assets/e7da1890-a294-44e0-b904-e0648c4a42ae)

<p>Развернем стек (группу сервисов) командой <b>docker stack deploy --compose-file=docker-stack.yml voting_stack</b> , определим количество развернутых сервисов командой <b>docker stack ls</b></p>

![Screenshot 2024-11-06 at 01 10 17](https://github.com/user-attachments/assets/bd41ce58-800b-40cc-b100-61d8a5de3008)

<p>Также можно получить более детальную информацию о каждом сервисе c помощью команды <b>docker stack services voting_stack</b>:</p>

![Screenshot 2024-11-06 at 01 24 23](https://github.com/user-attachments/assets/88f32f20-5984-4c06-9a90-4352522107bd)

<p>Список задач сервиса голосования можно получить командой <b>docker service ps voting_stack_vote</b>:</p>

![Screenshot 2024-11-06 at 01 15 06](https://github.com/user-attachments/assets/2f6976d2-bc56-41cc-acd0-a020116c5df8)

<h3>Scaling An Application</h3>

<p>Для масштабирования приложения выполним команду <b>docker service scale voting_stack_vote=5</b>. Убедимся в том, что число сервисов возросло до 5 с помощью команды <b>docker stack services voting_stack</b></p>

![Screenshot 2024-11-06 at 01 20 29](https://github.com/user-attachments/assets/c95754b4-6ea7-4a78-9fec-87c186d185ab)

<h2>Stage 2: Digging deeper</h2>
<h3>Security Lab: Seccomp</h3>
<h3>Step 1: Clone the labs GitHub repo</h3>
<p>В данной работе рассмотрен  seccomp, который предоставляет  песочницу в ядре линукса, который действует как брандмауэр для системых вызовов. 
Он использует правила Berkeley Packet Filter (BPF), которые могут значительно ограничить доступ контейнеров к ядру Linux хоста Docker. Клонируем репозиторий, содержащий профиль seccomp для выполнения работы, изменим рабочую директорию </p>
 <b><p>git clone https://github.com/docker/labs</p>
 <p>cd labs/security/seccomp</p>
 </b>
 
![Screenshot 2024-11-06 at 21 26 17](https://github.com/user-attachments/assets/d47254be-db71-442f-9e49-e12598bdec43)

<h3> Step 2: Test a seccomp profile </h3>

<p>Загрженный с github файл deny.json профиля seccomp содержит пустой белый лист, это означает, что все системные вызовы будут блокированы, убедимся в этом.  Запустим новый контейнер, уберем ограничения, накладываемые apparmor, применим профиль deny.json, убедимся в том, что системые вызовы отсутствют в белом списке</p>

<b><p>docker run --rm -it --cap-add ALL --security-opt apparmor=unconfined --security-opt seccomp=seccomp-profiles/deny.json alpine sh</p></b>
<b><p>cat seccomp-profiles/deny.json</p></b>

![Screenshot 2024-11-06 at 21 35 29](https://github.com/user-attachments/assets/835f304a-a0cc-4d6e-91b2-a534ed518d91)

<p>В данном случае у Docker недостаточно разрешения на системные вызовы и контейнер не был запущен. </p>
 <h3>Step 3: Run a container with no seccomp profile</h3>
 <p>Запустим контейнер без применения seccomp, убедимся в том, что контейнер работает и отправляет системные вызовы docker host:</p>
<b>
 <p>docker run --rm -it --security-opt seccomp=unconfined debian:jessie sh</p>
 <p>whoami</p>
 <p>  unshare --map-root-user --user
  whoami</p>
</b>

![Screenshot 2024-11-06 at 21 44 40](https://github.com/user-attachments/assets/9db8a36d-9c63-4f67-8a6c-cc9496fc6bb1)

<p>Для того, чтобы увидеть последовательность системмных вызовов, которые были сделаны при обработке команды whoami можно воспользоватся командой :</p>
<b>
 <p>apk add --update strace
strace -c -f -S name whoami 2>&1 1>/dev/null | tail -n +3 | head -n -2 | awk '{print $(NF)}'</p>
 <p>strace whoami</p>
</b>

![Screenshot 2024-11-06 at 21 47 45](https://github.com/user-attachments/assets/3341c7a0-3f8c-499f-a10d-50a27a5e377b)

<h3>Step 4: Selectively remove syscalls</h3>
<p>Запустим новый контейнер с профайлом default-no-chmod.json и попробуем запутить команду chmod 777 / -v :</p>
<b><p>docker run --rm -it --security-opt seccomp=./seccomp-profiles/default-no-chmod.json alpine sh</p>
<p>chmod 777 / -v</p>
</b>

![Screenshot 2024-11-06 at 21 53 14](https://github.com/user-attachments/assets/30416282-a4ef-45c9-8b99-f0e9c54a3415)

Данную операцию не удалось выполнить, поскольку системный вызов chmod был удален из белого списка в default-no-chmod.json

Запустим другой контейнер, в котором воспользуемся профилем, default.json содержащем команду chmod в белом списке:

<b>
docker run --rm -it --security-opt seccomp=./seccomp-profiles/default.json alpine sh

chmod 777 / -v</b>

![Screenshot 2024-11-06 at 21 55 59](https://github.com/user-attachments/assets/c574f2d2-cc27-40d3-b757-89144b6bdc5d)

В данном случае удалось успешно выполнить операцию. Убедимся в том, что файл default.json содержит chmod , а файл default-no-chmod.json не содержит chmod:

<b>
cat ./seccomp-profiles/default.json | grep chmod

cat ./seccomp-profiles/default-no-chmod.json | grep chmod
</b>

![Screenshot 2024-11-06 at 21 58 03](https://github.com/user-attachments/assets/25624f94-a237-4cda-9a16-25af8cdd3d7b)

<h3>Step 5: Write a seccomp profile</h3>
С помощью strace можно получить список всех системных вызовов, выполняемых программой, убедимся в этом:

<b>strace -c -f -S name ls 2>&1 1>/dev/null | tail -n +3 | head -n -2 | awk '{print $(NF)}'</b>


![Screenshot 2024-11-06 at 21 59 45](https://github.com/user-attachments/assets/07370a24-3f20-4820-82a6-f719643d15d4)

<h3>Linux kernel capabilities and Docker</h3>

<h3>Introduction to capabilities</h3>

Ядро линукс способно разделить привилегии пользователя на отдельные блоки, называемые возможностями. Почти все специальные полномочия, связанные с root пользователем Linux, разбиты на отдельные возможности. Docker накладывает определенные ограничения, которые значительно упрощают работу с возможностями. Например, возможности файла хранятся в его расширенных атрибутах, а расширенные атрибуты удаляются при сборке образов Docker.

В среде без файловых возможностей приложения не могут повышать свои привилегии за пределы bounding set. Docker устанавливает граничное множество перед запуском контейнера. С помощью команд Docker можно добавлять или удалять возможности из граничного набора.

<h3>Step 2: Working with Docker and capabilities</h3>

Начиная с версии Докер 1.12 существует 3 способа использования возможностей 

+ Запускать контейнеры от имени root с большим набором возможностей и пытаться управлять возможностями внутри контейнера вручную.
+ Запускать контейнеры от имени root с ограниченным набором возможностей и никогда не изменять их внутри контейнера.
+ Запускать контейнеры от имени непривилегированного пользователя без каких-либо возможностей.

Существующие команды для управления возможностями (будут использоваться в следующем подразделе):

+ docker run --rm -it --cap-drop $CAP alpine sh - сбросить возможности из аккаунта root контейнера
+ docker run --rm -it --cap-add $CAP alpine sh - Добавить возможности в root аккаунт контейнера
+ docker run --rm -it --cap-drop ALL --cap-add $CAP alpine sh - отказаться от всех возможностей, а затем явно добавить отдельные возможности в корневую учетную запись контейнера.

<h3>Step 3: Testing Docker capabilities</h3>

Запустим контейнер и убедимся в том, что root пользователь может изменять права на файлы

<b> docker run --rm -it alpine chown nobody /</b>

![Screenshot 2024-11-06 at 22 54 16](https://github.com/user-attachments/assets/5eed0d7c-9dc2-4544-92a7-7996ab002ea1)

Контейнер успешно запустился, поскольку по умолчанию новые контейнеры запускаются с правами пользователя root. Этот пользователь root по умолчанию имеет права CAP_CHOWN.

Запустим другой контейнер и удалим все возможности кроме CHOWN:

<b>docker run --rm -it --cap-drop ALL --cap-add CHOWN alpine chown nobody /</b>

![Screenshot 2024-11-06 at 22 59 21](https://github.com/user-attachments/assets/42dfb94b-7bc8-4124-8f12-2fb4756deed9)

Контейнер успешно запустился,  поскольку данной возможни достаточно для запуска контейнера. Попробуем убрать возможность CHOWN и запустить контейнер:

<b>  docker run --rm -it --cap-drop CHOWN alpine chown nobody / </b> 

![Screenshot 2024-11-06 at 23 00 20](https://github.com/user-attachments/assets/fa86dbbc-cbaa-4990-ac98-b382850c7bc2)

Контейнер не был запущен, поскольку была удалена требуемая возможность. Попробуем добавить возможность CHOWN для пользователя отличого от root:

![Screenshot 2024-11-06 at 23 02 50](https://github.com/user-attachments/assets/3d04f414-f374-489c-966c-926edfa1daa7)

Контейнер не был запущен, поскольку Docker не поддерживает установку возможностей для пользователей, отличных от root

<h3>Step 4: Extra for experts</h3>

Для вывода возможностей можно воспользоваться пакетом libcap:

<b>    docker run --rm --network=host -it alpine sh -c 'apk add -U libcap; capsh --print'</b>

![Screenshot 2024-11-06 at 23 07 32](https://github.com/user-attachments/assets/e7e02d63-d986-4720-806d-d5aa298a9cce)

Для эуспериментальных целей команда capsh является полезной, вывести справку по ее использованию можно с помощью команды:

<b>docker run --rm --network=host -it alpine sh -c 'apk add -U libcap;capsh --help' </b>

![Screenshot 2024-11-06 at 23 09 25](https://github.com/user-attachments/assets/e61bb7f8-7631-4271-9e9c-d2845158c936)

<h3> Docker networking hands-on lab</h3>

<h3> Section 1: Networking Basics</h3>

Главная команда для конфигурирования сети - docker network, при ее выполнении появляется подсказка по использованию:

<b>docker network</b>

![Screenshot 2024-11-06 at 23 15 31](https://github.com/user-attachments/assets/f08fc8dc-a46c-49fb-adf7-707ca8583867)

Для вывода существующих сетей контейнера используется команда:

<b>docker network ls</b>

![Screenshot 2024-11-06 at 23 17 11](https://github.com/user-attachments/assets/1d37ae29-88ed-4dc3-85c6-6d7b78bd62f4)

Для просмотра подробных параметров конфигурации сети используется команда:

<b> docker network inspect bridge </b>

![Screenshot 2024-11-06 at 23 19 07](https://github.com/user-attachments/assets/901e7b83-6375-44d8-83e9-5938483194b7)

Для просмотра установленных драйверов сети используется команда:

<b>docker info</b>

![Screenshot 2024-11-06 at 23 21 19](https://github.com/user-attachments/assets/a7837228-8c70-40c3-b4d2-a8ee629abc57)

![Screenshot 2024-11-06 at 23 21 31](https://github.com/user-attachments/assets/3e4c7424-3067-4d86-968e-3bfa26753ced)

Среди установленных плагинов сети видим bridge, host,macvlan, null, и overlay драйверы.

<h3> Section #2 - Bridge Networking </h3>

При запуске Docker всегда существует предустановленная сеть bridge, в предыдущем подразделе убедились в существовании данной сети (<b>docker netork ls</b>). Добавим команду brctl для получения списка мостов Linux на хосте Docker.

<b>apk update

apk add bridge</b>

Получим список мостов с помощью команды:

<b>brctl show</b>

![Screenshot 2024-11-06 at 23 33 41](https://github.com/user-attachments/assets/40dba0f2-9fe3-41ad-b9f6-0d721a2be9ca)

Для получения дополнительной информации о мостах необходимо выполнить команду:

<b>ip a</b>

![Screenshot 2024-11-06 at 23 53 18](https://github.com/user-attachments/assets/5580a0b4-347b-47f3-91b9-e44fba3704e0)

Создадим контейнер командой:

<b>docker run -dt ubuntu sleep infinity</b>

Убедимся в том, что контейнер запустился:
<b>docker ps</b>

Поскольку никакая сеть не была задана при запуске контейнера, то используется сеть bridge, запустим команду <b>brctl show</b>:

![Screenshot 2024-11-07 at 00 15 09](https://github.com/user-attachments/assets/f9de4ead-ce4c-406e-bb09-b0c83744e6af)

Также можем получить информацию о сети bridge:

<b>docker network inspect bridge</b>

![Screenshot 2024-11-07 at 00 19 34](https://github.com/user-attachments/assets/3cc26bca-c5b5-4de0-94b0-0d6e5a9fe3cc)

![Screenshot 2024-11-07 at 00 19 46](https://github.com/user-attachments/assets/0b379e85-7584-4b99-bff5-377230cdc3b8)

Успешно находим инфомрацию о контейнере, который подключен к сети bridge. Попробуем пропинговать IP адрес сети моста, к которой подключен контейнер.

<b> ping -c5 <IPv4 Address> </b>

![Screenshot 2024-11-07 at 00 22 19](https://github.com/user-attachments/assets/0db6f9f4-11cb-42fc-a841-f4f4f8d7c653)

Запустим shell контейнера командой <b> docker exec -it <CONTAINER ID> /bin/bash. </b>. Далее в пособии имеется ошибка и следующая команда не может быть выполнена, поскольку контейнер не подключен к внешней сети интернет, попытка обновления apt-get проваливается:

apt-get update && apt-get install -y iputils-ping

![Screenshot 2024-11-07 at 00 24 56](https://github.com/user-attachments/assets/b5715b54-0645-4afb-aab0-b210edd19672)

Остановим контейнер и передем к следующему шагу.

Запустим новый контейнер на основе образа nginx и соединим порт 8080 Docker host c портом 80 контейнера с помощью запуска команды:

<b> docker run --name web1 -d -p 8080:80 nginx</b>

![Screenshot 2024-11-07 at 00 34 58](https://github.com/user-attachments/assets/c69eef6d-8f0d-49a3-93e1-06c2d37ee13c)

Проверим статус контейнера и соответсвие портов командой <b>docker ps</b>:

![Screenshot 2024-11-07 at 00 35 18](https://github.com/user-attachments/assets/5143271c-9bc5-4833-b29f-eeddef043e6d)

Если нет возможности подключиться к браузеру, отправить запрос можно к docker host командой :

<b>curl 127.0.0.1:8080</b>

![Screenshot 2024-11-07 at 00 37 53](https://github.com/user-attachments/assets/e5166dfb-d2ea-498c-b680-27d97be835ff)

В ответ на запрос приходит тестовая страница образа nginx

![Screenshot 2024-11-07 at 00 44 29](https://github.com/user-attachments/assets/ebebd41e-04d0-4830-86ec-bd551721a546)

<h3>Section 3 - Overlay Networking</h3>

Запустим Swarm с одним узлом worker, проверим выполнение операций. Выполним команду <b>docker swarm init --advertise-addr $(hostname -i)</b>

![Screenshot 2024-11-07 at 00 51 54](https://github.com/user-attachments/assets/e5c056a4-5ad4-4582-9b11-7f491b6c1558)

Во втором узле выполним команду, добавим узел в swarm в качестве worker <b>docker swarm join --token SWMTKN-1-69nft06mpui4ygps7qzwu6lwvbbtuz478lp463kwcrre4m3awl-aykrmn6m9pgn5lo8f68gg7y89 192.168.0.27:2377</b>

![Screenshot 2024-11-07 at 00 52 58](https://github.com/user-attachments/assets/08032dc8-7194-4bc4-93b7-ba5297123451)

После выполнения команды убедимся, что оба узла добавлены в swarm: 

<b>docker node ls </b>

![Screenshot 2024-11-07 at 00 54 22](https://github.com/user-attachments/assets/34bf484e-0564-4f3e-84a8-3a63ec6055fb)

Создадим перекрывающуюся сеть командой :

<b>docker network create -d overlay overnet</b>

![Screenshot 2024-11-07 at 01 00 53](https://github.com/user-attachments/assets/55a70d75-0c7a-4b7c-9e3c-35f867fe8425)

Убедимся в том, что сеть была успешно создана с помощью команды <b>docker network ls </b> в узле менеджера

![Screenshot 2024-11-07 at 01 04 17](https://github.com/user-attachments/assets/5abfcef3-dca0-4675-a79f-cb898c4fc9ca)

Вместе с этим в узле worker сеть не отображается, это связано с overlay драйвером

![Screenshot 2024-11-07 at 01 04 43](https://github.com/user-attachments/assets/da682b11-3630-4b8c-9ee3-6b52b86aab89)

Для получения дополнительной информации о сети overnet можно воспользоваться командой:

<b>docker network inspect overnet</b>

![Screenshot 2024-11-07 at 01 06 00](https://github.com/user-attachments/assets/addf8418-c1cf-48fb-83b1-0f6e135671cf)

Выполним данные команды для создания сервиса с двумя репликами:

<b>
 
+  docker service create --name myservice \

+  --network overnet \

+ --replicas 2 \

+ ubuntu sleep infinity

</b>

![Screenshot 2024-11-07 at 01 08 34](https://github.com/user-attachments/assets/6e0a98fa-7221-4fdb-ae2d-4b5645ccf373)

Убедимся в том, что сервис был создан и обе реплики работают с помощью команды <b>docker service ls</b>

![Screenshot 2024-11-07 at 01 09 59](https://github.com/user-attachments/assets/17c8dc84-35e7-42a8-910b-a9c913fadbff)

Убедимся в том, что на каждом узле запущено одо задание с помощью команды: 

<b>docker service ps myservice</b>

![Screenshot 2024-11-07 at 01 10 35](https://github.com/user-attachments/assets/682c3831-44bb-4fdc-961d-b9ae2c08ff38)

Теперь во втором узле можем получить информацию о сети overlay с помощью команд:

<b>docker network inspect overnet</b>

<b>docker network ls</b>

![Screenshot 2024-11-07 at 01 12 36](https://github.com/user-attachments/assets/084d4b00-9843-4fbe-9fdb-1437540c4170)


![Screenshot 2024-11-07 at 01 12 48](https://github.com/user-attachments/assets/ec7b523b-d775-42bc-b1e4-15c99369cbf2)

Выполнение команды <b>apt-get update && apt-get install -y iputils-ping</b> не предоставляется возможным, поскольку при создании контейнера необходимо было подключить --network=host для доступа во внешгюю сеть интернет

Запустим bash внутри контейнера, просмотрим содержимое файла resolve.cof:

<b>
docker exec -it yourcontainerid /bin/bash
cat /etc/resolv.conf
</b>

![Screenshot 2024-11-07 at 01 21 14](https://github.com/user-attachments/assets/4201e12f-da5e-40b2-ab71-66e2ca828a1d)

Интересующее нас значение - это сервер имен 127.0.0.11. Это значение отправляет все DNS-запросы от контейнера к встроенному DNS-резольверу, работающему внутри контейнера и слушающему 127.0.0.11:53. Все контейнеры Docker запускают встроенный DNS-сервер по этому адресу.

Очистим созданные сервисы командой <b>docker service rm myservice</b>

![Screenshot 2024-11-07 at 01 23 33](https://github.com/user-attachments/assets/7485a2ca-89fe-4e42-a5f3-b578c38dde06)

Просмотрим работающие контейнеры <b> docker ps</b>:

![Screenshot 2024-11-07 at 01 25 21](https://github.com/user-attachments/assets/379e57dc-c40f-4813-a25a-61e2324004e8)

Удалим узлы 1 и 2 из Swarm командой <b>docker swarm leave --force</b>

![Screenshot 2024-11-07 at 01 26 20](https://github.com/user-attachments/assets/d7338da8-ca13-4e99-981d-2196c8a490a8)

![Screenshot 2024-11-07 at 01 27 37](https://github.com/user-attachments/assets/7298b642-abb4-4b66-bdaf-2dead4318a42)

После удаления узлов работающий контейнер был остановлен 

![Screenshot 2024-11-07 at 01 29 49](https://github.com/user-attachments/assets/e60a6275-edd2-42a6-809d-d3f8a6d9bcb1)

<h3>Orchestration<h3>
<h3>Section 1: What is Orchestration</h3>

Оркестрация необходима при разработке выскоко-нагруженных приложений с высокими требованиями доступности. Механизм оркестрации позволяет автоматически распределять нагрузку между узлами приложения, в случае если например один из узлов входит из строя. Развертывание приложения вручную является трудоемким, поскольку необходимо прописывать ssh для каждой машины самостоятельно, с помощью инструментов оркестровки  можно освободиться от большей части этой ручной работы и позволить автоматизации выполнить всю тяжелую работу

Запустим контейнер в первом узле: <b>docker run -dt ubuntu sleep infinity</b>

![Screenshot 2024-11-07 at 09 57 57](https://github.com/user-attachments/assets/4a3f85fe-b0fb-43d0-b06a-ed13fc96bc2e)

Убедимся в том, что контейнер запущен <b>docker ps</b>

![Screenshot 2024-11-07 at 09 59 27](https://github.com/user-attachments/assets/95e203f0-6b2c-449f-879d-13f79a79b839)

Запустим swarm менеджер с помощью команды <b> docker swarm init --advertise-addr $(hostname -i)</b>

![Screenshot 2024-11-07 at 10 00 37](https://github.com/user-attachments/assets/0761f0db-890e-4dac-b5cf-0e92a6ec45a3)

С помощью команды <b> docker info</b> можно убедиться в том, что узел 1 успешно сконфигурирован как менеджер

![Screenshot 2024-11-07 at 10 01 55](https://github.com/user-attachments/assets/6bc6ccd4-f447-44ee-9bec-f89e88cb94fe)

![Screenshot 2024-11-07 at 10 02 12](https://github.com/user-attachments/assets/97908a5a-81c1-40bc-a758-f60df9dac2bb)

Добавим узлы 2 и 3 командой <b>docker swarm join ...</b>

![Screenshot 2024-11-07 at 10 03 02](https://github.com/user-attachments/assets/fbcdc3fb-2544-4a26-9ff9-63171ee24329)

![Screenshot 2024-11-07 at 10 03 15](https://github.com/user-attachments/assets/691c5357-da16-4a3a-93d0-2fcacaaaf3fe)

Убедимся в том, что узлы 2 и 3 были успешно добавлены с помощью выполнения команды <b>docker node ls</b> в узле 1

![Screenshot 2024-11-07 at 10 04 20](https://github.com/user-attachments/assets/66bf851a-d355-4f8a-96a1-89f3fe85d8ac)

Развернем сервис sleep через docker swarm с помощью команды 

<b> docker service update --replicas 7 sleep-app </b>

![Screenshot 2024-11-07 at 10 07 23](https://github.com/user-attachments/assets/7aa2ea6f-bd9f-42f2-80e9-af587e361baa)

Swarm менеджер запланировал 7 контейнеров в кластере. Убедимся в том, что число контейнеров 7. Просмотрим список работающих контейнеров с помощью команды 

<b>docker service ps sleep-app</b>

![Screenshot 2024-11-07 at 10 09 25](https://github.com/user-attachments/assets/fd805850-2fe5-412b-8a94-f6d480cadf80)

![Screenshot 2024-11-07 at 10 09 35](https://github.com/user-attachments/assets/9d295d13-5b30-4e44-8a88-f6256c5bea0a)

Представим, что необходимо снизить число работающих контейнеров до 4, необходимо выполнить команду :

<b>docker service update --replicas 4 sleep-app </b>

 ![Screenshot 2024-11-07 at 10 11 20](https://github.com/user-attachments/assets/173e55e9-93fe-4bc2-b893-67a1197ee332)

Убедимся в том, что число контейнеров уменьшилось до 4 : 

<b>docker service ps sleep-app</b>

![Screenshot 2024-11-07 at 10 12 12](https://github.com/user-attachments/assets/23b5b774-2a8c-458d-b143-b0f251f27337)

Допустим, необходимо провести какие-то работы и вывести из строя один из узлов (например второй). Просмотрим состояние узлов в узле менеджера:

<b> docker node ls </b>

![Screenshot 2024-11-07 at 10 14 52](https://github.com/user-attachments/assets/6c0697e8-1821-4d20-baf6-50d75c7b63f8)

Просмотрим контейнеры, зыпущенные на втором узле

<b> docker ps </b>

![Screenshot 2024-11-07 at 10 15 12](https://github.com/user-attachments/assets/4be1a43d-4a7d-4eae-9e80-4ea158afbe2a)

Выполним команду для вывода из строя узла 2, подставляем в команду ID второго узла, далее просмотрим список узлов

<b> docker node update --availability drain yournodeid</b>
<b>docker node ls</b>

![Screenshot 2024-11-07 at 10 17 31](https://github.com/user-attachments/assets/2af2d539-cac5-4c7d-8cc3-a7737e756b21)

Просмотрим список контейнеров, запущенных во втором узле

<b>docker ps</b>

![Screenshot 2024-11-07 at 10 18 49](https://github.com/user-attachments/assets/c80b4bba-5b11-4543-a15a-99a04f1f46f9)

Убеждаемся в том, что приложение а данном узле было остановлено. Просмотрим снова список работающих узлов, убедимся в том, что второй узел был заменен, нагрузка перераспределена между оставшимися контейнерами.

<b>docker service ps sleep-app </b>

![Screenshot 2024-11-07 at 10 19 33](https://github.com/user-attachments/assets/db8e2219-d7c2-4791-be34-4b460174a24c)

Удалим созданный сервис:

<b>docker service rm sleep-app</b>

![Screenshot 2024-11-07 at 10 21 38](https://github.com/user-attachments/assets/65335672-0a9d-4b25-847a-dcc7c27609a0)

Просмотрим список запущеных контейнеров:
<b> docker ps</b>

![Screenshot 2024-11-07 at 10 23 19](https://github.com/user-attachments/assets/8f18d952-ccad-499a-b463-5ac35a516dc1)

остановим запущенный контейнер с помощью команды <b>docker kill</b>

![Screenshot 2024-11-07 at 10 24 07](https://github.com/user-attachments/assets/a478a27e-538b-44e0-b50d-01d4d26d9aa6)

Удалим запущенные узлы из swarm командой <b> docker swarm leave --force</b>

![Screenshot 2024-11-07 at 10 25 37](https://github.com/user-attachments/assets/81fa508d-4946-4ea5-8989-11d68193a3ef)

![Screenshot 2024-11-07 at 10 25 46](https://github.com/user-attachments/assets/be4c4550-8949-4e33-adfe-c27820630802)

![Screenshot 2024-11-07 at 10 25 54](https://github.com/user-attachments/assets/a4a47185-f00f-4233-92db-c09510136108)

# Getting Started Walk-through for Developers

<h2>Basics</h2>

<h3>Docker for Beginners - Linux</h3>

Клонируем репозиторий для лаборной работы

<b>git clone https://github.com/dockersamples/linux_tweet_app</b>

![Screenshot 2024-11-07 at 20 27 53](https://github.com/user-attachments/assets/c84547bb-82dc-43f1-a69e-781869988cee)

Запустим контейнер linux alpine, который выполнит команду hostname и остановится

<b> docker container run alpine hostname</b>

![Screenshot 2024-11-07 at 20 32 55](https://github.com/user-attachments/assets/7f0333da-b326-4900-8365-82c2063858d9)

Данный контенер работает до тех пор, пока не выполнит команду hostname, однако потом не исчезает, продолжает существовать в состоянии exited. 
Просмотреть список всех контейнеров можно с помощью команды:

<b> docker container ls --all</b>

![Screenshot 2024-11-07 at 20 35 38](https://github.com/user-attachments/assets/33628abc-cb0d-4356-a3e0-05ece594a297)

В списке контейнеров можем найти ранее запущенный и остановленный контейнер. Запустим контейнер Ubuntu и в контейнере запустим bash:

<b> docker container run --interactive --tty --rm ubuntu bash </b>

Использованные ключи:

+ --interactive - задает интерактивную сессию
+ --tty - выделяет псевдотерминал
+ --rm - после завершения выполнения контейнер будет удален

Внутри контейнера выполним команды:

+ ls / - отображение всех файлов и каталогов текущей директории
+ ps aux - отображение запущеннх процессов в контейнере
+ cat /etc/issue - отображение дистрибутива линукс на основе которого запущен контейнер
+ exit - выход из контейнера

![Screenshot 2024-11-07 at 20 42 56](https://github.com/user-attachments/assets/fdcc7fab-d141-42f8-b1eb-4e1875510ab0)

Просмотрим версию линукс виртуальной машины host:

<b>  cat /etc/issue </b>

![Screenshot 2024-11-07 at 20 47 19](https://github.com/user-attachments/assets/7667f6a1-1504-4ea9-ab02-ccf70f7c6d40)

Запустим mysql контейнер с помощью команды:

 <b>docker container run \
 --detach \
 --name mydb \
 -e MYSQL_ROOT_PASSWORD=my-secret-pw \
 mysql:latest</b>

В команде использованы ключи:

+ --detach - запускает контейнер в фоновом режиме
+ --name - имя контейнера
+ -e - позволяет задать пароль как переменную среды

![Screenshot 2024-11-07 at 20 54 34](https://github.com/user-attachments/assets/09207d80-0897-4bd6-8665-483ee716ff31)

Просмотрим список запущенных контейнеров, обратим внимание, что контейнер mysql запущен:

<b>docker container ls</b>

![Screenshot 2024-11-07 at 20 56 03](https://github.com/user-attachments/assets/1cf66015-4cf5-475d-b56e-d769bb121698)

Также существует возможность просмотра логов контейнера с помощью команды <b> docker container logs mydb</b>

![Screenshot 2024-11-07 at 20 58 04](https://github.com/user-attachments/assets/24f18822-9360-4972-85ab-ae7054be17df)

Список запущенных команд внутри контейнера можно просмотреть с помощью команды <b>  docker container top mydb</b>

![Screenshot 2024-11-07 at 20 59 44](https://github.com/user-attachments/assets/4957e8a0-8ca0-40be-b71d-c4c29841f9ca)

Запросим версию mysql с помощью команды <b> docker exec -it mydb \
 mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version</b>

![Screenshot 2024-11-07 at 21 01 49](https://github.com/user-attachments/assets/cc7a8aff-0fe9-4787-b59d-42264220ca4b)

Выполним аналогичное дествие последовательно, сначала запустив shell внутри контейнера, затем запросив версию mysql, 
убедимся в том, что результат совпадает с результатом при выполнении предыдущей команды:

<b> docker exec -it mydb sh</b>

<b>  mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version </b>

<b> exit </b>

![Screenshot 2024-11-07 at 21 04 02](https://github.com/user-attachments/assets/2789bcb3-cee7-4b97-9528-3148e74bc149)

<h3>Task 2: Package and run a custom app using Docker</h3>

Переместимся в нужныю директорию, отобразим содержимое докерфайла
<b>  cd ~/linux_tweet_app </b>
<b>  cat Dockerfile </b>

![Screenshot 2024-11-07 at 21 06 12](https://github.com/user-attachments/assets/6291de85-0c1f-4e92-bbc6-868fe8763dfd)

Рассмотрим синтаксис докерфайла:

+ FROM - определяет базовый образ на основе которого строится контейнер
+ COPY - копирует файлы из хоста Docker в необходимую директорию докер образа
+ EXPOSE - фиксирует занимаемые приложением порты
+ CMD - определяет команды, которые необходимо выполнить при запуске контейнера

Зададим переменную среды DOCKERID, проверим, что переменная среды успешно задана

<b>export DOCKERID=DOCKERID</b>
<b> echo $DOCKERID</b>

![Screenshot 2024-11-07 at 21 13 05](https://github.com/user-attachments/assets/25308ee8-ba8d-4b58-ab94-600bc8626be2)

Соберем докер образ из докер файла, зададим таг контейнера:

<b>docker image build --tag $DOCKERID/linux_tweet_app:1.0 .</b>

![Screenshot 2024-11-07 at 21 14 38](https://github.com/user-attachments/assets/8c0dd18e-3f9d-48d8-a57d-28721671ccfd)

Запустим докер контейнер командой:

<b> docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0</b>
 
![Screenshot 2024-11-07 at 21 15 54](https://github.com/user-attachments/assets/717db3c9-d111-4d8c-a6f5-d5f8500a46df)

При запуске контейнера использовался ключ --publish, который необходим для разрешения трафика между портами докер хоста и контейнера. 
После запуска контейнера убедимся в том, что на порту 80 контейнера стала доступна тестовая страница:

![Screenshot 2024-11-07 at 20 19 06](https://github.com/user-attachments/assets/67b69a92-6bd7-4279-b58c-a706ae9ef3fe)

После просмотра сайта остаовим контейнер и удалим его:
<b> docker container rm --force linux_tweet_app</b>

![Screenshot 2024-11-07 at 21 24 20](https://github.com/user-attachments/assets/bce2cf1c-2ce8-41a3-a126-093303d964e9)

Запустим контейнер, воспользуемся командой mount, чтобы смонтировать текущую директорию в директорию контейнера:

<b>
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 --mount type=bind,source="$(pwd)",target=/usr/share/nginx/html \
 $DOCKERID/linux_tweet_app:1.0
</b>


![Screenshot 2024-11-07 at 21 26 49](https://github.com/user-attachments/assets/7ff6484f-574c-4802-89cc-46e6b85569f3)

Как результат можем наблюдать запущенный на порту 80 сайт 

![Screenshot 2024-11-07 at 20 19 06](https://github.com/user-attachments/assets/67b69a92-6bd7-4279-b58c-a706ae9ef3fe)

Заменим файл index.html  на файл index-new.html из клонированнаго ранее git репозитория:
 
<b> cp index-new.html index.html</b>

![Screenshot 2024-11-07 at 21 32 04](https://github.com/user-attachments/assets/5301fad1-3f3b-44ea-87b0-9d5510b4ee97)

Как результат увидим обновленный сайт на порту 80

![Screenshot 2024-11-07 at 20 19 59](https://github.com/user-attachments/assets/efbc0cce-e11f-4831-9a60-de935f7b9b1a)

Остановим и удалим текущий контейнер 

<b> docker rm --force linux_tweet_app </b>

![Screenshot 2024-11-07 at 21 32 34](https://github.com/user-attachments/assets/88872de3-259c-4040-b9ef-a705bb9a8b45)

Повторим текущий запуск без привязки:

<b>
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0
</b>

![Screenshot 2024-11-07 at 21 32 46](https://github.com/user-attachments/assets/da6910c1-7c0a-454b-8e09-bcd23fdf64d3)

ОБратим внимание на то, что сайт имеет первоначальный вид, поскольку отключена привязка и в контейнере находится оргинальный index.html

![Screenshot 2024-11-07 at 20 20 39](https://github.com/user-attachments/assets/a47cdedd-3fdc-47ba-b955-5efda6b7e46e)

Остановим и удалим текущий контейнер

![Screenshot 2024-11-07 at 21 33 39](https://github.com/user-attachments/assets/add4c8ce-f9a8-4812-a33b-7c38ab7b9c73)

Соберем новый образ и обозначим его как 2.0

<b> docker image build --tag $DOCKERID/linux_tweet_app:2.0 .</b>

![Screenshot 2024-11-07 at 21 33 53](https://github.com/user-attachments/assets/fe500adf-f147-4ff6-b68f-fac3149cf6d4)

Просмотрим список новых контейнеров:
 
 <b>docker image ls</b>
 
![Screenshot 2024-11-07 at 21 34 07](https://github.com/user-attachments/assets/ed4cf845-6d64-44bc-a921-e966b0c55d10)

Запустим контейнер из новой версии образа:

<b> docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:2.0</b>


![Screenshot 2024-11-07 at 21 34 21](https://github.com/user-attachments/assets/db39fcca-ca39-4488-8006-db5627165888)

Как результат, на порту 80 запущена новая версия сайта


![Screenshot 2024-11-07 at 20 21 45](https://github.com/user-attachments/assets/d82779a6-faa6-4b0a-bd04-3aef05ff9ea6)

Запустим на другом порту контейнер на основе старого образа

<b>
 docker container run \
 --detach \
 --publish 8080:80 \
 --name old_linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0
</b>b

![Screenshot 2024-11-07 at 21 34 30](https://github.com/user-attachments/assets/cd97c8c6-fe6c-4b34-9026-f97d68a7e932)

Убедимся в том, что на соответствующем порту запущена первоначальная версия сайта 

![Screenshot 2024-11-07 at 20 22 29](https://github.com/user-attachments/assets/7468be4b-b8ed-4b40-8947-7e277edcd324)

Просмотрим образы, на текущем докер хосте:

<b> docker image ls -f reference="$DOCKERID/*" </b>

![Screenshot 2024-11-07 at 21 34 49](https://github.com/user-attachments/assets/b333081c-89fa-4992-94a1-dac554cdf01f)

Войдем в профиль докер <b> docker login -u username </b>

![Screenshot 2024-11-07 at 21 35 00](https://github.com/user-attachments/assets/909a29ff-1566-4c92-8d2f-c47d45c27235)

Отправим в Docker Hub первую версию контейнера

<b> docker image push $DOCKERID/linux_tweet_app:1.0 </b>

![Screenshot 2024-11-07 at 21 35 25](https://github.com/user-attachments/assets/bac068dd-df18-4009-82a9-2968192fac65)

Отправим в Docker Hub вторую версию контейнера

<b> docker image push $DOCKERID/linux_tweet_app:2.0 </b>

![Screenshot 2024-11-07 at 21 35 35](https://github.com/user-attachments/assets/d5c8d070-5013-48b9-991d-24e62863085c)

Убеждаемся в том, что в профиле Docker Hub образы корректно отображаются

![Screenshot 2024-11-07 at 20 26 41](https://github.com/user-attachments/assets/4462b65f-74a6-42af-9c32-a94e2febb73d)

![Screenshot 2024-11-07 at 20 27 28](https://github.com/user-attachments/assets/c17909d3-b33f-4f66-b96c-8cd82833af0f)

