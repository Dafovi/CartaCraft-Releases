# Verificación reproducible — local ahora, remota después

## Comprobación local de la identidad

Leer la identidad aprobada en artifacts/event_core/0.1.0/artifact.json y cotejar
su sidecar: nombre, versión, base técnica, tamaño y SHA-256 deben coincidir con
el inventario de confianza conservado por el propietario. Este repositorio no
contiene el JAR ni fuentes privadas. No recompilar ni cambiar hashes para
hacer coincidir un archivo diferente.

Para una copia recibida posteriormente, este bloque **local**, sin red, comprueba
nombre, tamaño y hash. $jarPath debe apuntar al temporal propio de esa descarga;
no ejecutar ni modificar el archivo. El hash procede del inventario aprobado,
no del sidecar descargado. Rechazar enlaces/reparse points y usar una carpeta
temporal propia sin componentes enlazados, comprobada antes de descargar.

```powershell
#Requires -Version 7.6
Set-StrictMode -Version Latest
$ErrorActionPreference = 'Stop'
# Definir $jarPath con la ruta absoluta del temporal propio, fuera de instalaciones.
if (-not [IO.Path]::IsPathFullyQualified($jarPath)) { throw 'Ruta absoluta requerida.' }
$jar = Get-Item -LiteralPath $jarPath -Force
if ($jar.PSIsContainer -or ($jar.Attributes -band [IO.FileAttributes]::ReparsePoint)) {
    throw 'No es un archivo regular autorizado.'
}
if ($jar.Name -cne 'event_core-0.1.0.jar' -or $jar.Length -ne 22700) {
    throw 'Nombre o tamaño incorrecto; no instalar.'
}
$expected = '85ba155e5701be6e8c4b9befa8e6be030503e67196c7bf928b0c4f7c824f2249'
if ((Get-FileHash -LiteralPath $jar.FullName -Algorithm SHA256).Hash.ToLowerInvariant() -cne $expected) {
    throw 'SHA-256 diferente; no instalar ni cambiar el inventario.'
}
```

## Verificación pública futura: BLOCKED hasta publicación autorizada

1. Verificar repositorio público exacto `Dafovi/CartaCraft-Releases`, propietario
   Dafovi y commit aprobado. Consultar API GitHub por **tag exacto**
   `https://api.github.com/repos/Dafovi/CartaCraft-Releases/releases/tags/event-core-v0.1.0`.
   Es una ruta hipotética, no consultada en esta fase. No usar latest o búsqueda
   por versión aproximada. Rechazar 404, borrador, tag diferente o commit incorrecto;
   resolver la referencia del tag al commit completo, no fiarse de target_commitish
   si contiene un nombre de rama. Registrar ID de release y asset, sin tokens.
2. Exigir un único asset de cada uno de los cuatro nombres aprobados. Para el JAR:
   state uploaded, size 22700 y browser_download_url exactamente igual a la ruta
   propuesta del contrato. Metadata/digest de GitHub son comprobaciones adicionales,
   no reemplazan el inventario. Avisos/términos deben corresponder al texto aprobado
   y MIT original; fijar sus hashes en el acta final, todavía no existente.
3. Descargar sin autenticación de jugadores, a una carpeta temporal nueva propia,
   sin sobrescribir una instalación sana. Usar HTTPS con validación TLS estándar,
   rechazar userinfo, downgrade, IP/puertos alternativos y redirecciones abiertas.
   Seguir cada Location de forma controlada: máximo 3 saltos, origen inicial
   github.com y destino de assets release-assets.githubusercontent.com únicamente.
   **Cadena concreta pendiente de observar/verificar** al existir la release;
   si GitHub usa otro host, parar para revisar la procedencia, no ampliar comodines.
   No registrar queries firmadas temporales ni cabeceras sensibles.
4. Límites propuestos de la comprobación: conexión 10 s, 120 s por intento,
   máximo 3 intentos, espera máxima Retry-After 30 s, bytes de cuerpo <=22700
   durante streaming. Reintentar solo timeout/429/5xx, con cancelación; abortar
   TLS/origen/404/hash incorrecto y descartar parciales propios. Content-Length
   no sustituye el conteo real. No utilizar una descarga automática que siga
   redirects sin inspección o que solo compruebe el tamaño al terminar.
5. Comprobar archivo completo de 22700 bytes y SHA-256 con el bloque local anterior.
   Verificar sidecar exacto y textos aprobados. HTML, bytes truncados, duplicados,
   falta de avisos o checksum discordante producen rechazo, incluso con HTTP 200.
6. Guardar acta con fecha UTC, repo/tag/commit/releaseID/assetID, URL pública estable,
   nombre/tamaño/hash observados y referencias de avisos. No guardar URL firmada,
   tokens ni datos de cuenta. Conservar el archivo fuera de instalaciones hasta
   autorización de integración; no ejecutarlo como parte de esta verificación.

No hay descargador implementado ni ensayos de red realizados en esta fase.
El operador futuro debe usar un transporte que aplique esos controles; sin él,
la verificación remota queda BLOCKED. Un navegador que complete una descarga
por sí solo no acredita los límites anteriores. Este documento no los da por PASS.
