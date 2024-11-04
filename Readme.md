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
<p>В данномм задании изучается запуск контейнера</p>
<p>Выполним команду: </p>
docker container run alpine ls -l
<p>Результат выполнения команды</p>
![Screenshot 2024-11-04 at 22 27 06](https://github.com/user-attachments/assets/6c5366b6-4841-40df-b8cc-6232e6e6ac47)
<p> В результате выполнения комманды из ране згруженного образа linux alpine был запущен 
Docker контейнер, а также внутри линукс контейнера был запрошен список дииректорий, который был успшно выведен</p>

