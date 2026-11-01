# MeteoND

Visor meteorológico *track-up* inspirado en el Navigation Display del 737NG.

## Pantalla

- **Arriba en el centro:** el rumbo de desplazamiento (TRK verdadero).
- **Arriba a la izquierda:** tu velocidad (GS, km/h).
- **Arriba a la derecha:** el valor de la capa activa en tu posición:
  - RADAR: reflectividad en dBZ, el máximo en unos 3 km a tu alrededor. Pone "SIN ECO" si no llueve y "NIEVE" si el proveedor lo marca como nieve.
  - TEMP: temperatura a 2 m (°C).
  - VIENTO: velocidad a 10 m (km/h).
  - NIEBLA: visibilidad (km).
- **Arco graduado:** está en el borde superior y gira con tu rumbo. Su distancia a tu posición es la escala elegida: 20, 50 o 100 km.
- **Línea de rumbo:** lleva dos marcas de distancia en km.
- **Avisos ámbar:** solo aparecen cuando algo falla (GPS, o una fuente no disponible).
- **Atribución de las fuentes:** el botón **©**, abajo a la derecha. Está plegado por defecto.

## Botones

- **Fila superior:**
  - Escala: **20 KM · 50 KM · 100 KM**.
  - **INCEND** y **TRÁFICO**: se superponen a cualquier capa y se activan o desactivan cada una por separado.
- **Fila inferior:** **RADAR · TEMP · VIENTO · NIEBLA**. Son excluyentes; si pulsas la capa activa, se apaga.

## Fuentes

Ninguna requiere cuenta ni clave.

| Capa | Fuente | Actualización |
|---|---|---|
| Mapa | OpenTopoMap | — |
| Radar | RainViewer (último fotograma, paleta Universal Blue) | se consulta cada 2 min; el proveedor publica cada 10 min |
| Temp / viento / niebla | Open-Meteo, rejilla de 9×9 puntos alrededor de ti | cada 15 min |
| Incendios | NASA GIBS: focos VIIRS (NOAA-20 y Suomi-NPP) de hoy y ayer | cada 30 min; los datos llegan con cada pasada del satélite |
| Retenciones | DGT, incidencias DATEX II | cada 3 min; la DGT publica cada minuto |

## Limitaciones conocidas

- **Radar:** RainViewer solo sirve hasta zoom 7 (≈1 km por píxel). En la escala de 20 km se ve suavizado.
- **Niebla:** es la visibilidad prevista por el modelo, no una observación. Se pinta como velo gris a partir de unos 6 km de visibilidad, más opaco cuanto menor es.
- **Retenciones:**
  - Se dibujan en rojo las de tráfico parado o en cola, y en ámbar las de tráfico lento.
  - Cuando la DGT da dos puntos se dibuja un tramo recto entre ellos; si solo da uno, un punto.
  - Cataluña y País Vasco no están incluidos: publican aparte.
  - El fichero de la DGT es de toda España. Con la capa activa se descarga cada 3 minutos, lo que gasta datos móviles.
  - Si la DGT no permite leer el fichero desde el navegador, verás el aviso **TRÁFICO N/D**. En ese caso hay que poner un intermediario en la constante `TRAFFIC_URL` de `index.html`.
- **Incendios:** si aparece **INCEND N/D**, el servidor de la NASA no responde o bloquea la petición.

## Actualizar en GitHub

Sube los archivos nuevos con **Add file → Upload files** y pulsa **Commit changes**; se sobrescriben. Si el móvil sigue mostrando la versión anterior, cierra la app y vuelve a abrirla.

Para probar sin moverte: `https://gonzalbaz-eng.github.io/meteond/?sim`
