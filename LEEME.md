# Control de Sures (versión web)

Web que se abre con un enlace normal y se puede instalar en el Android. Entras con tu cuenta de Google y ves las mismas sures en todos tus dispositivos.

Necesitas dos servicios gratuitos: **Firebase** (guarda los datos y hace el login) y **GitHub Pages** (publica la web).

## 1. Crear el proyecto en Firebase
1. Entra en https://console.firebase.google.com con tu cuenta de Google.
2. «Crear un proyecto», ponle un nombre (por ejemplo `sures`) y desactiva Google Analytics.

## 2. Activar el login con Google
1. Menú **Compilación > Authentication > Comenzar**.
2. En «Proveedores de acceso» elige **Google**, actívalo, elige tu correo como correo de asistencia y guarda.

## 3. Crear la base de datos
1. Menú **Compilación > Firestore Database > Crear base de datos**.
2. Elige una ubicación en Europa (por ejemplo `eur3`) y el modo **producción**.
3. Abre la pestaña **Reglas**, borra lo que haya, pega el contenido del archivo `firestore.rules` y pulsa **Publicar**.

## 4. Registrar la app web
1. En **Configuración del proyecto** (la rueda dentada), sección «Tus apps», pulsa el icono web `</>`.
2. Ponle un nombre y pulsa «Registrar app» (no marques Firebase Hosting).
3. Te enseña un bloque `firebaseConfig`. Copia los valores en el archivo `firebase-config.js`, sustituyendo cada `PEGA_AQUI`.

## 5. Publicar la web en GitHub Pages
1. En https://github.com crea un repositorio público llamado `sures`.
2. Pulsa **Add file > Upload files** y sube **todos** los archivos de esta carpeta (ya con `firebase-config.js` rellenado). Pulsa «Commit changes».
3. Ve a **Settings > Pages**. En «Branch» elige `main` y la carpeta `/ (root)`, y guarda.
4. Tras un minuto, tu web estará en `https://TU-USUARIO.github.io/sures/`.

No pasa nada porque `firebase-config.js` sea público: esos valores no son secretos. Lo que protege tus datos son las reglas del paso 3.

## 6. Permitir el dominio en Firebase
En Firebase: **Authentication > Configuración > Dominios autorizados > Añadir dominio** y escribe `TU-USUARIO.github.io`. Sin esto, el botón de Google no funciona.

## 7. Instalar en el Android
Abre tu enlace en Chrome, pulsa el menú de los tres puntos y elige **Instalar aplicación** (o «Añadir a pantalla de inicio»). En el ordenador, abre el mismo enlace y entra con la misma cuenta de Google.

## 8. Pasar los datos que ya tienes
1. En la versión de Claude, pestaña **Casas > Copia de seguridad > Exportar mis datos**. Copia el texto.
2. En la web nueva, pestaña **Casas > Copia de seguridad**, pega el texto en el cuadro y pulsa **Importar datos pegados arriba**.

## Opcional: que solo entres tú
Cada usuario solo ve sus propios datos. Si además quieres que nadie más pueda guardar nada, cambia en `firestore.rules` la condición por:

`request.auth != null && request.auth.uid == userId && request.auth.token.email == "tucorreo@gmail.com"`

## Si cambias archivos más adelante
Sube el número de versión de `CACHE` en `sw.js` (por ejemplo `sures-v2`), para que los móviles carguen la versión nueva.
