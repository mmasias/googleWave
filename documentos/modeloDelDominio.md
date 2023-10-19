# Modelo del dominio

## Idea base

- Una "wave" era la unidad básica de conversación, similar a un hilo en un foro. Cada wave podía tener múltiples "blips" que eran contributions individuales.
- Los blips podían ser mensajes de texto, archivos, imágenes, etc. Cada blip tenía un autor y timestamp.
- Las waves permitían edición colaborativa en tiempo real, todos los participantes podían editar y ver los cambios simultáneamente blip por blip.
- Las waves podían tener relaciones padre-hijo, similares a hilos de discusión, donde una nueva wave surge de otra previa.
- Existía un servidor central donde se almacenaban todas las waves. Los clientes se conectaban en tiempo real para enviar/recibir updates.
- La información se replicaba en servidores para escalar. Los clientes se conectaban al servidor más cercano.
- Había APIs para acceder a la información de las waves desde aplicaciones externas.
- Los datos se almacenaban en BigTable, la base de datos distribuida de Google.
- El frontend utilizaba tecnologías como AJAX para actualizaciones en tiempo real.

## Primera versión

Interesa obtener un modelo del dominio general, con ciertos detalles y sobretodo atendiendo a la definición de modelo del dominio, esto es, sin entrar en detalles técnicos finales, pero sí describiendo adecuadamente la solución.

|||
|-|-|
![](../imagenes/modelosUML/gW-v0.svg)|![](../imagenes/modelosUML/gW-v0C.svg)

En este modelo tenemos:

- La Wave como la entidad central que representa una conversación o hilo de discusión. Tiene atributos como id, título y fecha de creación.
- El Blip que representa una contribución individual dentro de una Wave. Tiene atributos como id, contenido, autor y fecha de creación.
- El User que representa a un usuario del sistema. Un blip es creado por un usuario.
- Las Waves contienen 0 o más Blips.
- Los Blips son creados por un User.

Este modelo intenta capturar la esencia del dominio de Google Wave sin entrar en detalles de implementación. Me enfoco en las principales entidades, sus atributos y relaciones.

## Iteración...

<div align=center>

![](/imagenes/modelosUML/gW-v1C.svg)

</div>

- Se agrega la entidad Thread para modelar hilos de discusión dentro de una Wave
- Una Wave puede contener multiples Threads
- Un Thread contiene multiples Blips
- Se agrega la entidad Annotation para representar anotaciones/comentarios sobre un Blip específico.
- Un Blip puede contener multiples Annotations

De esta forma se puede modelar threads de discusión y respuestas/comentarios a un blip de manera más granular.

## Iteración...

<div align=center>

![](/imagenes/modelosUML/gW-v2C.svg)

</div>

- Wave ahora tiene atributos como privacidad (isPrivate) y lista de participantes
- Thread tiene título y fecha de creación
- Blip ahora está asociado a un Thread como padre
- Blip ahora puede tener múltiples Annotations y Attachments
- Attachment modela archivos adjuntos a un Blip
- Annotation y Blip tienen autoría con relación a un User

De esta forma se pueden modelar con más detalle los metadatos, contenidos, relaciones y autoría de las diferentes entidades. 