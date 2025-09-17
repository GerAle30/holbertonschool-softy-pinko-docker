# 🐳 Softy Pinko Docker Project

## 📋 Project Overview

This project demonstrates the evolution of a web application from a basic Docker container to a **horizontally scalable microservices architecture** with load balancing. Through 6 progressive tasks, we build a complete web application using Docker, Docker Compose, Nginx, Flask, and modern scaling techniques.

## 🎯 Learning Objectives

- **Containerization** with Docker
- **Microservices architectures**
- **Reverse proxy** and load balancing
- **Dynamic horizontal scaling**
- **Orchestration** with Docker Compose
- **Inter-container communication**

---

## 🚀 Architecture Evolution

### Task 0: Basic Container
```
Docker Container (Ubuntu) → "Hello, World!"
```

### Task 1: Back-end API
```
Docker Container (Flask) → REST API on port 5252
```

### Task 2: Front-end + Back-end
```
Front-end Container (Nginx) ←→ Back-end Container (Flask)
       Port 9000                     Port 5252
```

### Task 3: CORS Communication
```
Front-end (Nginx) ←--AJAX--> Back-end (Flask + CORS)
```

### Task 4: Docker Compose
```
docker-compose.yml
├── Front-end Service
├── Back-end Service
└── Automatic Networking
```

### Task 5: Proxy Server
```
Client → Proxy (Nginx:80) → Front-end (9000)
                          ↘ Back-end (5252)
```

### Task 6: Horizontal Scaling
```
Client → Proxy (Load Balancer) → Back-end-1
                               ↘ Back-end-2
                               ↘ Back-end-N
```

---

## 📁 Estructura del Proyecto

```
holbertonschool-softy-pinko-docker/
├── README.md
├── task0/
│   ├── Dockerfile
│   └── README.md
├── task1/
│   ├── Dockerfile
│   ├── api.py
│   └── README.md
├── task2/
│   ├── back-end/
│   │   ├── Dockerfile
│   │   └── api.py
│   └── front-end/
│       ├── Dockerfile
│       ├── softy-pinko-front-end/
│       └── softy-pinko-front-end.conf
├── task3/
│   ├── back-end/ (con CORS habilitado)
│   └── front-end/ (con AJAX dinámico)
├── task4/
│   ├── docker-compose.yml
│   ├── back-end/
│   └── front-end/
├── task5/
│   ├── docker-compose.yml
│   ├── proxy/
│   │   ├── Dockerfile
│   │   └── proxy.conf
│   ├── back-end/
│   └── front-end/
└── task6/
    ├── docker-compose.yml
    ├── 2-api-servers.txt
    ├── proxy/ (con load balancing)
    ├── back-end/
    └── front-end/
```

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Propósito | Task |
|------------|-----------|------|
| **Docker** | Containerización | Todos |
| **Docker Compose** | Orquestación | 4-6 |
| **Ubuntu** | Sistema base | 0-1 |
| **Nginx** | Servidor web/proxy | 2,5-6 |
| **Flask** | API REST | 1-6 |
| **Python** | Lenguaje backend | 1-6 |
| **HTML/CSS/JS** | Frontend | 2-6 |
| **jQuery** | AJAX dinámico | 3-6 |

---

## 📚 Detalles por Task

### 🎯 Task 0: Primer Contenedor Docker

**¿Qué hace?**
- Crea un contenedor básico con Ubuntu
- Imprime "Hello, World!" al ejecutarse

**¿Por qué se ve así?**
```bash
$ sudo docker run softy-pinko:task0
Hello, World!
```

**Conceptos aprendidos:**
- Dockerfile básico
- Comandos `RUN`, `CMD`
- Build y ejecución de contenedores

---

### 🎯 Task 1: API REST con Flask

**¿Qué hace?**
- Instala Python3 y Flask en Ubuntu
- Crea una API REST en el puerto 5252
- Endpoint `/api/hello` que retorna "Hello, World!"

**¿Por qué se ve así?**
```bash
$ curl http://localhost:5252/api/hello
Hello, World!
```

**Conceptos aprendidos:**
- Instalación de dependencias en Docker
- Exposición de puertos
- API REST básica
- Mapeo de puertos host:container

---

### 🎯 Task 2: Arquitectura Front-end + Back-end

**¿Qué hace?**
- **Back-end**: API Flask en contenedor separado
- **Front-end**: Servidor Nginx sirviendo sitio web estático
- Dos servicios independientes

**¿Por qué se ve así?**
```bash
# Front-end (sitio web)
http://localhost:9000

# Back-end (API)
http://localhost:5252/api/hello
```

**Conceptos aprendidos:**
- Separación de responsabilidades
- Múltiples contenedores
- Configuración de Nginx
- Arquitectura de microservicios básica

---

### 🎯 Task 3: Integración Dinámica con CORS

**¿Qué hace?**
- El front-end consume dinámicamente la API del back-end
- Habilita CORS para peticiones cross-origin
- JavaScript AJAX carga contenido dinámico

**¿Por qué se ve así?**
- El sitio web muestra "Hello, World!" dinámicamente cargado desde la API
- Sin CORS: Error de cross-origin
- Con CORS: Comunicación exitosa entre contenedores

**Conceptos aprendidos:**
- CORS (Cross-Origin Resource Sharing)
- Comunicación entre contenedores
- JavaScript AJAX
- Integración front-end/back-end

---

### 🎯 Task 4: Orquestación con Docker Compose

**¿Qué hace?**
- Un solo archivo `docker-compose.yml` maneja ambos servicios
- Networking automático entre contenedores
- Dependencias y orden de inicio

**¿Por qué se ve así?**
```bash
$ sudo docker compose up
# Inicia front-end y back-end automáticamente
# Misma funcionalidad, pero más fácil de manejar
```

**Conceptos aprendidos:**
- Docker Compose
- Definición declarativa de servicios
- Networking automático
- Gestión de dependencias

---

### 🎯 Task 5: Proxy Server (Reverse Proxy)

**¿Qué hace?**
- **Un solo punto de entrada**: Puerto 80
- El proxy Nginx enruta las peticiones:
  - `/` → Front-end (puerto 9000)
  - `/api` → Back-end (puerto 5252)
- Front-end y back-end **no son accesibles directamente**

**¿Por qué se ve así?**
```bash
# Todo a través del proxy
http://localhost          # Sitio web
http://localhost/api/hello  # API

# Estos YA NO funcionan (securidad)
http://localhost:9000     # ❌ Bloqueado
http://localhost:5252     # ❌ Bloqueado
```

**Conceptos aprendidos:**
- Proxy reverso
- Punto único de entrada
- Seguridad por capas
- Enrutamiento de tráfico
- Configuración upstream de Nginx

---

### 🎯 Task 6: Escalado Horizontal con Load Balancing

**¿Qué hace?**
- **Múltiples servidores API** ejecutándose simultáneamente
- **Load Balancer Round-Robin** distribuye peticiones
- Escalado dinámico: `--scale back-end=N`

**¿Por qué se ve así?**
```bash
$ sudo docker compose up --scale back-end=2

# Múltiples contenedores back-end
task6-back-end-1    # Servidor API #1
task6-back-end-2    # Servidor API #2

# Las peticiones se alternan:
Petición 1 → back-end-1
Petición 2 → back-end-2
Petición 3 → back-end-1
Petición 4 → back-end-2
```

**Logs del Load Balancer:**
```
back-end-1 | 172.18.0.5 - - [17/Sep/2025 19:59:36] "GET /api/hello HTTP/1.0" 200 -
back-end-2 | 172.18.0.5 - - [17/Sep/2025 19:59:38] "GET /api/hello HTTP/1.0" 200 -
back-end-1 | 172.18.0.5 - - [17/Sep/2025 19:59:40] "GET /api/hello HTTP/1.0" 200 -
back-end-2 | 172.18.0.5 - - [17/Sep/2025 19:59:42] "GET /api/hello HTTP/1.0" 200 -
```

**Conceptos aprendidos:**
- Escalado horizontal
- Load balancing (Round-Robin)
- Alta disponibilidad
- Distribución de carga
- Arquitectura escalable

---

## 🚀 Comandos de Ejecución

### Task 0-1: Contenedores individuales
```bash
cd task0
sudo docker build -t softy-pinko:task0 .
sudo docker run softy-pinko:task0
```

### Task 2-3: Múltiples contenedores
```bash
cd task2
sudo docker build -t back-end ./back-end
sudo docker build -t front-end ./front-end
sudo docker run -d -p 5252:5252 --name back-end back-end
sudo docker run -d -p 9000:9000 --name front-end front-end
```

### Task 4-5: Docker Compose
```bash
cd task4  # o task5
sudo docker compose build
sudo docker compose up -d
```

### Task 6: Escalado Horizontal
```bash
cd task6
sudo docker compose build
sudo docker compose up --scale back-end=2 -d
```

---

## 🌐 URLs de Acceso

### Task 2-3
- **Front-end**: http://localhost:9000
- **Back-end**: http://localhost:5252/api/hello

### Task 4
- **Front-end**: http://localhost:9000
- **Back-end**: http://localhost:5252/api/hello

### Task 5-6
- **Todo a través del proxy**: http://localhost
- **API a través del proxy**: http://localhost/api/hello

---

## 🔍 ¿Por Qué Cada Step?

### 🎯 **Progresión Lógica del Proyecto**

1. **Task 0-1**: Fundamentos de Docker
2. **Task 2**: Separación de servicios (microservicios)
3. **Task 3**: Comunicación entre servicios
4. **Task 4**: Simplificación con orquestación
5. **Task 5**: Seguridad y punto único de entrada
6. **Task 6**: Escalabilidad y alta disponibilidad

### 🏗️ **Arquitectura Real**
Esta progresión refleja cómo se desarrollan aplicaciones reales:

- **Netflix**: Miles de microservicios con load balancers
- **Amazon**: Proxy servers para millones de peticiones
- **Google**: Escalado horizontal masivo

---

## 💡 Conceptos Clave Aprendidos

### 🐳 **Docker**
- Containerización de aplicaciones
- Aislamiento de dependencias
- Portabilidad entre entornos

### 🏗️ **Arquitectura**
- Monolítico → Microservicios
- Separación de responsabilidades
- Comunicación entre servicios

### ⚖️ **Escalabilidad**
- Escalado vertical vs horizontal
- Load balancing algorithms
- Alta disponibilidad

### 🔒 **Seguridad**
- Proxy como firewall
- Exposición mínima de puertos
- Principio de menor privilegio

### 🔧 **DevOps**
- Infrastructure as Code
- Orquestación de contenedores
- Automatización de despliegues

---

## 🎯 Aplicaciones en el Mundo Real

### 🌟 **E-commerce**
```
Cliente → Load Balancer → Web Servers (1-N)
                       → API Servers (1-N)
                       → Database Servers
```

### 🌟 **Redes Sociales**
```
Usuario → CDN → Proxy → Auth Service
                     → Feed Service (escalado)
                     → Media Service (escalado)
```

### 🌟 **Streaming**
```
Viewer → Load Balancer → Video Servers (1000s)
                      → Metadata API (100s)
                      → User Service (100s)
```

---

## 📊 Métricas y Monitoreo

### Task 6: Observabilidad
```bash
# Ver logs de load balancing
sudo docker compose logs --follow back-end

# Ver estado de contenedores
sudo docker compose ps

# Estadísticas en tiempo real
sudo docker stats
```

---

## 🏆 Logros Completados

- ✅ **Containerización** básica
- ✅ **API REST** con Flask
- ✅ **Frontend** con Nginx
- ✅ **Comunicación CORS** entre servicios
- ✅ **Orquestación** con Docker Compose
- ✅ **Proxy reverso** para seguridad
- ✅ **Load balancing** Round-Robin
- ✅ **Escalado horizontal** dinámico

---

## 🌟 Próximos Pasos (Bonus)

### 🚀 **Posibles Mejoras**
- **Kubernetes**: Orquestación avanzada
- **Monitoring**: Prometheus + Grafana
- **CI/CD**: GitHub Actions + Docker
- **Database**: PostgreSQL en contenedor
- **Cache**: Redis para performance
- **SSL/TLS**: HTTPS con certificados

### 📚 **Conceptos Avanzados**
- **Service Mesh** (Istio)
- **API Gateway**
- **Circuit Breakers**
- **Blue-Green Deployments**

---

## 👥 Créditos

**Proyecto**: Holbertonschool Softy Pinko Docker  
**Autor**: Alejandro  
**Tecnologías**: Docker, Nginx, Flask, Python, HTML/CSS/JS  
**Arquitectura**: Microservicios con escalado horizontal  

---

*🐳 "De un simple 'Hello World' a una arquitectura escalable de clase empresarial"*
