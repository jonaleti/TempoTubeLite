# Primer APK de TempoTube Lite

## Requisitos

- Node.js 20 o superior.
- Android Studio.
- Android SDK y SDK Platform instalados.
- JDK 21 configurado para Gradle/Android Studio.
- Un dispositivo Android o un emulador.

El identificador Android configurado es `com.tempotube.lite`.

## Preparar el proyecto

```bash
npm install
npm run build
npx cap sync android
```

Si Android Studio no está abierto:

```bash
npx cap open android
```

## Generar APK debug

```bash
npm run android:apk
```

El APK queda en:

```text
android/app/build/outputs/apk/debug/app-debug.apk
```

También se puede generar desde Android Studio con:

`Build > Build Bundle(s) / APK(s) > Build APK(s)`

## Probar en un dispositivo

1. Activar las opciones de desarrollador y la depuración USB.
2. Conectar el dispositivo.
3. Ejecutar `npx cap open android`.
4. Seleccionar el dispositivo en Android Studio.
5. Presionar Run.

## Google OAuth

El cliente Android debe usar:

- Package name: `com.tempotube.lite`
- La SHA-1 del certificado debug para desarrollo.

Para la versión web se mantiene el Client ID web en `VITE_GOOGLE_WEB_CLIENT_ID`.
No incluir secretos OAuth dentro del repositorio.

Para probar Google Identity Services dentro de Capacitor, el Client ID web debe tener
también estos orígenes autorizados en Google Cloud:

```text
http://localhost
https://localhost
http://localhost:5173
http://127.0.0.1:5173
```

El origen `http://localhost` es el que utiliza la WebView de Capacitor. Sin ese origen
Google devuelve `Error 400: origin_mismatch`.

En Android, la aplicación utiliza `@capgo/capacitor-social-login` y el selector de
cuentas nativo de Google. El `webClientId` sigue siendo el Client ID web; el Client ID
Android se valida mediante el paquete y la SHA-1 registrados en Google Cloud. Esto evita
abrir el flujo web `accounts.google.com/gsi/transform` dentro del APK.

