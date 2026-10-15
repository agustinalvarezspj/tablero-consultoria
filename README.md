# Tablero Operativo — Consultoría de Marketing

Tablero semanal de tareas del equipo de la consultoría de marketing. Mismo motor que el [tablero de Mar Azul](https://github.com/agustinalvarezspj/tablero-marazul): página estática (GitHub Pages) que guarda los datos en un Google Sheet a través de Google Apps Script.

- **App:** https://agustinalvarezspj.github.io/tablero-consultoria/ *(cuando se publique)*
- **Datos:** Google Sheet propio del tablero *(a crear)*

## Equipo y áreas

- **Personas:** Agustín, Tomás, Franco y Agus Novaira (los cuatro como administradores).
- **Áreas:** Estrategia, Contenido, Tiendas online, Mercadolibre, Publicidad, Eventos, Google ads, Diagnóstico, Captación y Comercialización.

## Qué hace

- Tareas semanales por área y por persona, con prioridad, temporalidad, fecha límite y notas.
- **Permisos:** los administradores crean, editan y eliminan cualquier tarea. Si se agrega un colaborador (`role:'colab'`), puede cargarse tareas a su nombre y editar o eliminar las propias.
- **Traslado automático:** toda tarea pendiente de una semana anterior pasa sola a la semana actual, con la etiqueta «↪ Arrastrada».
- **Mail diario:** cada persona recibe a las 8:00 un correo con sus pendientes (las vencidas en rojo).
- **App instalable (PWA)** en el celular.

## Modo demo

Mientras `API_URL` en `index.html` sea `'TU_URL_DE_APPS_SCRIPT_AQUI'`, el tablero funciona igual pero guarda las tareas **solo en el navegador** de cada uno (no se comparten). Sirve para probarlo; para usarlo en equipo hay que instalar el backend.

## ⚠️ Instalación del backend (una sola vez)

1. Crear un Google Sheet nuevo (ej. «Tablero Consultoría Marketing»). La primera hoja puede quedar vacía: los encabezados se crean solos.
2. En el Sheet: **Extensiones → Apps Script**. Borrar el contenido de `Código.gs` y pegar el de [`apps-script/Code.gs`](apps-script/Code.gs).
3. Completar `SPREADSHEET_ID` con el ID del Sheet (lo que está entre `/d/` y `/edit` en la URL) y los mails del equipo en `EMAILS` (en el repo quedan vacíos porque es público; la copia con los mails está en `apps-script/Code.privado.gs`, que no se sube).
4. En **Configuración del proyecto** verificar zona horaria **Buenos Aires** (GMT-3).
5. Ejecutar una vez **`configurarDisparadorDiario`** y aceptar los permisos (mail diario a las 8:00).
6. **Implementar → Nueva implementación → Aplicación web**: ejecutar como «Yo», acceso «Cualquier usuario». Copiar la URL `.../exec`.
7. Pegar esa URL en `API_URL` dentro de `index.html` y volver a publicar.

Cambios futuros del script: **Implementar → Administrar implementaciones → ✏️ → Nueva versión** (así no cambia la URL).

Para probar sin esperar: `probarTrasladoAhora` o `probarEmailAhora`.

## Agregar o cambiar personas / áreas

- Personas: array `PERSONS` en `index.html` y `EMAILS` / `NOMBRES` en `Code.gs` (mismo `id` en ambos).
- Áreas: array `AREAS` en `index.html` y `AREAS_NOMBRE` en `Code.gs`.

## Estructura

| Archivo | Qué es |
|---|---|
| `index.html` | Toda la aplicación (HTML + CSS + JS) |
| `apps-script/Code.gs` | Backend para pegar en Google Apps Script |
| `manifest.webmanifest`, `sw.js`, `icon-*.png` | PWA (instalable + funciona con mala señal) |
