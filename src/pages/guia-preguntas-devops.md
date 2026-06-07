---
layout: ../layouts/Layout.astro
title: "GUÍA DE PREGUNTAS: ENTREVISTA TÉCNICA DEVOPS & CLOUD"
---

# 🚀 GUÍA DE PREGUNTAS: ENTREVISTA TÉCNICA DEVOPS & CLOUD
> **Autor:** Academia @jemjaf
> **Objetivo:** Preparación intensiva para entrevistas técnicas de nivel Junior (Jr) y Semi-Senior (SSR).
> **Enfoque:** ¡CONCEPTS > CODE! No memorices comandos. Entiende el *por qué* de la arquitectura, los tradeoffs de cada decisión y los escenarios de producción reales.

---

## 🧠 LA MENTALIDAD DE UN DEVOPS SSR: LO QUE BUSCA EL CLIENTE

El 90% de los candidatos fallan porque responden como "instaladores de herramientas" en lugar de **Ingenieros de Plataforma**. Un cliente técnico te va a evaluar por:

1. **BLAST RADIUS (Radio de Impacto):** ¿Cómo diseñas para que si algo explota, solo afecte a una pequeña parte y no tumbe toda la infraestructura?
2. **SEGURIDAD POR DISEÑO (Zero Trust):** ¿Tus pipelines e infraestructura están protegidos, o metes credenciales hardcodeadas por flojera de configurar OIDC?
3. **COSTOS Y EFICIENCIA:** ¿Levantas recursos sobredimensionados o sabes optimizar costes apagando entornos inactivos y ajustando réplicas?
4. **OPERACIÓN Y TROUBLESHOOTING:** ¿Cómo actúas cuando las métricas de CPU están en verde pero la aplicación está lenta o caída?

---

## 🛠️ BLOQUE 1: CI/CD & AUTOMATIZACIÓN DE DESPLIEGUES

### 📌 Preguntas Clave & Filtros

#### 1. ¿Cuál es la diferencia entre Entrega Continua (Continuous Delivery) y Despliegue Continuo (Continuous Deployment)?
*   **Respuesta Corta:** En *Continuous Delivery*, el artefacto compilado y testeado queda listo para ir a producción, pero el despliegue requiere una **aprobación manual** (intervención humana). En *Continuous Deployment*, cada cambio que pasa los tests se despliega en producción **automáticamente** sin intervención humana.
*   **Diferencial (SSR):** *"Continuous Deployment exige un nivel de madurez extremo en pruebas automatizadas. Si los tests automáticos no son completamente confiables, Continuous Deployment es solo una forma más rápida de romper producción. Por eso, en la mayoría de entornos reales se opta por Continuous Delivery con un flujo de aprobación controlado."*

#### 2. ¿Qué pasos consideras obligatorios en un pipeline de CI/CD antes de llegar a producción?
*   **Junior responde:** Build de la app, tests unitarios y deploy.
*   **SSR responde:**
    1.  **Análisis Estático:** Linting de código y de Dockerfiles (ej. `tflint`, `hadolint`).
    2.  **Seguridad Estática (SAST):** Análisis de código (ej. SonarCloud) y escaneo de vulnerabilidades en dependencias (ej. Trivy) y secretos (ej. Gitleaks).
    3.  **Compilación:** Build de la imagen Docker etiquetada con el hash del commit (`SHA`), evitando siempre usar el tag `latest` en producción.
    4.  **Despliegue a Staging:** Despliegue automatizado de la infraestructura y aplicación usando variables de entorno específicas.
    5.  **Pruebas Dinámicas:** Smoke tests (pruebas de humo) y pruebas de integración sobre el ambiente de Staging.
    6.  **Aprobación Manual:** Gate de control para autorizar el paso a Producción.

---

### 🔄 Equivalencias de Herramientas (Conceptos Universales)

En las entrevistas te dirán: *"Nosotros usamos GitLab CI, pero tú solo tienes experiencia en GitHub Actions. ¿Cómo lo manejas?"*. **Muestra que conoces los patrones conceptuales:**

| Concepto / Recurso | GitHub Actions | GitLab CI | Jenkins | Azure Pipelines |
| :--- | :--- | :--- | :--- | :--- |
| **Definición del Pipeline** | `.github/workflows/*.yaml` | `.gitlab-ci.yml` | `Jenkinsfile` | `azure-pipelines.yml` |
| **Entorno de Ejecución** | Runner | Runner | Agent / Node | Agent |
| **Bloque de Trabajo** | `job` | `stage` | `stage` | `job` / `stage` |
| **Paso Individual** | `step` | `script` | `step` / `sh` | `task` / `script` |
| **Reusabilidad** | Reusable Workflows | `include` / `extends` | Shared Libraries | Templates |
| **Manejo de Estados** | Artifacts / Cache | Artifacts / Cache | Workspace / Archive | Artifacts / Cache |

#### ⚖️ Tradeoffs de Selección:
*   **Jenkins:** Altamente extensible con plugins. **Desventaja:** Requiere un mantenimiento constante del servidor, parches de seguridad y es complejo de administrar como código en comparación con opciones modernas.
*   **GitHub Actions / GitLab CI:** Integración nativa con el repositorio y excelente experiencia de desarrollo. **Desventaja:** Dependencia del proveedor (vendor lock-in) y costos por minutos de ejecución de runners en la nube.
*   **Azure DevOps:** Estructura excelente y alta trazabilidad con tableros corporativos. **Desventaja:** Interfaz densa y ecosistema más enfocado a ambientes Microsoft.

---

### 💡 Caso Real: Automatización y Ahorro de Costos en CI/CD (Entornos AWS/ECS/RDS)

**Escenario planteado en la entrevista:** *"Tenemos clústeres de base de datos y contenedores encendidos 24/7 en ambientes de desarrollo y Staging. El presupuesto se nos está yendo de las manos. ¿Cómo lo solucionarías?"*

**Tu respuesta diferencial (SSR):**
> *"Diseñé e implementé un workflow programado (`schedule` via cron) en GitHub Actions que actúa como un **Infrastructure Scheduler**. 
>
> 1. **Fuera de oficina:** De lunes a viernes a las 10:00 PM, el pipeline apaga el clúster de base de datos (ejecutando un comando CLI que detiene las instancias Aurora RDS) y escala a **0 réplicas** los servicios de contenedores en AWS ECS.
> 2. **Inicio del día:** A las 6:00 AM, otro evento cron vuelve a encender las bases de datos y escala los servicios a su cantidad deseada (`desired-count: 1`).
> 3. **Flexibilidad:** El pipeline cuenta con un disparador manual (`workflow_dispatch`) para que cualquier desarrollador pueda encender o apagar el ambiente de su elección si necesita trabajar fuera de hora.
> 
> Con esta automatización simple redujimos el consumo de cómputo en ambientes no productivos en más del **60%**."*

---

## 🐳 BLOQUE 2: CONTENEDORES Y ORQUESTACIÓN (DOCKER & KUBERNETES)

### 📌 Preguntas Clave & Filtros

#### 1. ¿Cómo optimizas el tamaño y la seguridad de tus imágenes de Docker?
*   **Junior responde:** Uso imágenes Alpine y borro la caché del instalador de paquetes.
*   **SSR responde:**
    *   **Multi-stage Builds:** Separo la etapa de compilación (con SDKs y herramientas pesadas) de la etapa de ejecución (donde solo copio el binario final a una imagen base minimalista como `distroless` o `alpine`).
    *   **Layer Caching:** Copio primero los archivos de dependencias (ej. `package.json` o `requirements.txt`) e instalo las dependencias **antes** de copiar el código fuente. Así, los cambios en el código no invalidan el caché de las dependencias, reduciendo drásticamente el tiempo de build.
    *   **Ejecución como No-Root:** Configuro un usuario sin privilegios en el Dockerfile (`USER appuser`). Si el proceso sufre una brecha, el atacante no tendrá privilegios de root en el nodo host.

#### 2. Un Pod en Kubernetes se encuentra en estado `ImagePullBackOff`. ¿Cómo lo diagnosticas? ¿Y si está en `CrashLoopBackOff`?
*   **Diagnóstico general:** Uso `kubectl describe pod <pod_name>` para ver los eventos del ciclo de vida y `kubectl logs <pod_name>` para ver la salida estándar.
*   **Para `ImagePullBackOff`:**
    *   **Causas:** Nombre de la imagen incorrecto, tag inexistente, o falta de permisos para autenticarse en el Container Registry (falta el secreto `imagePullSecrets` o permisos del nodo).
*   **Para `CrashLoopBackOff`:**
    *   **Causas:** El contenedor arranca pero se cae inmediatamente. Suele ser por fallos en el código (falta una variable de entorno obligatoria, error de conexión a la base de datos o puerto ya en uso).
    *   **Acción:** Reviso logs anteriores del pod usando `kubectl logs <pod_name> --previous`.

---

### 💡 Caso Real: Troubleshooting en Upgrades de Kubernetes con Límites de Cómputo (AKS/Azure)

**Escenario planteado en la entrevista:** *"Debes actualizar un clúster de Kubernetes a una nueva versión, pero la cuenta de cloud está al límite de su cuota de CPU y no puedes simplemente duplicar el clúster. ¿Cómo procedes de forma segura?"*

**Tu respuesta diferencial (SSR):**
> *"Me enfrenté a esta situación actualizando clústeres de AKS (Azure Kubernetes Service) privados. La suscripción de Azure tenía una restricción severa de **cuota de vCPUs** en la región (mexicocentral limitada a 50 vCPUs).
>
> **El problema:** Al actualizar Kubernetes, el proveedor realiza un *Rolling Upgrade*, creando un pool temporal y levantando nuevos nodos antes de eliminar los viejos para no perder disponibilidad. Al estar al límite de vCPUs, la creación de nuevos nodos fallaba por cuota insuficiente (`QuotaExceeded`).
>
> **Cómo lo solucioné:**
> 1. **Deshabilitar el Autoscaler:** Desactivé temporalmente el autoescalador de los pools de nodos.
> 2. **Drenado y Acordonamiento:** Marqué los nodos viejos como no-programables (`kubectl cordon`) y drené las cargas (`kubectl drain <node> --ignore-daemonsets`).
> 3. **Resolución de PDBs (Pod Disruption Budgets) bloqueantes:** En servicios como Elasticsearch, el PDB impedía el drain porque exigía un mínimo de réplicas activas. Eliminé temporalmente los PDBs para permitir desalojar los nodos.
> 4. **Escalar a lo mínimo:** Reduje manualmente el tamaño de los pools de nodos no críticos a 1 nodo usando la API de Azure CLI (`az aks nodepool scale`), liberando la cuota de vCPUs necesaria para que el upgrade pudiera rotar los nodos del pool principal.
> 5. **Restaurar el estado:** Una vez finalizada la actualización, volví a habilitar el autoescalador y los límites de los pools originales."*

---

## 🏗️ BLOQUE 3: INFRASTRUCTURE AS CODE (TERRAFORM / IaC)

### 📌 Preguntas Clave & Filtros

#### 1. ¿Cómo manejas el estado de Terraform (tfstate) en un equipo multi-usuario? ¿Cómo previenes conflictos de escritura?
*   **Respuesta:** El estado se almacena en un **Remote Backend** (como S3 o Azure Blob Storage). Para prevenir conflictos si dos personas ejecutan `apply` al mismo tiempo, se utiliza un mecanismo de bloqueo (*State Locking*).
*   **Diferencial (SSR):** 
    *   *Opción estándar:* Guardar el `.tfstate` en S3 con versionamiento activo y usar una tabla de **DynamoDB** para gestionar el bloqueo de escritura.
    *   *Opción moderna:* Usar la funcionalidad nativa de S3 `use_lockfile = true` (en TF 1.10+) que maneja los bloqueos directamente en el bucket sin requerir DynamoDB.

#### 2. ¿Cuándo utilizas `locals` en lugar de `variables` de entrada en Terraform?
*   **Variables (Inputs):** Parámetros externos que se inyectan al módulo. Sirven para parametrizar la infraestructura según el entorno (ej. `environment = "prod"`).
*   **Locals:** Variables internas y calculadas dentro del propio código. No pueden ser modificadas desde el exterior. Sirven para formatear etiquetas o nombres unificados (ej. `name = "${var.project}-${var.environment}-db-cluster"`).

#### 3. ¿Cuál es el peligro de usar `count` en lugar de `for_each` para crear múltiples recursos a partir de una lista?
*   **El problema de `count`:** Asocia los recursos a un **índice numérico** de la lista (ej. `[0]`, `[1]`). Si eliminas o insertas un elemento en medio de la lista, Terraform reordena los índices y destruirá y recreará recursos que no deberían cambiar.
*   **La solución con `for_each`:** Asocia los recursos a una **clave única**. Si agregas o eliminas un elemento, Terraform solo modificará ese recurso específico.

---

### 💡 Caso Real: Resolución de Drift de Identidades (Principal ID) en Azure AD y Terraform

**Escenario de la entrevista:** *"El pipeline de CI/CD falla al aplicar Terraform alegando que quiere reemplazar (destroy and create) los Role Assignments de seguridad porque detecta diferencias en las identidades, a pesar de que el código no ha cambiado. ¿Qué está pasando?"*

**Tu respuesta diferencial (SSR):**
> *"Este problema se conoce como **Drift de principal_id** y ocurre cuando interactúan ejecuciones locales y pipelines automatizados.
>
> **La causa raíz:** Ocurre cuando se usa `data.azurerm_client_config.current.object_id` para asignar roles. Si yo ejecuto `terraform plan` localmente con mi cuenta personal (`az login`), la identidad activa es mi Object ID. Si luego el pipeline de CI/CD corre con un Service Principal (SP), la identidad activa es la del Service Principal. Terraform detecta que el `principal_id` del rol asignado cambió y propone recrear el acceso.
>
> **La solución:**
> 1. Pasamos los IDs de los Service Principals como variables explícitas en los archivos `.tfvars` de cada ambiente en lugar de usar data sources dinámicos de sesión.
> 2. Si hay una urgencia y el drift bloquea el plan general, corremos un `terraform apply` dirigido únicamente al recurso de asignación del rol afectado (`-target`), esperamos 10 minutos a que se propague el RBAC en Azure, y luego aplicamos el resto de la infraestructura."*

---

## ☁️ BLOQUE 4: CLOUD (AWS vs. AZURE vs. GCP)

### 🗺️ Equivalencias de Servicios Principales

| Categoría | Amazon Web Services (AWS) | Microsoft Azure | Google Cloud (GCP) |
| :--- | :--- | :--- | :--- |
| **Servidor Virtual** | EC2 | Virtual Machine (VM) | Compute Engine |
| **Contenedor Serverless** | ECS Fargate | Azure Container Apps | Cloud Run |
| **Kubernetes Gestionado** | EKS | AKS | GKE |
| **Storage de Objetos** | S3 | Blob Storage | Google Cloud Storage (GCS) |
| **Base de Datos Gestionada** | RDS / Aurora | Azure Database for PostgreSQL | Cloud SQL |
| **Bóveda de Secretos** | Secrets Manager | Key Vault | Secret Manager |
| **Red Virtual** | VPC | VNet | VPC Network |
| **CDN / Caché Edge** | CloudFront | Azure Front Door | Cloud CDN |

---

### 📌 Preguntas Clave & Filtros

#### 1. ¿Cómo gestionas el acceso a la nube desde un pipeline externo de forma segura? ¿Creas una clave de acceso permanente (Access Key)?
*   **Respuesta Correcta:** **NUNCA** se deben crear Access Keys estáticas de IAM para pipelines. Se utiliza **OIDC (OpenID Connect) Federation**.
    *   Configuras al proveedor (ej. GitHub) como un *Identity Provider* confiable dentro de la nube.
    *   El pipeline solicita credenciales temporales que duran minutos y se auto-destruyen, eliminando por completo las claves hardcodeadas.

---

### 💡 Caso Real: Integración Multi-Cloud Segura con Workload Identity Federation (WIF)

**Escenario de la entrevista:** *"Tenemos una aplicación corriendo en AWS que debe extraer datos y exportarlos directamente a un bucket de almacenamiento en Google Cloud Storage (GCP). ¿Cómo diseñas esta integración de manera segura?"*

**Tu respuesta diferencial (SSR):**
> *"Para este caso, implementé una arquitectura multi-cloud basada en **Workload Identity Federation (WIF)**, eliminando por completo el uso de claves JSON de cuentas de servicio de GCP (`sa.json`).
>
> **Cómo funciona el flujo:**
> 1. La Lambda de exportación corre con un rol IAM específico de AWS.
> 2. En GCP configuré un *Workload Identity Pool* que confía en el ID de la cuenta de AWS y en el ARN del rol de la Lambda.
> 3. Al arrancar, la Lambda intercambia un token firmado de AWS por un token temporal de GCP (`sts:AssumeRoleWithWebIdentity`).
> 4. El código de la Lambda asume (impersonates) una Service Account de GCP con permisos estrictamente acotados al bucket de Google Cloud Storage. 0 claves estáticas almacenadas."*

---

## 📈 BLOQUE 5: MONITOREO, OBSERVABILIDAD Y LINUX TROUBLESHOOTING

### 📌 Preguntas Clave & Filtros

#### 1. ¿Cuál es la diferencia entre Monitoreo y Observabilidad?
*   **Monitoreo:** Te dice **cuándo** un sistema está fallando. Se basa en reglas predefinidas y alertas (ej. *"Alerta si la CPU supera el 85%"*).
*   **Observabilidad:** Te permite entender **por qué** está fallando un sistema a partir de sus outputs (Métricas, Logs y Trazas). Te ayuda a diagnosticar comportamientos inesperados sin necesidad de modificar el código.

#### 2. Tus usuarios se quejan de que la web va lenta, pero tu dashboard de Prometheus muestra la CPU y la RAM de las instancias al 30%. ¿Cómo investigas?
*   **Tu respuesta diferencial (SSR):** *"El uso de CPU y RAM no mide el rendimiento de la aplicación. Para diagnosticar esto, utilizo el estándar de Golden Signals:*
    *   **Rate:** Número de peticiones por segundo. ¿Hay un pico de tráfico?
    *   **Errors:** Tasa de fallos HTTP.
    *   **Duration:** Tiempo de respuesta del servidor (latencia).
    *   *Puntos de cuello de botella habituales:*
        1.  **Límites de conexión en la Base de Datos:** Las instancias pueden estar bloqueadas esperando una conexión libre en el pool de la base de datos.
        2.  **Límites de red o I/O de disco:** Las instancias esperan respuestas de APIs de terceros o sufren latencia de lectura/escritura en disco.
        3.  **Límites de Conexión en el Ingress/Reverse Proxy:** Cuellos de botella en Nginx que encolan peticiones."*

---

## 🤝 BLOQUE 6: PREGUNTAS DE RECURSOS HUMANOS Y FIT CULTURAL

En las entrevistas no todo es técnico. Los reclutadores y gerentes de ingeniería quieren validar cómo trabajas en equipo, tu nivel de comunicación y tu proyección.

### 📌 Preguntas que te harán a ti:

#### 1. ¿Cómo manejas una situación en la que un desarrollador insiste en que su código funciona pero en el entorno de Staging/QA está fallando?
*   **Enfoque correcto (SSR):** *"Evito la confrontación y me enfoco en los datos. No digo 'tu código no sirve'. En su lugar, abro los logs del contenedor o del Ingress y le muestro el comportamiento objetivo (por ejemplo, un error 500 o una variable de entorno faltante). Le ofrezco revisar juntos el archivo de configuración en Staging. El objetivo de DevOps no es poner barreras a desarrollo, sino ayudarlos a que desplieguen de forma autónoma y segura."*

#### 2. Describe una situación en la que tuviste que trabajar bajo presión durante un incidente en producción. ¿Cómo lo manejaste?
*   **Enfoque correcto (SSR):** *"Lo primero es la comunicación y el control del Blast Radius. Ante un incidente, sigo tres pasos: 1. Contener el daño (por ejemplo, hacer rollback al último commit estable o desviar tráfico), 2. Resolver la causa raíz, y 3. Documentar un postmortem. Durante la crisis, mantengo informados a los líderes mediante actualizaciones cortas cada 15 minutos, evitando que el pánico se propague en el equipo."*

---

### 📌 Preguntas que DEBES hacer tú al final de la entrevista (Ownership):

Hacer preguntas inteligentes demuestra interés real, iniciativa técnica y profesionalismo. **Lanza estas preguntas al panel:**

#### 1. *"¿Cómo medirán ustedes si mi contratación fue un éxito a los 3 y 6 meses? ¿Cuáles son los objetivos clave que esperan que cumpla en ese periodo?"*
*   **Por qué funciona:** Muestra que estás orientado a resultados y que te importa cumplir con las expectativas del negocio desde el primer día. Obliga al manager a definir el éxito para ti.

#### 2. *"¿Cómo está estructurado el equipo? ¿Me uniré a un equipo de varios ingenieros DevOps/Plataforma, seré el único DevOps asignado al proyecto, o trabajaré de forma independiente dando soporte a diferentes squads?"*
*   **Por qué funciona:** Te da claridad sobre tu nivel de autonomía, si tendrás mentores o compañeros con quienes discutir soluciones arquitectónicas, o si se espera que seas el único responsable de la infraestructura del cliente.

#### 3. *"¿Tienen un modelo de guardias u on-call actualmente establecido para este rol? Si es así, ¿cómo está estructurada la rotación y la criticidad de las alertas fuera de la jornada laboral?"*
*   **Por qué funciona:** Demuestra madurez y experiencia operativa real. Un DevOps experimentado sabe que los incidentes ocurren fuera de horario y quiere conocer las reglas del juego de antemano.

#### 4. *"¿Cuál es el dolor técnico o el cuello de botella más grande que tienen hoy en día los desarrolladores con el pipeline de despliegue o la infraestructura?"*
*   **Por qué funciona:** Te posiciona inmediatamente como un solucionador de problemas. Quieres saber dónde duele el proceso para aportar valor desde la primera semana.

---

## 🎯 CONSEJOS CLAVE PARA EL DÍA DE TU ENTREVISTA

1.  **Usa el método S.T.A.R. en las preguntas de comportamiento:**
    *   **S (Situación):** *"En mi anterior proyecto, teníamos un problema con..."*
    *   **T (Tarea):** *"Mi rol consistía en rediseñar el pipeline y garantizar..."*
    *   **A (Acción):** *"Lo que hice fue implementar Workload Identity y..."*
    *   **R (Resultado):** *"Gracias a esto, redujimos el tiempo de build en un 60%."*
2.  **Honestidad Técnica:** Si te preguntan sobre algo que no conoces, **no inventes**. Di la verdad usando este patrón:
    *   *"No he implementado X en producción todavía, pero entiendo su concepto básico, que es solucionar Y. En mis proyectos he solucionado ese mismo problema utilizando la herramienta Z, donde el tradeoff fue..."*
