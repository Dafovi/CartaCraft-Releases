# Políticas de distribución — alcance documental

## Nombres y versiones

Cada artefacto propio tiene versionado y autorización independientes. Para el mod:
tag `event-core-v<versión>`, archivo `event_core-<versión>.jar` y checksum
`event_core-<versión>.jar.sha256`. Primera propuesta: event-core-v0.1.0.
Minecraft/NeoForge/Java se declaran explícitamente; no se infiere compatibilidad
entre versiones. No publicar otros artefactos por extensión de esta autorización.

No usar latest, tags móviles, reemplazos silenciosos de assets ni selección por
nombre aproximado. Una versión publicada fija bytes, tamaño, hash y avisos.
El tag identifica un commit del repositorio de distribución; no afirma que ese
commit haya compilado el mod. No se crean tags en esta fase.

## Integridad e inmutabilidad

SHA-256 del inventario aprobado es la referencia de confianza para event_core.
El sidecar debe coincidir con ella, pero no autentica al editor ni es una firma.
Conservar identidad, aprobaciones y evidencia de verificación posterior. No
añadir textos al JAR, recompilarlo, firmarlo o reempaquetarlo para esta entrega.

No sustituir assets o mover tags publicados. Los cambios de bytes requieren
otra versión aprobada y otro hash, no reutilizar 0.1.0. Una corrección documental
se registra con fecha y commit; no reemplaza silenciosamente los avisos asociados
al binario. Un cambio de términos requiere aprobación y versión documental nueva.
Esta es una política propuesta: **no hay configuración de inmutabilidad de GitHub
habilitada o verificada**, firma ni protección criptográfica de la release.

## Corrección y retirada

Si una versión resulta problemática, suspender su recomendación y abrir una
incidencia con motivo/fecha/identidad afectada, sin datos privados. No modificar
automáticamente instalaciones ni borrar la única copia recuperable del jugador.
Publicar una corrección solo con versión y autorización nuevas; no degradar mundos.

Una retirada urgente de assets por seguridad o derechos requiere autorización
del propietario. Registrar la retirada y mantener una nota pública de versión
retirada cuando sea posible. No reutilizar nombre/tag ni cambiar hashes para
ocultar el problema. Ante un asset ausente, el consumidor falla de forma explícita,
sin buscar mirrors, latest o una versión distinta. Estos procedimientos no se
ejecutan ahora ni autorizan eliminación de objetos remotos.

## Derechos y avisos

Dafovi confirmó la titularidad y autoridad sobre sus aportaciones propias y aprobó
el contenido sustantivo de los términos, todavía pendientes de publicación y
entrada en vigor. No se declara
MIT para el conjunto ni se añade una licencia general al repositorio.
Los archivos de plantilla NeoForged MDK conservan su MIT íntegro, copyright y
derechos propios. Los términos candidatos no restringen esos derechos.

Artes, logos, música, tipografías y marca CartaCraft quedan separados; no se
concede permiso sobre ellos. Minecraft y mods de terceros conservan sus propios
derechos. Este repositorio no redistribuye sus JAR ni les impone términos nuevos.
No atribuir respaldo a Microsoft, Mojang o NeoForged. No almacenar credenciales,
tokens, datos de jugadores ni fuentes privadas en documentos o assets.
