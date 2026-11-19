# Notas de verificación (2026-11-17)

Comprobado en Chromium de escritorio, desde España, una sola hora del día. **No** probado aún en el WebView del Chromecast.

## En la lista (se ven sin cuenta)

| Canal | Reproductor | Notas |
|---|---|---|
| Antena 3, laSexta | Atresplayer, `<video>` blob en página | **Solo con cookies aceptadas** (rechazarlas = muro Premium); el usuario lo decidió el 2026-11-17 y la receta las acepta. Sin cuenta. Hay que pulsar `button[aria-label="Directo"]` en la ficha, ~40 s de pre-roll y luego directo. Sin botón CC. Probado Antena 3; laSexta usa la misma receta, sin probar por separado. |
| Telecinco, Cuatro | Mediaset Infinity, Shaka Player | **Solo con cookies aceptadas** (mismo motivo y decisión). Sin cuenta. Autoplay; el modal «Has preferido rechazar…» desaparece al aceptar. 1 pista `subtitles` oculta de Shaka, sin botón CC identificado. Probado Telecinco; Cuatro sin probar por separado. |
| RTVE 24h | THEOplayer, `<video>` en página | Autoplay con sonido. Sin banner de cookies en la prueba. Comprobar que no es simulcast de La 1. |
| TV3, 3Cat Info, SX3, 33, Esport3 | Bitmovin | Pre-roll de ~60 s. Subtítulos: `select.bmpui-ui-subtitleselectbox` (solo con programa subtitulado). Marcado `x-subs` solo TV3. |
| ETB1, ETB2 | Player propio en etbon.eus | Pre-roll IMA ~35 s. No se ve botón CC. |
| TVG, TVG2 | agalega.gal | Banner Sourcepoint en iframe (se oculta con CSS, no se rechaza). |
| Canal Sur | canalsurmas.es | Pre-roll ~20 s. |
| Telemadrid, La Otra | Brightcove / video.js | Existe `.vjs-subs-caps-button`, sin pistas en la prueba. |
| À Punt | video.js | Sin autoplay: receta con `play`. Pre-roll ~20 s. |
| TPA | video.js | Banner Cookiebot. Autoplay con sonido. |
| La 7 Castilla y León | Clappr | Autoplay. La 8 (provincias): solo León probada; Valladolid dio error de manifiesto. |
| Canal Extremadura | Player propio en canalextremadura.app | Autoplay. |

## Añadidos a mano por el dueño de la lista (2026-11-17, sin verificar por Claude)

Neox, Nova, Mega, Atreseries (Atresplayer: misma receta que Antena 3, aceptan cookies); Factoría de Ficción, Boing, Divinity,
Energy, Be Mad (Mediaset Infinity: misma receta que Telecinco); DMAX, DKISS, TEN, Paramount Network, TRECE, Gol Play,
Real Madrid TV, Squirrel, Veo 7 (webs propias, receta `default`, que rechaza cookies). Si alguno pide aceptar cookies o cuenta,
se hace una vez con el modo cursor (OK en el mando) y queda guardado; si hace falta automatizarlo, receta por dominio en `recipes.json`.
Orden y selección de la lista: son los del dueño, no se reordenan.

### Revisión del 2026-11-19 de «Otros operadores nacionales»

Tras las pruebas en el Chromecast (algunos de estos canales no se veían) se comprobaron las 9 URLs en Chromium de escritorio
(no en el WebView) y sus códigos HTTP con curl. Ninguna de las 9 URLs originales daba el directo tal cual.

| Canal | Resultado | Cambio |
|---|---|---|
| Paramount Network | `paramountnetwork.es` redirige a Pluto TV | Se puso la URL de Pluto (`https://pluto.tv/es/watch/live-tv/29330/`, canal FAST, con anuncios) y después **se eliminó de la lista** (decisión del dueño, 2026-11-19): el canal de TDT habría cedido su frecuencia a Squirrel 2 el 1-ene-2026 (según un resumen de búsqueda de Xataka/Espinof, sin confirmar) |
| TRECE | `trecetv.es` redirige a `cope.es/directos/trece`; el reproductor arranca en modo audio y el vídeo está oculto | URL → `https://www.cope.es/directos/trece` y receta `cope.es` que pulsa el botón «Video» (comprobado: el vídeo pasa a ocupar la pantalla). Los programas «POR TV» (p. ej. la teletienda) salen con la cartela «sin derechos de emisión a través de internet»: es de la propia emisión |
| Real Madrid TV | con `es-es` en minúsculas la web da error; con `es-ES` carga, pero pide cuenta Madridista gratuita | Primero URL `https://www.realmadrid.com/es-ES/real-madrid-tv` con `x-login="1"`; después pasó a **flujo HLS directo** sin cuenta (ver «Flujos HLS directos») |
| Gol Play | `golplay.com` no conecta (sin respuesta); TDTChannels ya no lo lista | **Eliminado de la lista** (decisión del dueño). Si algún día se quiere algo parecido: Replay (`https://replaytv.es/en-directo`, de Mediapro; reproductor Dailymotion que arranca solo), que no es el mismo canal |
| DMAX | `max.com` redirige a `hbomax.com` (404, de pago); `dmax.es` solo tiene VOD | `x-disabled="1"`: sin directo web gratuito |
| DKISS, TEN | 404; sus webs solo tienen guía de programación | `x-disabled="1"`: sin directo web |
| Squirrel | redirección rota (`squirreltv.esdirecto`); su web no tiene directo (ver abajo) | `x-disabled="1"`: sin directo web |
| Veo 7 | `veo7.es/directo` va a la home `veo7.com`; el vídeo que avanza es un promocional | `x-disabled="1"`: sin directo web |

Pluto y Real Madrid TV están sin probar en el Chromecast. Para reactivar un canal desactivado, borra su `x-disabled="1"`.

### TDTChannels (https://www.tdtchannels.com/listas/), 2026-11-19

Su lista (`https://www.tdtchannels.com/lists/tv.json`) trae DMAX, DKISS, Ten, Veo7, Squirrel y Squirrel2 con 0 emisiones
online, y ya no trae Gol Play. Que Telecinco, Cuatro, FDF, Energy, Divinity, Be Mad y Boing también salgan con 0 no significa que no
haya directo: los ven en la web de Mediaset (con cookies aceptadas), solo que su lista no incluye ese tipo de emisión. TDTChannels
solo da enlaces directos `.m3u8`/YouTube; los `.m3u8` se reproducen desde la app 0.3.0 (ver más abajo), los de YouTube no.

### Flujos HLS directos (app 0.3.0 o posterior)

Una URL que termina en `.m3u8` se reproduce con el reproductor nativo de Android, sin página web, sin cuenta y sin cookies.

| Canal | Estado |
|---|---|
| Real Madrid TV | **En la lista** (2026-11-19): `https://rmtv.akamaized.net/hls/live/2043153/rmtv-es-web/master.m3u8`. Comprobado con curl: responde 200 sin cuenta ni token, igual con el User-Agent de Android y el de un navegador; lista maestra con 3 calidades (320x180 a 1280x720, H.264 + AAC), segmentos MPEG-TS de 6 s, sin `EXT-X-MAP`. Variante en inglés: `.../2043154/rmtv-en-web/master.m3u8`. Sin probar en el Chromecast |
| La 1, La 2, 24 Horas, Clan, Teledeporte | **En la lista** (2026-11-19): `https://rtvelivestream.rtve.es/rtvesec/<canal>/<canal>_main_dvr.m3u8` (`la1`, `la2`, `24h`, `clan`; Teledeporte: `tdp/tdp_main.m3u8`). Sin cuenta ni token, listas maestras de 3-4 calidades (hasta 720p), segmentos TS. La web de RTVE Play queda como `x-web` de respaldo |
| TRECE | **En la lista**: `https://play.cdn.enetres.net/091DB7AFBD77442B9BA2F141DCC182F5021/021/playlist.m3u8` (1080p, TS); respaldo `x-web` = la web de COPE con su receta. Los programas «POR TV» salen con la cartela de sin derechos de emisión |
| 3Cat Info, SX3, Canal 33, Esport3 | **En la lista**: `directes-tv-es.3catdirectes.cat/live-content/<canal>-hls/master.m3u8` (`canal324`, `super3`, `c33-super3`; Esport3 solo tiene `live-origin/esport3-hls`). TS, hasta 1080p, sin anuncios previos. **TV3 se queda con la web** (tiene `x-subs`: el flujo directo no ofrece subtítulos); su flujo TS existe (`directes3-tv-cat.3catdirectes.cat/live-content/tv3-hls/master.m3u8`) |
| ETB1, ETB2, TVG, TVG2, Canal Sur, Canal Extremadura | **En la lista**: `cdn1.etbon.eus/etb{1,2}/index.m3u8`, `crtvg-europa.flumotion.cloud/playlist_dvr.m3u8` (TVG), `crtvg-tvg2.flumotion.cloud/playlist_dvr.m3u8`, cloudfront de Canal Sur (`CanalSurAndaluciaES.m3u8`) y de Canal Extremadura. Todos TS, 200 sin token (comprobado con curl el 2026-11-19) |
| À Punt | **Se queda con la web**: su flujo (`fastly.live.brightcove.com/.../playlist-hls-dvr.m3u8`) usa fMP4/CMAF (`EXT-X-MAP`, segmentos `.mp4`), que el reproductor nativo de Android reproduce mal, y lleva un JWT en la ruta |
| Telemadrid, La Otra, TPA, La 7 CyL, Aragón TV, Atresmedia, Mediaset | Sin flujo en TDTChannels: se quedan con la web |

### Guía de programación (app 0.4.0 o posterior)

La cabecera de la lista lleva `url-tvg="https://www.tdtchannels.com/epg/TV.xml.gz"` (XMLTV, ~0,6 MB comprimido, 188 canales,
unos 2,5 días; TDTChannels la regenera cada día sobre las 07:00 UTC). El `tvg-id` de cada canal es su id en esa guía
(`La1.TV`, `TDP.TV`, `324.TV`, `13.TV`, `RMTV.TV`, `Bemad.TV`…). Cubre 31 de los 37 canales activos; **no tiene Atresmedia**
(Antena 3, laSexta, Neox, Nova, Mega, Atreseries), que salen sin programa. Comprobado el 2026-11-19 con el analizador real:
400 ms para leer el XML y 97 KB de caché en disco.

### Squirrel y Squirrel 2

Son dos canales de TDT de Squirrel Media: Squirrel (cine; `squirreltv.es`) y Squirrel 2 o «Squirreldos» (ficción; `squirrel2.tv`).
Los dos tienen una página `live.php`, pero el enlace «EN DIRECTO» del menú está comentado en el HTML y la página no lleva
reproductor: no hay directo web. Squirrel+ (`squirrelplus.com`) es una plataforma gratuita de cine y series bajo demanda con registro
opcional, sin canales en directo en su portada. En TDTChannels, ambos con 0 emisiones. Se ven por TDT y por operadores.

## Con cuenta gratuita (`x-login`, app 0.2.0 o posterior)

**Desde la 0.4.0 los canales de RTVE (La 1, La 2, 24 Horas, Clan, Teledeporte) van por flujo HLS directo y no necesitan cuenta**;
solo piden cuenta si cae a la web (`x-web`). Aragón TV sigue siendo el único con cuenta de verdad. Los tres textos siguientes
describen la web: La 1, La 2, Teledeporte, Clan (RTVE, `login_advice`) y Aragón TV (aragonplay.es). Están en la lista; la primera vez hay que
iniciar sesión con OK (modo cursor y teclado) y la sesión queda guardada. Sin probar en el Chromecast: no se sabe aún si el
formulario de acceso funciona con el cursor, si el directo arranca solo tras iniciar sesión, ni cuánto dura la sesión.

## Fuera de la lista
- **Reproductor en iframe cruzado o sin autoplay:** TV Canaria (RTVC, iframe codev8 + Sourcepoint), IB3 (YouTube tras pulsar play), CMM TV (iframe Mangomolo), 7RM (los scripts del reproductor esperan un evento de ratón real).
- **Más canales de Atresmedia y Mediaset** (Neox, Nova, Mega, Atreseries, FDF, Divinity, Energy, BeMad, Boing): mismas plataformas y misma receta; sin añadir ni probar todavía.
- **Navarra TV:** mostraba pantalla de desconexión; reprobar a otra hora.
- **13TV:** sin directo web a la hora de la prueba (Teletienda); solo ciertos programas son «por TV y online».

## Pendiente de probar en el Chromecast

Autoplay con sonido en WebView, tamaño real del viewport, DRM, pre-rolls, y que `ccJs` de 3Cat active subtítulos en un programa subtitulado.
