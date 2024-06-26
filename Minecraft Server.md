[[Шпора]]
Minecraft server 
apt install docker.io ( dnf install docker-ce)

``` bash
Docker run -d -p 25565:25565 --volume '/opt/mc/data:/data' --restart always -e EULA=true --name mc-junprofi itzg/minecraft-server 

nano /opt/mc/data/server.properties 

docker restart mc-junprofi
```


