# Guía de Flujo de Trabajo con Ramas (Git Branching Workflow) 🌿

Este documento establece la estrategia y las mejores prácticas para el uso de ramas de Git en el desarrollo del ecosistema **Red BRC**. Seguir este flujo garantiza un historial limpio, despliegues seguros y una colaboración fluida dentro del equipo.

---

## 📌 Ramas Principales (Long-lived Branches)

El proyecto cuenta con dos ramas principales permanentes:

### 1. `main`
* **Propósito**: Código estable y listo para producción.
* **Despliegue**: Cualquier cambio fusionado en esta rama es compilado y desplegado de forma automática a los servidores de producción.
* **Regla**: **NUNCA** se realizan commits directos a esta rama. Toda adición pasa por una Pull Request (PR) revisada y aprobada.

### 2. `develop` (o `dev`)
* **Propósito**: Rama de integración para desarrollo. Aquí converge el trabajo diario de todas las nuevas características antes de pasar a producción.
* **Despliegue**: Generalmente conectada a un entorno de pruebas/staging.
* **Regla**: Es la base de donde se crean casi todas las ramas de soporte.

---

## 🛠️ Ramas de Soporte (Short-lived Branches)

Estas ramas tienen un ciclo de vida corto y se eliminan una vez que se fusionan con la rama base correspondiente.

### 1. Ramas de Características (`feature/*`)
Para el desarrollo de nuevas funcionalidades o componentes.
* **Creada desde**: `develop`
* **Fusiona hacia**: `develop`
* **Nomenclatura**: `feature/<identificador-breve>`
  * *Ejemplo*: `feature/login-form`, `feature/user-profile-page`

### 2. Ramas de Corrección (`bugfix/*`)
Para corregir errores o bugs descubiertos en la rama de integración.
* **Creada desde**: `develop`
* **Fusiona hacia**: `develop`
* **Nomenclatura**: `bugfix/<error-corregido>`
  * *Ejemplo*: `bugfix/fix-navbar-spacing`, `bugfix/api-headers-error`

### 3. Ramas de Parche de Emergencia (`hotfix/*`)
Para solucionar problemas críticos que ocurren directamente en **producción** (`main`) y requieren una solución inmediata.
* **Creada desde**: `main`
* **Fusiona hacia**: `main` y `develop` (para no perder el parche en futuros desarrollos)
* **Nomenclatura**: `hotfix/<parche-critico>`
  * *Ejemplo*: `hotfix/auth-token-vulnerability`, `hotfix/payment-gateway-crash`

### 4. Ramas de Lanzamiento (`release/*`)
Para preparar una versión específica de producción (limpieza de detalles de última hora, metas, documentación de versión).
* **Creada desde**: `develop`
* **Fusiona hacia**: `main` y `develop`
* **Nomenclatura**: `release/v<numero-version>`
  * *Ejemplo*: `release/v1.0.0`

---

## 🔄 El Proceso Paso a Paso (Workflow Diario)

Para añadir cualquier cambio al repositorio, sigue este flujo estándar:

### Paso 1: Asegurar la rama base actualizada
Antes de crear tu rama de trabajo, colócate en la rama base (usualmente `develop`) y obtén los últimos cambios del servidor:
```bash
$ git checkout develop
$ git pull origin develop
```

### Paso 2: Crear la rama con el formato correcto
Crea y accede a tu nueva rama de soporte utilizando la nomenclatura adecuada:
```bash
$ git checkout -b feature/mi-nueva-caracteristica
```

### Paso 3: Realizar commits organizados y semánticos
Realiza cambios incrementales y añade commits claros utilizando **Commits Semánticos** (ver sección abajo):
```bash
$ git add .
$ git commit -m "feat: implementar componente de botones interactivos"
```

### Paso 4: Subir la rama al servidor remoto
Sube tu rama para que esté disponible en GitHub / GitLab:
```bash
$ git push origin feature/mi-nueva-caracteristica
```

### Paso 5: Abrir un Pull Request (PR)
1. Ve a la plataforma de repositorios (GitHub).
2. Crea un Pull Request comparando tu rama (`feature/mi-nueva-caracteristica`) con la rama base correcta (`develop`).
3. Describe detalladamente qué cambios has hecho y cómo probarlos.
4. Solicita la revisión de al menos un compañero de equipo.
5. Asegúrate de que el flujo de Integración Continua (CI) pase con éxito.

### Paso 6: Fusión y Limpieza
Una vez aprobado el PR y pasada la suite de pruebas del pipeline:
1. Fusiona la Pull Request en la plataforma web.
2. Elimina la rama remota en el navegador.
3. Limpia tu entorno local para mantener el orden:
   ```bash
   $ git checkout develop
   $ git pull origin develop
   $ git branch -d feature/mi-nueva-caracteristica
   ```

---

## 📝 Convención de Mensajes de Commit (Semantic Commits)

Mantener un estándar de commits facilita la generación de registros de cambios (Changelogs) automatizados y la legibilidad del historial.

Formato: `<tipo>: <descripción en imperativo y minúsculas>`

### Tipos de Commits más comunes:
* **`feat`**: Una nueva funcionalidad para el usuario final (e.g. `feat: agregar vista de detalle de producto`).
* **`fix`**: Corrección de un error o bug (e.g. `fix: resolver desalineamiento en el menú responsivo`).
* **`docs`**: Cambios exclusivos en la documentación (e.g. `docs: actualizar el manual de uso de ramas`).
* **`style`**: Cambios que no afectan el significado del código (espacios, formateo, punto y coma omitido).
* **`refactor`**: Reestructuración de código sin añadir características ni corregir errores (e.g. `refactor: modularizar funciones de ayuda`).
* **`test`**: Añadir o modificar pruebas unitarias o de integración.
* **`chore`**: Tareas de mantenimiento o configuración del proyecto (e.g. `chore: actualizar dependencia de eslint`).

---

## ⚠️ Buenas Prácticas y Reglas de Oro

> [!IMPORTANT]
> - **Commits pequeños e iterativos**: Evita realizar commits gigantescos con múltiples tareas no relacionadas. Un commit por cada unidad lógica de trabajo facilita volver atrás si algo sale mal.
> - **No subas archivos confidenciales**: Mantén siempre las credenciales, llaves secretas y entornos locales `.env` listados en el `.gitignore`.
> - **Mantén tu rama actualizada**: Si una tarea dura varios días, haz `git merge develop` (o `git rebase develop`) con frecuencia para solucionar conflictos de manera incremental.
