# 🌸 Anahata Studio — Instrucciones de instalación

Sigue estos pasos para tener tu app funcionando en la web e instalable en teléfono.
Tiempo estimado: **30–45 minutos**.

---

## PASO 1 — Crear proyecto en Firebase (base de datos gratuita)

1. Ve a **https://console.firebase.google.com**
2. Inicia sesión con tu cuenta de Google
3. Haz clic en **"Agregar proyecto"**
4. Nombre del proyecto: `anahata-studio` (o el que prefieras)
5. Desactiva Google Analytics (no es necesario) → clic en **"Crear proyecto"**

### Activar Firestore (la base de datos)

1. En el menú izquierdo busca **"Compilación" → "Firestore Database"**
2. Clic en **"Crear base de datos"**
3. Selecciona **"Comenzar en modo de prueba"** → Siguiente
4. Elige la región más cercana (ej: `us-central1`) → Listo

### Obtener tu configuración Firebase

1. En Firebase, haz clic en el ⚙️ (engrane) junto a "Descripción general del proyecto"
2. Selecciona **"Configuración del proyecto"**
3. Baja hasta la sección **"Tus apps"**
4. Haz clic en el ícono **`</>`** (web)
5. Nombre de la app: `Anahata Web` → clic en "Registrar app"
6. Verás un bloque de código como este:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "anahata-studio.firebaseapp.com",
  projectId: "anahata-studio",
  storageBucket: "anahata-studio.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

7. **Copia estos valores** — los necesitarás en el siguiente paso.

---

## PASO 2 — Agregar tu configuración al archivo index.html

1. Abre el archivo `index.html` con un editor de texto
   - En Windows: clic derecho → "Abrir con" → Bloc de notas
   - En Mac: clic derecho → "Abrir con" → TextEdit
2. Busca esta sección cerca de la línea 200:

```js
const FIREBASE_CONFIG = {
  apiKey:            "REEMPLAZA_CON_TU_API_KEY",
  authDomain:        "REEMPLAZA_CON_TU_PROJECT_ID.firebaseapp.com",
  projectId:         "REEMPLAZA_CON_TU_PROJECT_ID",
  ...
};
```

3. Reemplaza cada valor `"REEMPLAZA_..."` con los valores de tu proyecto Firebase
4. Guarda el archivo

---

## PASO 3 — Agregar los íconos de la app

La app necesita dos archivos de ícono para instalarse correctamente en teléfonos:

- `icon-192.png` — 192×192 píxeles
- `icon-512.png` — 512×512 píxeles

**Opción fácil:** Usa una foto del logo de Anahata y renómbrala.
Puedes redimensionarla gratis en: **https://squoosh.app**

Coloca los dos archivos PNG en la misma carpeta que `index.html`.

---

## PASO 4 — Publicar la app en internet (hosting gratuito)

Usaremos **Vercel** — es gratuito y muy sencillo.

1. Ve a **https://vercel.com** y crea una cuenta gratuita (puedes usar tu cuenta de Google)
2. Haz clic en **"Add New → Project"**
3. Selecciona **"Deploy from CLI"** o usa la opción de arrastrar archivos:
   - Haz clic en **"Upload"** o arrastra tu carpeta con los 4 archivos:
     - `index.html`
     - `manifest.json`
     - `sw.js`
     - `icon-192.png`
     - `icon-512.png`
4. Vercel te dará una URL como: `https://anahata-studio.vercel.app`
5. ¡Listo! Esa es la dirección de tu app.

### Dominio personalizado (opcional)
Si quieres usar `anahata.com.mx` o similar:
- Compra el dominio en **Namecheap.com** (~$200 MXN/año)
- En Vercel → Settings → Domains → agrega tu dominio

---

## PASO 5 — Instalar la app en tu teléfono

### En Android (Chrome):
1. Abre la URL de tu app en Chrome
2. Aparecerá un banner en la parte inferior: **"Agregar a pantalla de inicio"**
3. Si no aparece: toca los tres puntos ⋮ → "Agregar a pantalla de inicio"
4. La app se instalará como si fuera nativa

### En iPhone (Safari):
1. Abre la URL en Safari
2. Toca el ícono de compartir (cuadro con flecha hacia arriba)
3. Selecciona **"Agregar a la pantalla de inicio"**
4. Ponle nombre y toca "Agregar"

---

## Reglas de seguridad en Firestore (recomendado)

Por defecto, tu base de datos está abierta. Para mayor seguridad, en Firebase Console:

1. Ve a **Firestore Database → Reglas**
2. Reemplaza el contenido con esto:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /estudio/{document=**} {
      allow read, write: if request.time < timestamp.date(2025, 12, 31);
    }
  }
}
```

Esto limita el acceso a una fecha específica. Para protección real con contraseña, 
consulta la documentación de Firebase Authentication.

---

## Preguntas frecuentes

**¿Los datos están seguros?**
Sí, se guardan en los servidores de Google (Firebase) con cifrado. Nadie más puede ver tu información a menos que tenga tu configuración.

**¿Funciona sin internet?**
Sí, gracias al Service Worker. Puedes ver los datos en modo offline y se sincronizan cuando vuelve la conexión.

**¿Puedo usarlo en múltiples dispositivos?**
Sí. Como los datos están en Firebase, si abres la app en tu teléfono y en la computadora del estudio, verás exactamente lo mismo en tiempo real.

**¿Cuánto cuesta Firebase?**
El plan gratuito (Spark) incluye 50,000 lecturas y 20,000 escrituras por día — más que suficiente para un estudio pequeño.

**¿Qué pasa si se llena el plan gratuito?**
Firebase te avisará. El plan de pago (Blaze) cobra aproximadamente $0.06 USD por cada 100,000 lecturas adicionales — centavos.

---

📍 200 casi esq con Paris. Frente al Cinépolis  
📱 (644) 260-2332 · 📷 @anahata.est
