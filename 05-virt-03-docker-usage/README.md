# Домашнее задание к занятию "5.3. Контейнеризация на примере Docker"
1.  
~/Docker ❯ docker run  -d -p 83:80 nginx                                       
8f15570062955269edb483fc5c1d2f2db49ca28cd37524e95241c9062641ab80  
~/Docker ❯ docker ps  
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS         PORTS                NAMES  
8f1557006295   nginx     "/docker-entrypoint.…"   10 seconds ago   Up 9 seconds   0.0.0.0:83->80/tcp     magical_mcnulty  
~/Docker ❯ docker exec -it 8f1557006295 bash  
root@8f1557006295:/usr/share/nginx/html# vim index.html  
![Docker](d1.png)  
