# 🌱 Proyecto Integrador: Plataforma Comunitaria "EcoColecta"

Aplicación web desarrollada de forma colaborativa para el municipio local, diseñada para gestionar puntos de reciclaje comunitario y registrar las entregas de materiales reciclables de los ciudadanos.

---

## 📋 Fase 1: Investigación Inicial e Identidad

### 1. Evolución del Control de Versiones: Centralizado vs. Distribuido
* **Sistemas Centralizados (ej. SVN - Subversion):** 
  * Funcionan bajo un modelo cliente-servidor tradicional. Existe un único servidor central que almacena toda la base de datos con el historial completo del proyecto. 
  * Las computadoras de los desarrolladores solo guardan una "foto" local de los archivos actuales para trabajar. 
  * *Desventaja crítica:* Si el servidor central sufre una caída o se pierde la conexión de red, es imposible realizar *commits*, ver historiales o trabajar localmente.
* **Sistemas Distribuidos (ej. Git):** 
  * Cada desarrollador que clona el repositorio posee una copia local exacta e íntegra de toda la base de datos y del historial completo del proyecto desde su origen. 
  * Permite realizar *commits*, crear ramas, fusionar y consultar historiales 100% offline sin depender de internet o de un servidor central.

### 2. Diferencias Conceptuales: Git vs. GitHub
* **Git:** Es el motor o software de control de versiones de código abierto que se ejecuta localmente en la computadora del desarrollador a través de la terminal o herramientas de software. Registra cada cambio mediante puntos de restauración llamados *commits*.
* **GitHub:** Es una plataforma web de alojamiento en la nube (basada en Git) que centraliza el trabajo colaborativo, añadiendo herramientas empresariales como tableros Kanban (*GitHub Projects*), gestión de incidencias (*Issues*), solicitudes de fusión (*Pull Requests*) y automatización de despliegues (*GitHub Actions*).

---

## 🏗️ Fase 2: Configuración del Repositorio y Arquitectura

### Estructura Base del Proyecto
El proyecto utiliza una arquitectura web limpia y modular:
* `index.html`: Interfaz de usuario principal y estructura de vistas.
* `styles.css`: Hojas de estilo y diseño responsivo de la plataforma.
* `app.js`: Lógica del cliente, manipulación del DOM y registro de datos.
* `.gitignore`: Archivos y dependencias excluidos del control de versiones (entornos locales, cachés del sistema operativo y credenciales).

### Análisis de Arquitectura: Cliente-Servidor vs. Modelo Distribuido de Git
* **Arquitectura Cliente-Servidor (Aplicación Web):** La interfaz cliente consume recursos y envía peticiones HTTP/S a un servidor backend centralizado que procesa las reglas de negocio y almacena la información en bases de datos relacionales (como MySQL).
* **Paralelismo con Git:** Mientras que el servidor web central atiende las peticiones de los ciudadanos en tiempo de ejecución, el motor distribuido de Git garantiza que la ingeniería del software se desarrolle de forma descentralizada y segura, evitando puntos únicos de fallo durante el trabajo en equipo.

---

## 🔄 Fase 4: Estrategia de Branching (Git Flow) y Resolución de Conflictos

* **Normativa de ramas:** Está prohibido realizar commits directos sobre la rama principal `main`. Todo el desarrollo se ejecuta mediante ramas de funcionalidad utilizando el convenio `feature/nombre-funcionalidad` (ej. `feature/pantalla-inicio`).
* **Metodología de integración:** 
  * Se empleó `git merge` para la integración conservadora de ramas mediante commits de fusión, manteniendo la trazabilidad histórica del equipo.
* **Simulación y Resolución de Conflictos:**
  * Se provocó deliberadamente un conflicto de convergencia al modificar de manera simultánea la misma línea del archivo `README.md` tanto en el repositorio remoto como en el entorno local.
  * *Resolución:* Se aplicó un *pull* para detectar el bloqueo, se inspeccionaron las marcas de conflicto (`<<<<<<<` / `======={` / `>>>>>>>`), se editaron manualmente los bloques de código en Visual Studio Code para conservar la integridad lógica, y se consolidó el cambio mediante un nuevo *commit* de resolución y `git push`.

---

## 🚀 Fase 6: Automatización e Integración Continua (CI/CD)

El repositorio cuenta con un pipeline automatizado mediante **GitHub Actions** ubicado en `.github/workflows/main.yml`. 
* **Disparadores (*Triggers*):** Se ejecuta automáticamente en cada `push` o `pull_request` dirigido a la rama `main`.
* **Verificaciones automatizadas (*Jobs*):**
  1. Clona el código en una máquina virtual limpia con Ubuntu (`ubuntu-latest`).
  2. Valida la existencia estricta de los archivos críticos del proyecto (`index.html`, `styles.css`, `app.js`, `README.md`).
  3. Ejecuta un análisis estático de sintaxis sobre los scripts de JavaScript (`node --check app.js`) para garantizar que ningún error de sintaxis llegue a producción.
