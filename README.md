# Front Red BRC 🚀

<p align="center">
  <a href="https://react.dev/" target="blank"><img src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" width="120" alt="React Logo" /></a>
</p>

Una interfaz de usuario moderna, rápida y reactiva para el ecosistema **Red BRC**, construida con **React**, **TypeScript** y potenciarizada por **Vite**. Este repositorio contiene el frontend del proyecto diseñado para ofrecer una experiencia de usuario excepcional y de alto rendimiento.

---

## 🛠️ Stack Tecnológico y Versiones

El frontend está configurado con las tecnologías web más modernas y herramientas óptimas para asegurar el tipado fuerte, la calidad del código y un flujo de trabajo ágil:

| Componente / Herramienta | Tecnología | Versión | Descripción |
| :--- | :--- | :--- | :--- |
| **Framework Principal** | [React](https://react.dev/) | `^19.2.6` | Biblioteca declarativa y eficiente para construir interfaces de usuario. |
| **Plataforma de Ejecución** | [Node.js](https://nodejs.org/) | `>= 22.0.0` | Entorno de ejecución para el desarrollo local (Recomendado v22). |
| **Herramienta de Compilación / Bundler** | [Vite](https://vite.dev/) | `^8.0.12` | Entorno de desarrollo ultrarrápido y empaquetador moderno. |
| **Lenguaje de Programación** | [TypeScript](https://www.typescriptlang.org/) | `~6.0.2` | Superset de JavaScript que añade tipado estático al código. |
| **Linter de Código** | [ESLint](https://eslint.org/) | `^10.3.0` | Herramienta para identificar y reportar patrones en el código JavaScript/TypeScript. |
| **Estilado** | CSS | Vanilla CSS | Diseño responsivo y adaptable usando variables CSS y animaciones nativas. |

---

## ⚙️ Requisitos Previos

Antes de comenzar, asegúrate de tener instalado en tu máquina local:
- **Node.js** (versión recomendada `v22.x` o superior)
- **npm** (gestor de paquetes de Node.js)

---

## 🚀 Instalación y Configuración

Sigue estos pasos para clonar el repositorio e instalar las dependencias del proyecto de forma local:

```bash
# 1. Clonar el repositorio (si aún no lo has hecho)
$ git clone <url-del-repositorio>
$ cd front_red_brc

# 2. Instalar dependencias del proyecto
$ npm install
```

---

## 💻 Desarrollo y Ejecución

Puedes levantar el servidor de desarrollo local o realizar pruebas estáticas utilizando los siguientes comandos:

```bash
# Iniciar servidor de desarrollo (con Hot Module Replacement - HMR)
$ npm run dev

# Compilar la aplicación para producción (TypeScript + Vite build)
$ npm run build

# Ejecutar el linter para comprobar errores estáticos de formato y código
$ npm run lint

# Previsualizar localmente la compilación de producción generada en /dist
$ npm run preview
```

> [!NOTE]
> Por defecto, el servidor de desarrollo de Vite se iniciará en `http://localhost:5173`. Puedes abrir esta dirección en tu navegador para ver la aplicación ejecutándose en tiempo real.

---

## 🔄 Flujo de Integración Continua (Workflows)

El repositorio incluye un workflow de integración continua automatizado utilizando **GitHub Actions** para asegurar que no se introduzcan regresiones al código base.

### Configuración del Workflow (`.github/workflows/blank.yml`)

Este flujo de trabajo se activa de forma automática ante cada evento de **Push** o **Pull Request** hacia la rama principal `main` (o manualmente desde la pestaña de *Actions* mediante `workflow_dispatch`).

```yaml
name: CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout del código
        uses: actions/checkout@v4

      - name: Configurar Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '22'

      - name: Instalar dependencias
        run: npm install

      - name: Ejecutar pruebas
        run: npm test

      - name: Construir proyecto
        run: npm run build
```

### 📋 Pasos del Workflow CI:
1. **Checkout del código**: Clona el código fuente en la máquina virtual.
2. **Configuración de Node.js**: Instala **Node.js v22** preparando el entorno virtual.
3. **Instalación de dependencias**: Instala los paquetes requeridos de manera limpia.
4. **Ejecutar pruebas**: Ejecuta los scripts de prueba para validar que el sistema funciona sin problemas (nota: asegúrate de tener configurado tu script de testing si vas a añadir pruebas automatizadas en `package.json`).
5. **Construcción del proyecto**: Ejecuta `npm run build` para garantizar que el compilador de TypeScript y Vite generen el build de producción de forma exitosa sin fallos de compilación.

---

## 📦 Despliegue en Producción (Deployment)

Dado que este proyecto está empaquetado con Vite, compilarlo genera activos estáticos puros (HTML, JS, CSS, imágenes) que pueden ser alojados de manera extremadamente eficiente en cualquier servidor web o plataforma CDN.

### 1. Compilar el proyecto
Para generar el build de producción optimizado, ejecuta:
```bash
$ npm run build
```
Esto creará una carpeta llamada `/dist` en la raíz del proyecto conteniendo todos los archivos estáticos minimizados y listos.

### 2. Opciones de Hosting Recomendadas
Puedes desplegar la carpeta `/dist` en una gran cantidad de servicios modernos de manera gratuita o de bajo costo:
- **Vercel** / **Netlify** / **Cloudflare Pages**: Conexión directa al repositorio Git con despliegue automático tras cada Push a `main`.
- **GitHub Pages**: Despliegue automatizado mediante GitHub Actions configurado en tu repositorio.
- **Servidor Web Propio (Nginx / Apache)**: Copiar los contenidos del directorio `/dist` directamente a la carpeta raíz de tu servidor web (e.g. `/var/www/html`).

---

## 📄 Licencia

Este proyecto está bajo la licencia **MIT** (o la licencia especificada en `package.json`).
