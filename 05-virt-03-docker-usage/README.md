# Домашнее задание к занятию "5.3. Контейнеризация на примере Docker"
1.  
```~/Docker ❯ docker run  -d -p 83:80 nginx   ```                                    
8f15570062955269edb483fc5c1d2f2db49ca28cd37524e95241c9062641ab80  
```~/Docker ❯ docker ps  ```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS         PORTS                NAMES  
8f1557006295   nginx     "/docker-entrypoint.…"   10 seconds ago   Up 9 seconds   0.0.0.0:83->80/tcp     magical_mcnulty  
```~/Docker ❯ docker exec -it 8f1557006295 bash  ```
root@8f1557006295:/usr/share/nginx/html# vim index.html  
![Docker](d1.png)  
```~/Docker ❯ tag nginx astkam/nginx:0.0.1  ```
```~/Docker ❯ docker push astkam/nginx:0.0.1  ```
The push refers to repository [docker.io/astkam/nginx]  
9959a332cf6e: Mounted from library/nginx  
f7e00b807643: Mounted from library/nginx  
f8e880dfc4ef: Mounted from library/nginx  
788e89a4d186: Mounted from library/nginx  
43f4e41372e4: Mounted from library/nginx  
e81bff2725db: Mounted from library/nginx  
0.0.1: digest: sha256:7250923ba3543110040462388756ef099331822c6172a050b12c7a38361ea46f size: 1570  
![Docker](hub.png)  
2.  
