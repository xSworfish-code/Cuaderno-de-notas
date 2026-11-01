# Cuaderno de Notas

Cuaderno del profesor para registrar alumnos, tareas y notas por período escolar, grado y parcial.

- Cada período escolar (por ejemplo 2026-2027) es un cuaderno aparte, con sus propios alumnos, tareas y notas. Los períodos anteriores quedan guardados.
- Al crear un período nuevo puedes copiar los grados y materias del anterior, sin alumnos ni notas.
- Distribución automática de la nota según el grado (1ro–3ro, 4to–6to, 7mo–9no).
- Libreta de notas con botón "Agregar a todos" y acumulado sobre 100.
- Resumen con promedio del parcial, promedio del año y estado de cada alumno.
- Aviso de los puntos de tareas que faltan por asignar en cada parcial.
- Funciona en el teléfono y sin señal (se sincroniza al volver el internet).

Hecho con HTML, CSS y JavaScript. Los datos se guardan en Firebase (Firestore) y se entra con Google.

## Privacidad

Este repositorio **no contiene datos**: ni nombres de alumnos ni notas. Todo eso vive en la base de datos de Firebase del dueño, protegida así:

- Solo se entra con una cuenta de Google.
- Las reglas de `firestore.rules` permiten que cada cuenta lea y escriba **solo su propio cuaderno**. Otra persona que abra la página ve un cuaderno vacío.
- La configuración de Firebase dentro de `index.html` (apiKey, projectId…) **no es secreta**: identifica el proyecto, pero no da acceso a los datos. Lo que protege los datos son las reglas.
- Los respaldos (`respaldo-*.json`) tienen datos reales y están en `.gitignore` para que nunca se suban.

## Instalación

### 1. Firebase
1. Entra a [console.firebase.google.com](https://console.firebase.google.com) y crea un proyecto (puedes desactivar Google Analytics).
2. **Authentication → Comenzar → Google** → actívalo y guarda.
3. **Firestore Database → Crear base de datos** → modo **producción** → elige una ubicación (por ejemplo `us-central1`).
4. En **Firestore → Reglas**, borra lo que hay, pega el contenido de `firestore.rules` y toca **Publicar**.
5. En **Configuración del proyecto (⚙️) → Tus apps → Web (`</>`)**, registra una app y copia el objeto `firebaseConfig`.
6. Pega esos valores en `FIREBASE_CONFIG`, al inicio del `<script>` de `index.html`.

### 2. GitHub Pages
1. Crea un repositorio (por ejemplo `cuaderno-de-notas`) y sube `index.html`, `firestore.rules`, `README.md` y `.gitignore`.
2. **Settings → Pages → Branch: `main` / `(root)` → Save**.
3. La página queda en `https://<tu-usuario>.github.io/cuaderno-de-notas/`.
4. En Firebase, **Authentication → Configuración → Dominios autorizados → Agregar dominio** → `<tu-usuario>.github.io`.

### 3. Primer uso
1. Abre la página y toca **Entrar con Google**.
2. Escribe el período que vas a evaluar (por ejemplo `2026-2027`) y toca **Crear período**.
3. Si tienes un respaldo, toca **Importar respaldo** y elige el archivo `.json`. Se importa al período que tengas abierto.
4. En el teléfono: menú del navegador → **Agregar a pantalla de inicio**.

### Cambiar de período
En **Período**, arriba de los parciales, elige otro período o **+ Nuevo período…**.

## Respaldos
Toca **Descargar respaldo** de vez en cuando (descarga el período abierto) y guarda el archivo en tu computadora o en tu Drive. **No lo subas al repositorio.**
