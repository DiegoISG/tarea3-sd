Integrantes: Jose Arteaga, Diego Saavedra, Joaquin  Villalon


Este proyecto fue realizado utilizando el SO Ubuntu 20.04, una distrubución de Linnux basado en Debian.

Para poder iniciar el servidor, debe instalar los siguientes paquetes: Node.js - Express - Nodemon - npm

-Instalación de Node: en la consola debemos escribir los siguientes comandos y espera a que cada uno de ellos finalice: 
        
                      curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
                      sudo apt-get install -y nodejs
         En caso de no tener instalado curl, siga las indicaciones que se le mostraran en su consola.
         
Luego en la carpeta que haya clonado este repositorio, debe ejecutar el siguiente comando:
                      npm install
                      
Este comando descargara automanticamente todas las dependencias que requiere el proyecto, en este caso son express y nodemon.

Una vez completados estos pasos, su servidor estará listo para arrancar con el comando:  npm run dev

Ahora debemos instalar el balanceador de carga, para este caso haremos uso de NGINX, cuya instalación se realiza mediante el siguiente comando:
                      sudp apt update
                      sudo apt install nginx
                      
Ya tenemos instalado NGINX, ahora debemos configurarlo, para esto debemos introducir por consola las siguientes lineas de comando:
            
                      sudo touch /etc/nginx/conf.d/load-balancer.conf
                      sudo rm -r /etc/nginx/sites-enabled/default
                      sudo systemctl restart nginx
                      sudo nano /etc/nginx/conf.d/load-balancer.conf
          
Una vez llegado a este punto, podemos apreciar que el editor de texto __nano__ se habrá desplegado, dentro de este debemos fijar el siguiente archivo de configuración;
                        
                      upstream backend{
                        server localhost:3000;
                        server localhost:3001;
                        server localhost:3002;
                        }
                      server{
                        listen 80;
                        location /tarea3 {
                                proxy_pass http://backend;
                                }
                        }
                     
                      
Para guardar estos cambios, debemos oprimir CTRL+X, luego la letra __S__ y finalmente aceptar y abremos salido del editor de texto. Realizado esto, añadomos el siguiente comando por consola:
```


                       sudo systemctl restart nginx
```

Con esto tendremos operativo nuestro balanceador de carga.
Ahora debe ejecutar los 3 servidores, para esto una vez clonado este repositorio, debe arrancar los servidores indicando los puertos donde serán ejecutados, para esto debe abrir 3 terminales distintas dentro de la carpeta, y ejecutar los siguientes comandos, cada uno en una terminal distinta.
``` 
                      AQUI COMANDOS DEL JOAQUIN
```

Cabe recalcar que en nuestra tarea, la ruta de buscador si hace la verificación de si el búsqueda ya se encuentra en la cache, pero si no la encuentra, este accede directamente al archivo json donde se encuentra el inventario, esto debido a que no logramos implementar la comunicacion con mediante el metodo grpc con el servidor.
                    
          
          
          
