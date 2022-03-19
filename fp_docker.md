# fp_docker - работа faceplate через docker.

Запускаем докер, и следующие команды выполняем: 
docker start -i eecomet22.3 
Затем директорию
Затем    ./test_shell

1. Установить докер.
2. В терминале докера
sudo docker run -p 9000:9000 -p 8000:8000 -it --name ecomet22.3 -v /home/roman/PROJECTS:/opt/ext vzroman/erlang_ecomet:otp22.3 

но только вместо /home/roman/PROJECTS прописать произвольный путь.

3. ssh-keygen -t rsa -b 2048 -C "aliya_docker"
Вместо "aliya_docker" можно что угодно написать, это просто комент

4. скопировать и вставить в https://git.faceplate.io/-/profile/keys

5. ssh -T git@git.faceplate.io

6. git clone git@git.faceplate.io:fp/faceplate.git -b develop

7. ./rebar3 compile

