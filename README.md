# Backend Ventas - Innovatech Chile

## Descripción

Microservicio backend encargado de la gestión de ventas del sistema Innovatech Chile.

Fue desarrollado con Spring Boot y desplegado en una instancia EC2 privada dentro de AWS. El servicio se comunica con una base de datos MySQL ubicada en una capa de datos independiente.

## Tecnologías utilizadas

- Java 17
- Spring Boot
- Spring Data JPA
- Maven
- MySQL 8
- Docker
- AWS EC2
- AWS ECR

## Arquitectura

El backend de ventas se ejecuta en una instancia EC2 privada dentro de la VPC.

Puerto interno utilizado:

```txt
8080
```
La aplicación NO posee acceso público desde Internet. Solo recibe tráfico interno desde el frontend mediante proxy Nginx.

## Base de datos

El backend se conecta a MySQL mediante la IP privada de la instancia DATA:
10.0.2.218:3306

Base de datos utilizada:
ventas_db

## Variables de entorno
SPRING_DATASOURCE_URL=jdbc:mysql://10.0.2.218:3306/ventas_db
SPRING_DATASOURCE_USERNAME=ventas_user
SPRING_DATASOURCE_PASSWORD=ventas_pass

## Docker

Construcción de imagen:
docker build -t back-ventas .

Ejecución local:
docker run -p 8080:8080 back-ventas

## Swagger

Validación local del servicio:
http://localhost:8080/swagger-ui.html

## Despliegue AWS

Imagen publicada en Amazon ECR:
160661694072.dkr.ecr.us-east-1.amazonaws.com/back-ventas:latest

Despliegue realizado mediante Docker Compose en EC2 privada.

## Seguridad

- Backend desplegado en subred privada.
- Sin IP pública.
- Acceso permitido únicamente desde la capa Frontend.
- Comunicación interna mediante Security Groups y red privada VPC.

## Evidencias validadas

Se comprobó correctamente:

- Ejecución del contenedor Docker.
- Conectividad Backend → MySQL.
- Respuesta Swagger HTTP 302.
- Comunicación Frontend → Backend mediante proxy Nginx.