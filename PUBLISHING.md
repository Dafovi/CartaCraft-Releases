# Publicación autorizada de event_core 0.1.0

2026-10-31: Dafovi, titular de las aportaciones propias, autoriza una release
pública event-core-v0.1.0 en Dafovi/CartaCraft-Releases, con exactamente cuatro
assets y términos definitivos vigentes desde su publicación. No autoriza modificar
el catálogo, launcher, servidor u otros repositorios. Verificación remota: PENDING
en este commit previo a publicar; no se afirma un origen validado todavía.

## Secuencia controlada

1. Exigir ambos repositorios limpios y main local/remota sincronizadas; comprobar
   cuenta Dafovi, remoto exacto y ausencia de tag/release. Ante conflicto, detenerse
   sin sobrescribir ni cambiar credenciales, permisos o protecciones.
2. Verificar original event_core-0.1.0.jar: 22700 bytes y SHA-256 aprobado. No
   recompilar, firmar, reempaquetar o incorporarlo al historial Git. Cotejar el
   checksum y MIT original; revisar términos sin ampliar su permiso sustantivo.
3. Revisar diff completo; registrar documentos definitivos en un nuevo commit de
   main y subir solo esa rama. Registrar su SHA completo como objetivo del tag;
   no usar el commit inicial ni un commit privado del código del mod.
4. Crear y subir únicamente event-core-v0.1.0 apuntando a ese commit verificado.
   Comprobar de nuevo que no hay release previa; no mover tags ni reemplazar assets.
5. Preparar un único borrador de release con ese tag ya existente. Adjuntar solo
   los cuatro assets de ASSETS.md. Revisar nombres únicos, estado uploaded, tamaño
   y digest de cada asset contra los originales. Si falta alguno, no hacerla pública.
6. Publicar el borrador completo con el título exacto de RELEASE_NOTES.md. Los
   términos entran en vigor en ese momento. No usar latest como selector de versión.
7. Ejecutar VERIFYING.md: descargar los cuatro assets con controles de transporte,
   cotejar sus bytes y registrar acta pública sin secretos. Si falla, informar
   FAIL/BLOCKED; no alterar el JAR, el inventario o los assets para ocultarlo.
8. Registrar únicamente evidencia documental posterior en main, sin mover el tag
   de la release. Catálogo/launcher siguen sujetos a autorización independiente.

No subir terceros, ZIP de modpacks, instaladores, código privado, logs ni datos
personales. Los archivos fuente automáticos de GitHub corresponden a este repo
de distribución. No prueban compilación reproducible ni contienen el código del mod.
No hay autorización para una segunda release ni retirada destructiva de objetos.
