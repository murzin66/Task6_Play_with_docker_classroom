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


