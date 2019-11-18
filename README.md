# apshenniy_microservices
apshenniy microservices repository

### Homework 12 docker-2
##### Cоздаем новую ветку docker-2
```sh
git checkout -b docker-2
```
##### docker commands
```sh
docker version - версия докера
docker ps - список запущенных контейнеров
docker ps -a спикок всех контейнеров
docker images - список созраненных образов
docker start CONTAINER_ID (stop) запуск или остановка контейнера
docker attach - подсоединяет терминал к созданному контейнеру  / ( Ctrl + p, Ctrl + q ) позволяет выйти из контейнера не остановив его
docker exec -it <u_container_id> bash  - Запускает новый процесс внутри контейнера например bash
docker rm CONTAINER_ID - удаляет контейнер (ключ -f удаляет работающий контейнер)
docker rmi image_id - удаляет image
docker commit container_id yourName/imageName - создает image из контейнера
```
##### Запуск контейнера
```sh
docker run -it ubuntu:16.04 /bin/bash 
• -i – запускает контейнер в foreground режиме (docker attach)
• -d – запускает контейнер в background режиме
• -t создает TTY 
```
docker run = docker create + docker start + docker attach* 

#### GCP
Cоздаем новый проект docker в GCP  
gcloud init - инициализируем утилиту

##### Docker-Machine
```sh
docker-machine create <имя> - создание 
docker-machine rm <имя> - удаление
```
Имен может быть много, переключение между ними через eval $(docker-machine env <имя>). Переключение на локальный докер - eval $(docker-machine env --unset).

 Создание удаленного хоста с docker
```sh
export GOOGLE_PROJECT=docker-258409
docker-machine create --driver google \
--google-machine-image https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/family/ubuntu-1604-lts \
--google-machine-type n1-standard-1 \
--google-zone europe-west1-b \
docker-host
```
Проверяем, что хост создан
```sh
docker-machine ls
```
Переключаемся на удаленный хост
```sh
eval $(docker-machine env docker-host)
```
запускаем сборку образа
```sh
 docker build -t reddit:latest 
 ```
запускаем контейнер
```sh
docker run --name reddit -d --network=host reddit:latest
```
Настройка firewall'а
```sh
gcloud compute firewall-rules create reddit-app \
--allow tcp:9292 \
--target-tags=docker-machine \
--description="Allow PUMA connections" \
--direction=INGRESS
```
#### Docker hub
Аутентифицируемся командой 
```sh
docker login
```
ставим теэг и пушим
```sh
 docker tag reddit:latest <your-login>/otus-reddit:1.0
 docker push <your-login>/otus-reddit:1.0
```

