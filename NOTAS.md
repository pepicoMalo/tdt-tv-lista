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

## Fuera de la v1

- **Piden cuenta gratuita:** La 1, La 2, Teledeporte, Clan (`login_advice`), Aragón TV (aragonplay.es).
- **Reproductor en iframe cruzado o sin autoplay:** TV Canaria (RTVC, iframe codev8 + Sourcepoint), IB3 (YouTube tras pulsar play), CMM TV (iframe Mangomolo), 7RM (los scripts del reproductor esperan un evento de ratón real).
- **Más canales de Atresmedia y Mediaset** (Neox, Nova, Mega, Atreseries, FDF, Divinity, Energy, BeMad, Boing): mismas plataformas y misma receta; sin añadir ni probar todavía.
- **Navarra TV:** mostraba pantalla de desconexión; reprobar a otra hora.
- **13TV:** sin directo web a la hora de la prueba (Teletienda); solo ciertos programas son «por TV y online».

## Pendiente de probar en el Chromecast

Autoplay con sonido en WebView, tamaño real del viewport, DRM, pre-rolls, y que `ccJs` de 3Cat active subtítulos en un programa subtitulado.
