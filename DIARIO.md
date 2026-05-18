# Diario de trabajo

Este archivo contiene el trabajo de Joaquín para el curso del CEP Introducción a DevOps

### Capturas obligatorias

| #   | Qué debe mostrar la captura                                                       |
| --- | --------------------------------------------------------------------------------- |
| 1   | Terminal con `git remote -v` mostrando `origin` y `upstream`                      |
| 2   | GitHub con la rama `dev` visible en el desplegable de ramas                       |
| 3   | La app en el navegador con la Opción 5 recién añadida                             |
| 4   | El PR de Feature A en GitHub con la pestaña **Files changed** abierta             |
| 5   | El PR de Feature B en GitHub mostrando el banner rojo de conflicto                |
| 6   | Los marcadores de conflicto (`<<<<<<<`, `=======`, `>>>>>>>`) en VS Code          |
| 7   | La app en el navegador con todas las opciones visibles tras resolver el conflicto |
| 8   | Terminal con `git log --oneline` en `main` mostrando todos los commits     


### Tarea 1 — Fork y configuración inicial

1. Haz un fork del repositorio del instructor en tu cuenta de GitHub.
2. Clona tu fork en tu ordenador.
3. Entra en la carpeta `proyecto-demo`, instala las dependencias y arranca la app para confirmar que funciona.
4. Añade el repositorio del instructor como remote con el nombre `upstream`.
5. Verifica con `git remote -v` que tienes tanto `origin` (tu fork) como `upstream` (el instructor).
6. Crea la rama `dev` y súbela a tu fork.

> **Diario:** Escribe qué es un fork y para qué sirve `upstream`. Adjunta la captura 1 y la captura 2.

Un fork es una copia de un repositorio que no me pertenece que hago en mi propia cuenta para trabajar con él. En el caso de esta práctica he partido de un repositorio propiedad de LemonCode y he creado una copia de ese repositorio en mi propia cuenta de Github para poder trabajar libremente con él. 

El repositorio folkeado lo he clonado a mi ordenador en local. Lo hago pinchando en el botón verde “Code” y copiando la ruta url. Desde VS puedo usar la terminal y escribir “git clone [url del proyecto]”.

Abro la terminal y compruebo la versión de node con “node -v”. Luego descargo los paquetes necesarios con “npm install”. Ejecuto el proyecto de ejemplo en mi máquina. Para eso sigo las instrucciones del archivo Readme, arranco la aplicación y compruebo que funciona en el navegador.

Configuración del repositorio. Vamos a revisar la configuración con el comando: “git remote -v”. Se puede configurar el origin y el upstream. En principio sólo está el mio, pero puedo añadir el remote del repositorio original poniendole el nombre "upstream".

Para trabajar tranquilamente y hacer cambios sin modificar la rama principal, creo una rama (branch) llamada "dev". Usamos el comando “git switch -c dev”. Con este comando creamos la rama “dev” si no existe y nos movemos a esa rama. Para publicar la nueva rama a Github, desde la terminal ponemos: “git push -u origin dev”. 

- Captura 1: Terminal con `git remote -v` mostrando `origin` y `upstream` ![captura_01](capturas/captura_01.png)

- Captura 2: GitHub con la rama `dev` visible en el desplegable de ramas ![captura_02](capturas/captura_02.png)                       |

---

### Tarea 2 — Feature branch A: añadir la Opción 5

Esta rama parte de `dev`.

1. Crea la rama `feature/opcion-5` desde `dev`.
2. Abre `src/app.tsx` y añade la siguiente tarjeta al array `OPTIONS`:

```tsx
{
  id: 5,
  title: "Opción 5",
  description: "Pull Request",
  message:
    "Una Pull Request es una propuesta formal para incorporar cambios de una rama a otra. Permite revisar el código antes de mergear y deja un historial claro de qué se hizo y por qué.",
  featureFlag: false,
},
```

3. Además, cambia el campo `description` de la **Opción 3** de su valor actual a:

```tsx
description: "Flujo de trabajo",
```

4. Arranca la app y verifica en el navegador que aparece la Opción 5.
5. Haz un commit con el mensaje: `feat: añadir Opción 5 y actualizar descripción de Opción 3`
6. Sube la rama a tu fork.

> **Diario:** Explica por qué la rama parte de `dev` y no de `main`. Adjunta la captura 3.

Estoy usando la rama "dev" para desarrollo, en esta rama es donde se integran y prueban los cambios y nuevas funcionalidades. Cuando las nuevas funciones estén terminadas y probadas se integran a la rama principal "main".

Para subir al repositorio los cambios locales voy por pasos:
Tengo que preparar los archivos para el commit. Se usa el comando: 
“git add src/app.tsx”

Creo un commit, es decir, una versión guardada de los cambios realizados.
git commit -m "feat: añadir Opción 5 y actualizar descripción de Opción 3"

Subo mi rama feature/opcion-5 al repositorio remoto llamado origin.
El -u deja esa rama conectada al remoto para que después pueda usar git push o git pull sin escribir todo el comando.
git push -u origin feature/opcion-5

- Captura 3: La app en el navegador con la Opción 5 recién añadida ![captura_03](capturas/captura_03.png)
---

### Tarea 3 — Feature branch B: añadir la Opción 6 (aquí está el conflicto)

**Importante:** crea esta rama **ahora**, antes de mergear la Tarea 2. Ambas ramas deben partir del mismo punto en `dev`.

1. Vuelve a `dev` y crea la rama `feature/opcion-6` desde ahí.
2. Abre `src/app.tsx` y añade la siguiente tarjeta al array `OPTIONS`:

```tsx
{
  id: 6,
  title: "Opción 6",
  description: "gitignore",
  message:
    "El fichero .gitignore le dice a Git qué ficheros debe ignorar. Úsalo para excluir ficheros de entorno (.env), dependencias (node_modules) y cualquier cosa que no deba estar en el repositorio.",
  featureFlag: false,
},
```

3. Además, cambia el campo `description` de la **Opción 3** a:

```tsx
description: "Flujo profesional",
```

> Fíjate: la rama A cambió `description` de la Opción 3 a `"Flujo de trabajo"` y esta rama la cambia a `"Flujo profesional"`. Las dos parten del mismo valor original. Eso generará un conflicto cuando intentes mezclarlas.

4. Haz un commit con el mensaje: `feat: añadir Opción 6 y actualizar descripción de Opción 3`
5. Sube la rama a tu fork.

> **Diario:** Explica qué es un conflicto en Git y por qué se va a producir aquí.

Un conflicto en Git aparece cuando dos ramas han cambiado la misma parte del mismo archivo de forma distinta, y Git no sabe automáticamente cuál de las dos versiones debe dejar. En el ejemplo:
- En feature/opcion-5 la Opción 3 cambia description a "Flujo de trabajo".
- En feature/opcion-6 la Opción 3 cambia ese mismo campo a "Flujo profesional".
- Ambas ramas salen del mismo punto en dev, así que parten del mismo valor original, pero después lo modifican de manera distinta.

- Captura 4: Terminal con `git remote -v` mostrando `origin` y `upstream` ![captura_04](capturas/captura_04.png)

- Captura 5: Terminal con `git remote -v` mostrando `origin` y `upstream` ![captura_05](capturas/captura_05.png)

- Captura 6: Terminal con `git remote -v` mostrando `origin` y `upstream` ![captura_06](capturas/captura_06.png)


---

### Tarea 4 — Pull Request 1: Feature A a `dev`

1. Abre una Pull Request en GitHub desde `feature/opcion-5` hacia `dev`.
2. Ponle como título: `feat: añadir Opción 5 y actualizar descripción de Opción 3`
3. Antes de mergear, abre la pestaña **Files changed** y revisa el diff.
4. Mergea el PR.
5. Actualiza tu rama `dev` local con `git pull origin dev`.

> **Diario:** Explica qué revisaste en la pestaña Files changed y por qué es útil hacerlo antes de mergear. Adjunta la captura 4.



---

### Tarea 5 — Pull Request 2: Feature B a `dev`, conflicto

1. Abre una Pull Request desde `feature/opcion-6` hacia `dev`.
2. GitHub detectará un conflicto. No podrá mergear automáticamente.
3. Resuelve el conflicto **en local** siguiendo estos pasos:
   - Ponte en la rama `feature/opcion-6`
   - Descarga `dev` con `git fetch origin dev`
   - Fusiona con `git merge origin/dev`
   - Abre `src/app.tsx` en VS Code y localiza los marcadores de conflicto
   - Decide qué versión conservar: quédate con **`"Flujo profesional"`** (tu versión de esta rama)
   - Guarda el fichero
   - Arranca la app y verifica que se ven todas las opciones correctamente
   - Haz el commit de resolución: `merge: resolver conflicto de descripción en Opción 3`
   - Sube la rama con `git push origin feature/opcion-6`
4. Vuelve al PR en GitHub. El conflicto habrá desaparecido. Mergea el PR.
5. Actualiza tu `dev` local.

> **Diario:** Explica qué significan los marcadores `<<<<<<<`, `=======` y `>>>>>>>` y qué criterio usaste para decidir qué versión conservar. Adjunta las capturas 5, 6 y 7.

---

### Tarea 6 — Limpieza y cierre del diario

1. Borra las dos feature branches en GitHub (botón **Delete branch** o desde la pestaña de ramas).
2. Bórralas también en local:

```bash
git branch -d feature/opcion-5
git branch -d feature/opcion-6
```

3. Ejecuta `git branch` y confirma que solo te quedan `main` y `dev`.
4. Asegúrate de que tu `DIARIO.md` está completo con todas las capturas y haz commit y push.

> **Diario:** Adjunta la captura 8 (`git log --oneline`). Cierra el diario con un párrafo libre: qué te ha resultado más difícil y qué tiene más sentido ahora que antes de la clase.

---

## Tareas opcionales

---

### Opcional 1 — Feature flag

1. Abre el fichero `.env` en `proyecto-demo`.
2. Cambia `VITE_FEATURE_OPCION_3` a `false` y arranca el servidor.
3. Verifica en el navegador que la Opción 3 desaparece sin tocar el código.
4. Devuelve el valor a `true` y reinicia el servidor.

> **Diario:** Explica por qué `.env` no está en Git y para qué sirve `.env.example`.

.env no suele subirse a Git porque puede contener datos sensibles y configuración privada del entorno, como claves, contraseñas o valores distintos para cada equipo o despliegue. Sirve para que cada persona tenga su propia configuración local sin exponerla en el repositorio.

.env.example sirve como plantilla: muestra qué variables necesita el proyecto, pero sin poner los valores reales. Así, cuando alguien clona el repo, sabe qué debe copiar en su propio .env para que la app funcione.

- Captura Opcional 1: Terminal con `git remote -v` mostrando `origin` y `upstream` ![captura_opcional_01](capturas/captura_opcional_01.png)

---

### Opcional 2 — PR final: `dev` a `main`

1. Abre una Pull Request desde `dev` hacia `main`.
2. Título: `release: Opciones 5 y 6 + mejoras Opción 3`
3. Revisa **Files changed** y confirma que entran todos los cambios esperados.
4. Mergea el PR.
5. Actualiza tu `main` local con `git pull origin main`.

> **Diario:** Explica por qué se hace el release desde `dev` y no directamente desde una feature branch.

---