# MeteoND

Visor meteorológico *track-up* inspirado en el Navigation Display del 737NG.

- Tu posición queda fija abajo en el centro y el mapa gira según la dirección de desplazamiento (TRK verdadero).
- La base es OpenTopoMap, oscurecida para que las capas meteorológicas se lean bien.
- Hay tres capas excluyentes:
  - **RADAR**: RainViewer, último fotograma. Se consulta cada 2 minutos y el proveedor publica uno nuevo cada 10.
  - **TEMP**: temperatura a 2 m de Open-Meteo, en una rejilla de 9×9 puntos alrededor de tu posición. Se actualiza cada 15 minutos, al ritmo del dato "current" de Open-Meteo.
  - **VIENTO**: viento a 10 m de Open-Meteo, con campo de velocidad y partículas animadas. Mismo ritmo de actualización que TEMP.
- Si vuelves a pulsar el botón activo, la capa se apaga.
- Con el pellizco se cambia la escala. El número sobre el anillo discontinuo es la distancia en km hasta ese anillo.
- En la esquina superior izquierda verás:
  - **GS**: velocidad sobre el terreno, en km/h.
  - **Viento en tu posición**: dirección de procedencia y velocidad en km/h, con una flecha relativa a la pantalla.
  - **SAT**: temperatura exterior.
- La pantalla se mantiene encendida mientras la app está visible.

## Ponerla en el móvil (GitHub Pages, gratis)

La geolocalización exige HTTPS, así que hay que alojarla. Abrir el `index.html` desde los archivos del teléfono no sirve.

1. En github.com crea un repositorio público, por ejemplo `meteond`.
2. Pulsa **Add file → Upload files** y sube los 6 archivos de la carpeta. No subas el zip.
3. Ve a **Settings → Pages → Branch: main / root → Save**.
4. Al cabo de un minuto la app estará en `https://TU_USUARIO.github.io/meteond/`.
5. Ábrela en Chrome para Android, acepta el permiso de ubicación y pulsa **⋮ → Instalar app** (o **Añadir a pantalla de inicio**).

Para probarla sin moverte, añade `?sim` a la dirección: `https://TU_USUARIO.github.io/meteond/?sim`. Simula un recorrido a 90 km/h con giros suaves.

## Limitaciones de las fuentes gratuitas

- **RainViewer**:
  - Desde enero de 2026 sirve el radar como máximo a zoom 7. A escalas de detalle la capa se amplía y se ve suavizada.
  - Solo ofrece la paleta "Universal Blue". Los colores de la leyenda son aproximados.
  - Es para uso personal y no comercial.
- **Open-Meteo**: es gratuito para uso no comercial, con un límite de unas 10 000 llamadas al día. Cada punto de la rejilla cuenta como una llamada, así que son 81 por actualización. Con TEMP o VIENTO activos sin parar quedan unas 7 800 al día. Para un uso normal sobra.
- **OpenTopoMap**: su política permite el uso personal moderado.

## Archivos

- `index.html`: la app completa.
- `manifest.webmanifest`, `icon-192.png` e `icon-512.png`: lo necesario para instalarla como app.
- `sw.js`: guarda la app en caché para que arranque rápido. Mapas y datos meteorológicos se piden siempre a la red.
