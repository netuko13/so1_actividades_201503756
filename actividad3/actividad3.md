## Datos del estudiante
- **Estudiante:** Carlos Ernesto Fuentes Rasique
- **Carnet:** 201503756
- **Fecha:** 27/02/2023

## Problema problema

El problema que no carguen algunas de las páginas del frontend se debe a la configuración de nginx que trae por defecto.

## Solución
 Para darle solución a este inconveniente es necesario crear un archivo llamado ```nginx.conf``` este archivo contiene cierta configuración que permite localizar las direcciones de la aplicación.

Este es el código del archivo ```nginx.conf```

 ```
 events {
    worker_connections 1024;
}
http {
  server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
    }
  }
}
 ```

Una vez creado el archivo de configuración, se debe copiar este archivo en la ubicación por defecto en la image que vamos a construir de nginx.
 
Para esto se agrega esta línea de código en el archivo ```nginx.Dockerfile```

```docker

COPY nginx.conf /etc/nginx/conf.d/default.conf
```

Por último se construye la imagen

```
docker build -t mifrontend:0.1.0 -f nginx.Dockerfile .
```