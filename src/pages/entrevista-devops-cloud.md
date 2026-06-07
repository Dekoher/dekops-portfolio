---
layout: ../layouts/Layout.astro
title: "KIT DE ENTREVISTA TÉCNICA: DEVOPS / CLOUD"
---

# 📋 KIT DE ENTREVISTA TÉCNICA: DEVOPS / CLOUD
> **Autor:** Academia @jemjaf
> **Enfoque:** Guía de evaluación para el entrevistador técnico. Diseñado para calibrar conocimientos en perfiles Junior (Jr) y Semi-Senior (SSR).
> **Duración recomendada:** 45–60 minutos.

---

## 🧠 METODOLOGÍA DE EVALUACIÓN

Esta guía contiene preguntas estructuradas en bloques. Cada pregunta tiene un nivel objetivo y pistas de evaluación para diferenciar entre un candidato puramente teórico (que memorizó definiciones) y uno operativo (que ha solucionado problemas reales).

*   **Junior (Jr):** Entiende conceptos básicos de red, almacenamiento, Docker y pipelines. Necesita guía para tareas de arquitectura.
*   **Semi-Senior (SSR):** Diseña pipelines, optimiza contenedores, maneja infraestrucutra como código estructurada y soluciona incidentes de forma autónoma.
*   **SSR Avanzado (ex-Senior adaptado):** Resuelve drifts de estado, optimiza costos sistémicos, aplica parches complejos en clústeres restringidos y diseña con OIDC y Workload Identity.

---

## 🗂️ BLOQUE 1: INTRODUCCIÓN & FIT CULTURAL

### 1. Apertura
*   **Pregunta:** Preséntate en 2–3 minutos — quién eres, cuál es tu stack dominante y qué traes a la mesa.
*   **Criterio de Evaluación:**
    *   **Qué observar:** Claridad narrativa y si prioriza lo relevante en su historial.
    *   **⚠️ Red Flag:** 4+ años de experiencia y no logra sintetizar su background en menos de 5 minutos (problema típico al explicar incidentes más adelante).
    *   **🟢 Señal Positiva:** Hilo conductor claro, stack dominante definido y proyectos puntuales explicados de forma concisa.

### 2. Background
*   **Pregunta:** ¿Cómo llegaste al área de DevOps/Cloud? ¿Desde cuándo trabajas de forma profesional en ello?
*   **Criterio de Evaluación:**
    *   **Qué observar:** Años reales operando frente a años "solo teniendo acceso a la consola".
    *   **⚠️ Red Flag:** Dice tener 3 años pero en su primer año solo creaba branches o editaba código de desarrollo sin tocar la infraestructura.
    *   **🟢 Señal Positiva:** Puede ubicar hitos específicos y proyectos concretos por año. Para perfiles Jr, el trabajo autónomo (labs, homelabs) pesa bastante.

### 3. Motivación del Cambio
*   **Pregunta:** ¿Por qué te interesa esta posición concretamente? ¿Por qué estás buscando un cambio laboral en este momento?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** Respuestas genéricas como *"quiero aprender nuevas tecnologías"* sin citar nada específico del rol, o hablar mal de su empleador anterior de manera no constructiva.
    *   **🟢 Señal Positiva:** Menciona un proyecto, reto técnico, stack o arquitectura específica que maneja el equipo y donde desea aportar.

### 4. Mayor Orgullo Técnico
*   **Pregunta:** Describe el proyecto técnico del que más te sientas orgulloso en los últimos 12 meses. ¿Qué rol tuviste y qué problemas resolviste?
*   **Criterio de Evaluación:**
    *   **Qué observar:** Rol específico ("yo diseñé X") frente al uso constante de plurales indefinidos ("hicimos", "desplegamos").
    *   **🟢 Señal Positiva:** Identifica decisiones arquitectónicas propias, tradeoffs analizados y cuantifica el impacto del proyecto con métricas de negocio o ahorro de infraestructura.

### 5. Gestión de Incidentes
*   **Pregunta:** Cuéntame sobre un fallo o incidente grave en producción donde hayas sido responsable directa o indirectamente. ¿Qué pasó, cómo lo contuviste y qué aprendiste?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** *"Nunca rompí nada en producción"* (falta de exposición real) o *"fue culpa del equipo de desarrollo/proveedor"* (falta de ownership).
    *   **🟢 Señal Positiva:** Admite el error con honestidad, detalla los pasos de mitigación rápida y, sobre todo, explica las acciones posteriores para que no vuelva a suceder (postmortem y automatización).

### 6. Autoevaluación del Stack
*   **Pregunta:** De tu stack de herramientas actual, ¿cuál dominas en profundidad y cuál consideras que estás aprendiendo?
*   **Criterio de Evaluación:**
    *   **Qué observar:** Autenticidad y madurez para admitir brechas frente al perfil que dice ser "experto avanzado en todo".
    *   **🟢 Señal Positiva:** Delimita claramente sus fuertes y las herramientas donde está haciendo laboratorios para crecer.

### 7. Colaboración con Desarrollo
*   **Pregunta:** ¿Cómo trabajas con los desarrolladores? Dame un ejemplo de una fricción o desacuerdo con ellos y cómo lo resolviste.
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** Ver a DevOps como el "portero de seguridad" que bloquea accesos e insiste en que *"los desarrolladores no entienden nada"*.
    *   **🟢 Señal Positiva:** Propone soluciones autoservicio (módulos, documentación, plantillas) para empoderar al equipo en lugar de crear cuellos de botella manuales.

### 8. Criterio de Salud Operativa
*   **Pregunta:** ¿Cómo sabes que tu infraestructura y aplicaciones están funcionando correctamente en este momento en producción?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** *"Revisamos cuando los usuarios reportan un fallo"* o *"el equipo de QA está monitoreando en su turno"*.
    *   **🟢 Señal Positiva:** Menciona dashboards activos, alertas configuradas por canales (Slack/Teams), métricas de Golden Signals (latencia, tasa de error) y runbooks.

### 9. Madurez en Producción
*   **Pregunta:** ¿Alguna vez tuviste que revertir (hacer rollback) un cambio en producción? ¿Cómo lo hiciste y qué precauciones tomaste?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** Hacer hotfixes directos sobre producción en caliente sin un proceso de rollback configurado o probado previamente en Staging.
    *   **🟢 Señal Positiva:** Describe un proceso automatizado con validación rápida, versionado de imágenes y postmortem.

### 10. Seguridad Crítica (Urgente)
*   **Pregunta:** Encontrás una access key de AWS hardcodeada en un repositorio público de GitHub. ¿Qué haces en los próximos 10 minutos?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** Responder que lo primero es *"borrar el archivo del repositorio"* o *"reescribir el historial de Git"*. Eso no sirve; la clave ya fue comprometida por bots de escaneo automatizado.
    *   **🟢 Señal Positiva:** El orden de respuesta correcto es:
        1. Desactivar o revocar la clave en IAM inmediatamente (prioridad absoluta).
        2. Revisar los logs (ej. CloudTrail) para evaluar si hubo uso malicioso y el alcance.
        3. Eliminar la clave del repositorio histórico de Git.
        4. Rotar las credenciales en los sistemas correspondientes.

---

## ☁️ BLOQUE 2: AWS / CLOUD · REDES · SEGURIDAD

### 11. Redes Básicas (Jr)
*   **Pregunta:** ¿Cuál es la diferencia entre un Security Group y una NACL? ¿Cuándo necesitarías usar ambos a la vez?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** SG es a nivel de instancia y con estado (stateful - solo permite reglas de permitir). NACL es a nivel de subred y sin estado (stateless - permite reglas de permitir y denegar).
    *   **🟢 Caso combinado:** Usas NACL para denegar un rango de IPs maliciosas detectadas a nivel de subred, y Security Groups para administrar los puertos específicos permitidos para cada contenedor.

### 12. Redes Avanzadas (Jr)
*   **Pregunta:** ¿Qué hace exactamente que una subred sea "pública" en AWS?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** *"Es pública porque le asignamos IPs públicas a las instancias"*.
    *   **🟢 Respuesta Correcta:** Es pública porque su tabla de ruteo tiene una ruta explícita hacia el Internet Gateway (`0.0.0.0/0 -> igw-xxx`). La asignación de la IP pública es consecuencia, no la causa de la definición de la red.

### 13. Identity and Access Management (Jr)
*   **Pregunta:** ¿Cuál es la diferencia entre un Rol y una Política en IAM? ¿Cuándo asignas un rol frente a una política directa?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** La política define permisos (JSON). El rol es una identidad que puede ser asumida de forma temporal por servicios o usuarios federados.
    *   **🟢 Buena práctica:** Asignar roles a las instancias de cómputo (EC2, ECS tasks) en lugar de inyectar claves estáticas.

### 14. Almacenamiento (Jr)
*   **Pregunta:** ¿Cuáles son las diferencias entre EBS y EFS? ¿Cuándo usarías cada uno?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** EBS es almacenamiento de bloque acoplado a una sola instancia a la vez (baja latencia). EFS es un sistema de archivos compartido (NFS) al que pueden conectarse múltiples instancias simultáneamente.

### 15. Alta Disponibilidad en DB (Jr)
*   **Pregunta:** ¿Cuál es la diferencia entre RDS Multi-AZ y una Read Replica? ¿Cuál usas para alta disponibilidad y cuál para performance?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Multi-AZ es réplica síncrona en otra zona de disponibilidad para recuperación ante fallos (HA - alta disponibilidad) sin lectura directa. Read Replica es réplica asíncrona para escalar lecturas.

### 16. Buenas Prácticas S3 (Jr)
*   **Pregunta:** Un desarrollador necesita que un bucket de S3 sea accesible públicamente para servir imágenes, pero la cuenta tiene "Block Public Access" activo a nivel global por compliance de seguridad. ¿Qué haces?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** *"Desactivo la restricción de Block Public Access y pongo el bucket como público"*.
    *   **🟢 Respuesta Correcta:** Mantengo el bucket privado, configuro CloudFront apuntando al bucket mediante **OAC (Origin Access Control)** y expongo las imágenes por HTTPS usando la CDN de CloudFront.

### 17. Balanceadores de Carga (Jr)
*   **Pregunta:** ¿Cuál es la diferencia entre un Application Load Balancer (ALB) y un Network Load Balancer (NLB)?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** ALB opera en capa 7 (HTTP/HTTPS) permitiendo ruteo avanzado por URLs y cabeceras. NLB opera en capa 4 (TCP/UDP) ofreciendo latencia ultra baja e IPs fijas.

### 18. Redes y Salida a Internet (SSR)
*   **Pregunta:** ¿Cuál es la diferencia entre Internet Gateway y NAT Gateway? Si tienes una instancia en una subred privada con IP pública y su tabla de ruteo apunta a un IGW, ¿tiene salida a internet?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** IGW permite tráfico bidireccional (público). NAT GW solo permite salida hacia internet desde subredes privadas.
    *   **Respuesta al caso:** No tiene salida. Si su tabla de ruteo apunta al IGW, la subred se comporta como pública, pero al no tener una IP pública mapeada correctamente en la tabla de ruteo bidireccional para responder, la conexión fallará.

### 19. Seguridad en ECS (SSR)
*   **Pregunta:** En ECS, ¿cuántos roles IAM necesita una tarea (task) y qué permisos maneja cada uno?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:**
        1. **Task Execution Role:** Usado por el agente de ECS para descargar la imagen de ECR y subir logs a CloudWatch.
        2. **Task Role:** Permisos del código interno de la aplicación para interactuar con otros servicios de AWS (S3, base de datos).

### 20. Seguridad en Despliegues Externos (SSR Avanzado)
*   **Pregunta:** ¿Cómo diseñas los permisos de AWS para un pipeline externo (como GitHub Actions) que realiza deploys en tu cuenta de nube sin usar credenciales fijas?
*   **Criterio de Evaluación:**
    *   **🟢 Respuesta Correcta:** Implementar OIDC (OpenID Connect). Se configura GitHub como Identity Provider confiable en IAM de AWS, y el pipeline asume un rol temporal a través de un intercambio STS sin almacenar claves estáticas en los secretos del repositorio.

---

## 🏗️ BLOQUE 3: TERRAFORM / IaC

### 21. Variables vs Locals (Jr)
*   **Pregunta:** ¿Qué son los `locals` en Terraform? ¿Cuál es la diferencia con una variable de entrada?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Variables son parámetros que inyectas desde afuera (configurables por entorno). Locals son valores calculados internamente dentro de los archivos del módulo y no pueden ser alterados directamente.

### 22. Estado Remoto (Jr)
*   **Pregunta:** ¿Cómo manejas el estado remoto (state) de Terraform en un equipo? ¿Cómo evitas conflictos si dos personas ejecutan apply al mismo tiempo?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Se usa un remote backend (S3/Azure Blob). El bloqueo de estado se hace con DynamoDB o lockfiles nativos para evitar sobreescritura accidental.

### 23. Destrucción Accidental (Jr)
*   **Pregunta:** ¿Cómo evitas desde el código de Terraform que un destroy accidental elimine una base de datos en producción?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Configurar `lifecycle { prevent_destroy = true }` dentro del bloque del recurso en Terraform.

### 24. Estructura de Entornos (SSR)
*   **Pregunta:** ¿Cómo estructuras tus carpetas y módulos en Terraform para soportar desarrollo, Staging y Producción sin duplicar código?
*   **Criterio de Evaluación:**
    *   **Qué observar:** Estructura modular versus workspaces. Workspaces comparten el backend del estado, lo que puede ser un riesgo de seguridad en producción.
    *   **🟢 Buena práctica:** Estructura de directorios dedicada por ambiente (`env/dev/`, `env/prod/`) llamando a módulos versionados compartidos en una carpeta `modules/`, o el uso de Terragrunt.

### 25. Grafos de Dependencias (SSR)
*   **Pregunta:** ¿Cuál es la diferencia entre dependencias implícitas y explícitas en Terraform? ¿Cuándo es necesario usar `depends_on`?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Implícita es autodetectada por referencias del código. Explícita se fuerza con `depends_on` cuando un recurso necesita que otro exista pero no hay relación de atributos en el código (ej. adjuntar políticas IAM dinámicas).

### 26. Bucles de Recursos (SSR)
*   **Pregunta:** ¿Cómo usas `for_each` vs `count` para crear múltiples recursos? ¿Qué problemas trae usar `count` asociado a listas?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** `count` asocia índices numéricos. Si eliminas un recurso intermedio, todos los índices posteriores cambian de número y Terraform intentará recrearlos. `for_each` usa llaves únicas, por lo que es mucho más seguro para refactorizar.

### 27. Refactorización del Estado (SSR Avanzado)
*   **Pregunta:** Si necesitas renombrar o mover un recurso en Terraform que ya existe en producción, ¿cómo lo haces sin que intente destruirlo y recrearlo?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Uso el comando `terraform state mv` en la CLI de forma local para alinearlo.
    *   **🟢 Enfoque moderno:** Usar bloques `moved` directamente en el código HCL (en versiones recientes de Terraform) para automatizar la migración del estado de forma segura.

---

## 🐳 BLOQUE 4: DOCKER / CONTENEDORES

### 28. Comportamientos por Defecto (Jr)
*   **Pregunta:** Si ejecutas `docker pull nginx` sin tags ni especificaciones, ¿qué imagen se descarga y por qué es una mala práctica en producción?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Se descarga `docker.io/library/nginx:latest`. En producción es peligroso porque `latest` cambia dinámicamente y puede romper el entorno en el próximo reinicio o escalado del nodo.

### 29. Privilegios de Contenedor (Jr)
*   **Pregunta:** ¿Qué usuario ejecuta el proceso por defecto dentro de un contenedor si no especificas ninguno en el Dockerfile? ¿Qué riesgo tiene?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Corre como root (UID 0). Si hay una vulnerabilidad en el contenedor que compromete el namespace de aislamiento, el atacante obtiene privilegios de root directamente sobre la máquina host.

### 30. Construcción de Dockerfiles (Jr)
*   **Pregunta:** ¿Por qué copiamos los archivos de dependencias e instalamos los paquetes antes de copiar el código fuente completo de la aplicación?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Para aprovechar el caché de capas de Docker. Si el código fuente cambia pero las dependencias no, Docker reutiliza la capa de instalación de paquetes, reduciendo el tiempo de build drásticamente.

### 31. Directivas de Dockerfile (Jr)
*   **Pregunta:** ¿Cuál es la diferencia entre `COPY` y `ADD` en un Dockerfile?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** `COPY` transfiere archivos locales al contenedor sin alterar nada. `ADD` permite descargar archivos desde URLs y desempaqueta archivos comprimidos (`.tar.gz`) de forma automática.

### 32. Optimización y Seguridad (SSR)
*   **Pregunta:** ¿Qué es un multi-stage build? ¿Cómo reduce el tamaño de la imagen final?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Permite dividir la compilación de la imagen en etapas. Se compila con dependencias pesadas y luego se copian únicamente los binarios limpios al contenedor final (minimalista), reduciendo el tamaño de gigabytes a megabytes.

### 33. Dependencias de Sistema (SSR)
*   **Pregunta:** ¿Qué impacto tiene usar imágenes basadas en Alpine (musl) al compilar aplicaciones de Python con librerías en C como numpy o pandas?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Alpine no usa `glibc`, usa `musl libc`. Muchas librerías compiladas en C esperan `glibc`, por lo que `pip` se ve forzado a compilar desde código fuente dentro del contenedor. El build tarda mucho más y requiere instalar herramientas de compilación pesadas (gcc), resultando a menudo en una imagen más pesada que usar `slim` de Debian.

### 34. Análisis y Troubleshooting (SSR Avanzado)
*   **Pregunta:** Un contenedor en producción está al 100% de CPU. Sin reiniciarlo ni matarlo, ¿cómo investigas el proceso que causa el fallo en vivo?
*   **Criterio de Evaluación:**
    *   **🟢 Métodos válidos:**
        *   `docker exec -it <container> top` para ver la lista de procesos internos.
        *   `docker stats` para ver el uso de CPU de forma rápida en el host.
        *   `nsenter` para asociarse al PID del contenedor desde el host y analizar los hilos de ejecución de la máquina.

---

## ☸️ BLOQUE 5: KUBERNETES

### 35. Conceptos Core (Jr)
*   **Pregunta:** ¿Qué es un Pod y en qué se diferencia de un contenedor individual de Docker?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Un Pod es la unidad mínima en Kubernetes. Puede contener uno o más contenedores que comparten almacenamiento, namespace de red y la misma dirección IP.

### 36. Servicios (Jr)
*   **Pregunta:** ¿Cuál es la diferencia entre un servicio `ClusterIP` y un `NodePort`?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** `ClusterIP` expone el servicio en una IP interna del clúster (solo accesible internamente). `NodePort` expone el servicio en un puerto específico de cada nodo físico (accesible externamente).

### 37. Controladores (Jr)
*   **Pregunta:** ¿Diferencia entre Deployment y DaemonSet? Dame un caso de uso para DaemonSet.
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Deployment levanta N réplicas distribuidas por el clúster. DaemonSet garantiza exactamente un pod por cada nodo del clúster.
    *   **🟢 Caso de uso:** Agentes de monitoreo de infraestructura (Prometheus Node Exporter) o recolectores de logs (Fluentd) que necesitan residir en todos los servidores host.

### 38. Ciclo de Vida y Recursos (SSR)
*   **Pregunta:** ¿Qué son requests y limits? Si un pod supera su límite de memoria (RAM) vs su límite de CPU, ¿qué ocurre en cada caso?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Requests es lo reservado para arrancar; Limits es el techo máximo permitido.
    *   **🟢 Comportamiento clave:** Si supera el límite de RAM, el contenedor es eliminado de inmediato por el kernel del sistema (**OOMKilled**). Si supera el límite de CPU, se le aplica estrangulamiento de ciclos de procesamiento (**CPU throttling**), ralentizando la app pero sin apagar el proceso.

### 39. Manejo de Secretos (SSR)
*   **Pregunta:** ¿Para qué sirven los Secrets de Kubernetes? ¿Son seguros por defecto?
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** Pensar que los Secrets de K8s están cifrados por defecto de forma segura.
    *   **🟢 Respuesta Correcta:** Los Secrets están codificados únicamente en base64. Si alguien tiene acceso al etcd o lectura de manifiestos, los puede decodificar fácilmente. Deben protegerse usando cifrado en reposo en etcd y herramientas como External Secrets Operator integradas con AWS Secrets Manager/Azure Key Vault.

### 40. Ecosistema de Redes (SSR Avanzado)
*   **Pregunta:** ¿Qué alternativas tienes tras el fin de soporte del Ingress Nginx de la comunidad en 2026?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Migrar hacia controladores mantenidos comercialmente (como Nginx Inc) u otros proxies de Ingress (Traefik, Envoy, etc.).
    *   **🟢 Respuesta ideal:** Estudiar la adopción de **Gateway API** como el sucesor de la especificación de Ingress para Kubernetes.

### 41. Planificación de Carga (SSR Avanzado)
*   **Pregunta:** ¿Qué son los taints y tolerations? ¿Cómo los usarías en conjunto con node pools?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Taints repelen pods de ciertos nodos si estos no tienen la tolerancia correspondiente configurada. Sirve para segregar nodos específicos (como pools con GPUs o instancias spot baratas) para cargas de trabajo específicas.

---

## 🔁 BLOQUE 6: CI/CD & AUTOMATIZACIÓN

### 42. Flujos de GitOps (Jr)
*   **Pregunta:** ¿Qué es GitOps y en qué se diferencia del flujo tradicional de despliegue por "push" desde la CI?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** En GitOps, el repositorio es el origen de la verdad y un agente interno del clúster (ArgoCD/Flux) jala (*pull*) y reconcilia el estado. En el modelo tradicional, la CI tiene las credenciales del clúster y realiza un empuje activo (*push*).

### 43. Gestión de Secretos en CI (Jr)
*   **Pregunta:** ¿Cómo manejas las variables sensibles en pipelines para evitar que se muestren en los logs públicos?
*   **Respuesta básica:** Uso de secretos protegidos integrados en las plataformas (GitHub Secrets / GitLab CI variables) que son enmascarados de forma automática por la salida estándar del pipeline.

### 44. Optimización de Pipelines (SSR)
*   **Pregunta:** Si un pipeline de integración tarda 45 minutos y bloquea el flujo del equipo de desarrollo, ¿qué estrategias propones para reducirlo a menos de 10 minutos?
*   **Criterio de Evaluación:**
    *   **Estrategias válidas:** Cacheo de dependencias de código, paralelización de tareas independientes, uso de imágenes base precompiladas con herramientas requeridas, y Test Impact Analysis (correr solo pruebas afectadas por el cambio).

### 45. Rollback Automático (SSR)
*   **Pregunta:** ¿Cómo diseñas una estrategia de rollback automático si un deploy falla tras pasar a producción?
*   **Criterio de Evaluación:**
    *   **🟢 Enfoques:** Configurar políticas de despliegue como Canary o Blue-Green, integradas con health checks automáticos del balanceador de carga o Ingress, que reviertan automáticamente el tráfico al grupo de servidores anterior si detectan códigos de error 5xx.

### 46. Políticas de Seguridad (SSR Avanzado)
*   **Pregunta:** ¿Cómo integrarías un análisis de seguridad automatizado que bloquee el pipeline si detecta violaciones críticas en tu infraestructura como código?
*   **Criterio de Evaluación:**
    *   **Respuestas válidas:** Integración de herramientas como Checkov, Trivy o tfsec en la fase previa al plan de Terraform, configuradas para fallar el stage si encuentran recursos desprotegidos (ej. buckets S3 abiertos al público).

---

## 📈 BLOQUE 7: OBSERVABILIDAD & OPERACIONES

### 47. Los Tres Pilares (Jr)
*   **Pregunta:** ¿Cuáles son los tres pilares de la observabilidad y cuál es su diferencia básica?
*   **Respuesta básica:**
    *   **Logs:** Registro de eventos individuales en formato texto.
    *   **Métricas:** Valores numéricos agregados que miden uso de recursos en el tiempo (CPU, RAM).
    *   **Trazas:** Flujo y latencia de una petición a través de los componentes del sistema.

### 48. Herramientas Estándar (Jr)
*   **Pregunta:** ¿Qué rol juegan Prometheus y Grafana? ¿Cuál recolecta y cuál visualiza?
*   **Respuesta básica:** Prometheus realiza la recolección activa de métricas y la evaluación de alertas. Grafana lee desde Prometheus y se encarga puramente de la visualización en dashboards.

### 49. Instrumentación (Jr)
*   **Pregunta:** ¿Qué significa instrumentar una aplicación?
*   **Respuesta básica:** Añadir código para emitir métricas personalizadas de negocio, trazas de OpenTelemetry o estructuración de logs de aplicación.

### 50. Autoescalado por Eventos (SSR)
*   **Pregunta:** ¿Qué es KEDA y cuándo usarías autoescalado por eventos en lugar del tradicional por CPU (HPA)?
*   **Criterio de Evaluación:**
    *   **🟢 Respuesta Correcta:** HPA escala en base a recursos del sistema (CPU/RAM). KEDA permite escalar pods basándose en eventos externos, como el número de mensajes pendientes en una cola (SQS/Kafka). Si un servicio procesa colas, CPU baja no significa que no haya trabajo pendiente.

### 51. Mitigación de Alertas Fatigue (SSR Avanzado)
*   **Pregunta:** ¿Qué criterios sigues para diseñar una estrategia de alertas y evitar la fatiga por alertas?
*   **Criterio de Evaluación:**
    *   **Principios de diseño:** Solo alertar por síntomas orientados a la experiencia del usuario (ej. incremento en tiempos de respuesta HTTP) en lugar de causas secundarias (ej. uso temporal de CPU al 90%), y agrupar alertas duplicadas.

---

## ⚡ BLOQUE 8: TRAMPAS DE VANGUARDIA

### 52. Estructura de Compose (Jr/SSR)
*   **Pregunta:** ¿Cómo nombras tu archivo de Docker Compose y qué pasa con la cabecera `version` hoy en día?
*   **Criterio de Evaluación:**
    *   **🟢 Respuesta Correcta:** En Compose v2, el nombre estándar recomendado es `compose.yaml`. La cabecera `version: '3.x'` está obsoleta y se ignora por completo. Usarla genera warnings en herramientas actualizadas.

### 53. Reconciliación GitOps (SSR)
*   **Pregunta:** Si alguien edita manualmente un recurso dentro de Kubernetes usando `kubectl edit`, ¿qué ocurre si el clúster es administrado por ArgoCD?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** ArgoCD detecta la divergencia (estado OutOfSync) y, según su política, sobreescribirá el cambio manual para mantener el estado deseado en Git.

### 54. Redes en AWS (SSR)
*   **Pregunta:** ¿Cuándo elegirías un Transit Gateway frente a múltiples conexiones VPC Peering?
*   **Criterio de Evaluación:**
    *   **Respuesta básica:** Peering es una conexión directa 1 a 1 sin costo fijo por hora. Transit Gateway actúa como un hub centralizado; es preferible cuando se escalan muchas VPCs para evitar crear una malla de conexiones complejas.

### 55. IA en DevOps (Jr/SSR)
*   **Pregunta:** ¿Qué herramientas de inteligencia artificial usas en tu día a día técnico? Dame un caso real que hayas resuelto esta semana.
*   **Criterio de Evaluación:**
    *   **⚠️ Red Flag:** Respuestas vagas como *"solo estoy explorando herramientas"* en un entorno técnico dinámico.
    *   **🟢 Señal Positiva:** Ejemplos específicos de generación de código HCL, depuración de errores en pipelines o generación de scripts de automatización en bash/python.

---

## 🎯 CASO PRÁCTICO EN VIVO

*   **Enunciado para el Candidato:** *"Tienes un deployment en Kubernetes con 3 réplicas. El equipo de desarrollo reporta que los usuarios experimentan lentitud extrema y a veces se reciben errores HTTP 502 (Bad Gateway). No se han realizado despliegues de código en las últimas 4 horas. ¿Cómo inicias tu diagnóstico?"*

*   **Puntos clave a evaluar durante su respuesta:**
    *   **Orden lógico:** ¿Empieza validando alertas globales o salta directo a revisar pods individuales?
    *   **Comandos reales:** ¿Menciona comandos precisos como `kubectl get pods`, `kubectl describe`, `kubectl logs --previous` y revisión del estado de los nodos?
    *   **Visión de red:** ¿Considera evaluar el Ingress Controller y el Service, o solo se limita al contenedor?
    *   **Respuesta Ideal Esperada:**
        1. Comprobar alertas de infraestructura y latencias en el Ingress.
        2. Revisar el estado general de los pods y nodos.
        3. Obtener logs anteriores (`--previous`) del contenedor para buscar reinicios por memoria (OOMKilled).
        4. Validar el pool de conexiones hacia la base de datos o APIs externas antes de asumir que el clúster es la causa.
