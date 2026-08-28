<div align="center">
<img src="./assets/header_esp.png" alt="GitHub Copilot - Programa de Adopción" width="100%" />

# 🚀 Workshop 1 — GitHub Copilot CLI: Setup y Modo Interactivo

**Hands-on de instalación, autenticación, Trust Model, contexto y exploración de codebase**

**⏱️ Duración total: 90 minutos**

</div>

---

Este workshop práctico lleva al participante desde la instalación de **GitHub Copilot CLI** hasta una primera sesión de trabajo real sobre el repositorio del workshop. El foco está en ejecutar, validar y experimentar con el agente desde la terminal; la teoría se limita a lo estrictamente necesario para completar los laboratorios.

> [!TIP]
> Trabajá siempre dentro del directorio específico del proyecto. El Trust Model habilita al agente a operar sobre el contenido del directorio desde el que fue lanzado.

---

## 📋 Tabla de Contenidos

1. [🎯 Objetivos de aprendizaje](#-objetivos-de-aprendizaje)
2. [⏱️ Duración estimada](#️-duración-estimada)
3. [📚 Requisitos previos](#-requisitos-previos)
4. [🧰 Paso 1. Instalar y verificar GitHub Copilot CLI](#-paso-1-instalar-y-verificar-github-copilot-cli)
5. [🔐 Paso 2. Autenticarse, clonar el repo y validar el Trust Model](#-paso-2-autenticarse-clonar-el-repo-y-validar-el-trust-model)
6. [🩺 Paso 3. Validar el estado inicial del CLI](#-paso-3-validar-el-estado-inicial-del-cli)
7. [🔎 Paso 4. Explorar el codebase en Modo Normal](#-paso-4-explorar-el-codebase-en-modo-normal)
8. [📎 Paso 5. Adjuntar contexto y analizar un archivo](#-paso-5-adjuntar-contexto-y-analizar-un-archivo)
9. [🧭 Paso 6. Usar Modo Plan sin ejecutar cambios](#-paso-6-usar-modo-plan-sin-ejecutar-cambios)
10. [📝 Paso 7. Generar documentación y compartir la sesión](#-paso-7-generar-documentación-y-compartir-la-sesión)
11. [✅ Checklist de finalización](#-checklist-de-finalización)
12. [🧭 Reflexiones finales](#-reflexiones-finales)

---

## 🎯 Objetivos de aprendizaje

Al finalizar este taller serás capaz de:

- ✅ Instalar y verificar **GitHub Copilot CLI** desde la terminal.
- ✅ Autenticarte mediante `/login` y reconocer el **Trust Model** del directorio de trabajo.
- ✅ Clonar y abrir correctamente el repositorio del workshop antes de iniciar el agente.
- ✅ Consultar `/changelog`, `/version` y `/model` para validar el estado de la sesión.
- ✅ Usar **Modo Normal** para explorar la arquitectura de un codebase.
- ✅ Adjuntar archivos con `@...` para entregar contexto explícito al agente.
- ✅ Cambiar a **Modo Plan** con `Shift+Tab`, revisar un plan y cancelarlo con `Ctrl+C` antes de modificar código.
- ✅ Generar documentación del proyecto y compartir una sesión con `/share`.

---

## ⏱️ Duración estimada

> [!NOTE]
> La distribución siguiente adapta el material original a un workshop **hands-on de 90 minutos**. Los tiempos están orientados a ejecución y validación, no a exposición teórica.

| Bloque | Tiempo |
| --- | ---: |
| 🧰 Instalación y verificación | 20 min |
| 🔐 Autenticación, clone y Trust Model | 20 min |
| 🩺 Estado inicial del CLI | 10 min |
| 🔎 Exploración del codebase en Modo Normal | 15 min |
| 📎 Contexto explícito con `@archivo` | 10 min |
| 🧭 Modo Plan y cancelación controlada | 10 min |
| 📝 README + `/share` + cierre | 5 min |
| **Total** | **90 min** |

---

## 📚 Requisitos previos

Antes de comenzar, asegurate de tener:

- Una terminal disponible en **Windows, macOS o Linux**.
- **Git** instalado.
- Acceso a una cuenta de GitHub con GitHub Copilot habilitado.
- La URL del repositorio de práctica entregada por el instructor.
- Permisos para clonar el repositorio.
- Si elegís instalar vía npm: **Node.js / npm** disponibles.

Definí la URL del repositorio antes de comenzar:

```text
WORKSHOP_REPO_URL=<URL del repo del workshop>
```

> [!IMPORTANT]
> El material fuente no contiene la URL definitiva del repositorio; utiliza el placeholder `[URL del repo]`. Reemplazalo por la URL que entregue el instructor.

---

## 🧰 Paso 1. Instalar y verificar GitHub Copilot CLI

**Objetivo:** dejar el binario `copilot` disponible en la terminal y confirmar que responde correctamente.

Elegí **un solo método** de instalación.

### 1.1 Windows — WinGet

```powershell
winget install GitHub.CopilotCLI
```

### 1.2 macOS — Homebrew

```bash
brew install github/tap/copilot
```

### 1.3 macOS / Linux — script de instalación

```bash
curl -fsSL https://aka.ms/install-copilot-cli.sh | bash
```

### 1.4 Cross-platform — npm

```bash
npm install -g @github/copilot
```

### 1.5 Verificar la instalación

Cerrá y abrí nuevamente la terminal si fuese necesario y ejecutá:

```bash
copilot --version
```

### Resultado esperado

La terminal debe reconocer el comando `copilot` y devolver la versión instalada.

> [!NOTE]
> El material del workshop indica que Homebrew, WinGet y el script de instalación incluyen mecanismo de actualización, mientras que una instalación mediante npm requiere actualizar el paquete manualmente cuando corresponda.

### Checkpoint

- [ ] `copilot --version` responde sin error.
- [ ] El comando es reconocido desde una terminal nueva.

---

## 🔐 Paso 2. Autenticarse, clonar el repo y validar el Trust Model

**Objetivo:** autenticar Copilot CLI y ejecutar el agente únicamente desde el repositorio que se utilizará durante el workshop.

### 2.1 Autenticarse con OAuth

Ejecutá:

```bash
copilot /login
```

Seguí el flujo de autenticación mostrado en pantalla y completá la autorización en GitHub.

> [!NOTE]
> El material también contempla `COPILOT_GITHUB_TOKEN` para escenarios programáticos/CI/CD. Para este workshop interactivo se prioriza `/login`.

### 2.2 Clonar el repositorio

```bash
git clone <URL_DEL_REPO>
```

Ingresá al directorio recién clonado:

```bash
cd <DIRECTORIO_DEL_REPO>
```

Validá dónde estás parado:

```bash
pwd
```

En PowerShell también podés utilizar:

```powershell
Get-Location
```

### 2.3 Lanzar Copilot desde el directorio correcto

```bash
copilot
```

Cuando aparezca el **Trust Prompt**, revisá el directorio que Copilot solicita utilizar y aceptalo únicamente si corresponde al repositorio de práctica.

> [!WARNING]
> No lances `copilot` desde tu home (`~`) o desde un directorio demasiado amplio. El material destaca que allí pueden existir `.ssh`, `.aws`, `.env` y otros archivos que no deberían quedar dentro del alcance del agente.

### Resultado esperado

Copilot CLI inicia dentro del repositorio y el Trust Prompt corresponde al directorio de práctica.

### Checkpoint

- [ ] Autenticación completada.
- [ ] Repositorio clonado.
- [ ] La sesión se ejecuta desde el directorio del proyecto.
- [ ] El Trust Prompt fue revisado antes de continuar.

---

## 🩺 Paso 3. Validar el estado inicial del CLI

**Objetivo:** comprobar rápidamente versión, modelo y novedades antes de trabajar sobre el codebase.

Dentro de Copilot CLI ejecutá:

```text
/changelog
```

Luego:

```text
/version
```

Y finalmente:

```text
/model
```

Si el entorno ofrece el modo automático, podés seleccionar:

```text
/model auto
```

### Resultado esperado

Debés poder identificar:

- La versión activa del CLI.
- El modelo seleccionado para la sesión.
- Las novedades recientes expuestas por `/changelog`.

> [!TIP]
> El objetivo de este paso no es comparar modelos. Solo validar que la sesión está operativa antes de comenzar a modificar o analizar el repositorio.

---

## 🔎 Paso 4. Explorar el codebase en Modo Normal

**Objetivo:** usar el agente como un nuevo integrante del equipo que primero necesita comprender la arquitectura del repositorio.

### 4.1 Confirmar Modo Normal

El material utiliza tres modos de operación y permite alternarlos con `Shift+Tab`:

```text
Normal → Plan → Autopilot → Normal
```

Para esta actividad mantenete en **Modo Normal**.

### 4.2 Pedir una explicación de la arquitectura

Enviá un prompt equivalente a:

```text
Analiza este repositorio y explícame su arquitectura, los módulos principales, cómo se ejecuta la aplicación y cómo se ejecutan los tests.
```

No busques una respuesta teórica genérica: verificá que Copilot realmente inspeccione el repositorio.

### 4.3 Opcional: inicializar el contexto del repositorio

La transcripción muestra el uso de `/init` como primer "handshake" del agente con el codebase. Si el comando está disponible en tu versión/configuración, ejecutalo y revisá qué información descubre o qué instrucciones existentes detecta.

### Resultado esperado

El agente debe producir un overview relacionado con el contenido real del repositorio: estructura, módulos, comandos y convenciones detectadas.

### Checkpoint

- [ ] La respuesta menciona archivos o directorios reales del repo.
- [ ] Identificaste dónde está el código principal.
- [ ] Identificaste cómo ejecutar la aplicación o los tests, si el repositorio lo define.

---

## 📎 Paso 5. Adjuntar contexto y analizar un archivo

**Objetivo:** comprobar la diferencia entre una pregunta general y una consulta con un archivo explícitamente adjuntado al contexto.

### 5.1 Adjuntar un archivo

El ejemplo del material utiliza:

```text
@src/api/users.ts ¿hay algún bug en este código?
```

Si esa ruta no existe en tu copia del repositorio, utilizá el archivo equivalente dentro de `src/` que indique el instructor.

### 5.2 Explorar otras formas de contexto

El material también muestra estas posibilidades:

```text
@src/api/auth.ts @src/api/users.ts ¿inconsistencias entre estos módulos?
```

Y para ejecutar un comando shell directamente desde la sesión:

```text
!git log --oneline -10
```

### Resultado esperado

Copilot debe analizar el contenido concreto del archivo adjuntado y señalar hallazgos vinculados con ese código, no responder de forma genérica.

> [!TIP]
> Usá `@archivo` cuando el contexto explícito aporte precisión. Evitá agregar archivos innecesarios solo por costumbre.

---

## 🧭 Paso 6. Usar Modo Plan sin ejecutar cambios

**Objetivo:** practicar una planificación completa antes de permitir que el agente modifique el repositorio.

### 6.1 Cambiar a Modo Plan

Presioná:

```text
Shift+Tab
```

hasta quedar en **Plan**.

### 6.2 Solicitar una mejora

Utilizá un prompt como:

```text
Analiza uno de los endpoints de este proyecto y crea un plan para agregar manejo de errores. No ejecutes cambios todavía; primero quiero revisar el alcance y los archivos que serían modificados.
```

### 6.3 Revisar el plan

Antes de ejecutar nada, verificá:

- Qué archivos propone modificar.
- Qué comportamiento intenta cambiar.
- Qué tests propone agregar o actualizar.
- Si el alcance coincide con lo solicitado.

### 6.4 Cancelar la ejecución

Para este laboratorio **no implementes el plan**. Interrumpí la operación con:

```text
Ctrl+C
```

### Resultado esperado

Debés poder distinguir claramente:

- **Normal:** el agente propone acciones durante la ejecución y solicita aprobación.
- **Plan:** el agente diseña primero el roadmap de trabajo para que puedas revisar el scope antes de implementar.

> [!IMPORTANT]
> En este workshop el objetivo es aprender a inspeccionar el plan. No necesitamos introducir cambios funcionales en esta etapa.

---

## 📝 Paso 7. Generar documentación y compartir la sesión

**Objetivo:** utilizar el conocimiento acumulado por la sesión para documentar el repositorio y luego exportar/compartir el contexto de trabajo.

### 7.1 Generar o mejorar `README.md`

Volvé a Modo Normal si fuese necesario y pedí:

```text
Genera o actualiza el README.md de este proyecto usando lo que aprendiste del repositorio. Incluye overview, arquitectura, requisitos, comandos para ejecutar la aplicación y comandos de test. No inventes información que no esté respaldada por el codebase.
```

Revisá la propuesta antes de aceptar cambios.

### 7.2 Compartir la sesión

Ejecutá:

```text
/share
```

Seleccioná la opción permitida por tu entorno y copiá la referencia generada.

> [!NOTE]
> La disponibilidad de publicación mediante Gist u otros mecanismos puede depender de las políticas y permisos de la organización. El objetivo del laboratorio es conocer el flujo de exportación/compartición de la sesión.

### Resultado esperado

Al finalizar deberías contar con:

- Una propuesta de README basada en el repositorio real.
- Una sesión exportada o una referencia generada por `/share`, si la política del entorno lo permite.

---

## ✅ Checklist de finalización

- [ ] GitHub Copilot CLI instalado y verificado.
- [ ] Autenticación completada.
- [ ] Repositorio clonado y abierto desde el directorio correcto.
- [ ] Trust Prompt entendido y validado.
- [ ] `/changelog`, `/version` y `/model` ejecutados.
- [ ] Arquitectura del repositorio analizada en Modo Normal.
- [ ] Al menos un archivo adjuntado con `@...` y analizado.
- [ ] Un plan de cambio generado y cancelado antes de implementar.
- [ ] README generado o actualizado a partir del codebase.
- [ ] `/share` probado cuando la política del entorno lo permita.

---

## 🧭 Reflexiones finales

- El valor del CLI no está solamente en responder preguntas: el agente puede **leer, razonar y operar sobre el repositorio** desde la terminal.
- El **directorio de trabajo** define el alcance práctico del agente; por eso el Trust Model es una decisión operativa y de seguridad.
- **Modo Normal** es apropiado para aprender y revisar cada acción; **Modo Plan** permite validar alcance antes de ejecutar.
- Adjuntar contexto con `@archivo` mejora la precisión cuando el problema está localizado.
- Una sesión bien construida puede reutilizar su contexto para documentación y colaboración.

> [!IMPORTANT]
> El criterio principal del workshop es mantener control humano: revisar contexto, plan, archivos y cambios antes de aprobar acciones.

---