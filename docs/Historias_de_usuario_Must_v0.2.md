# Sistema de Gestión de Factoring — Historias de usuario Must (v0.2)

Base: `Requerimientos_v0.2.md`. Alcance: maqueta (frontend).
Revisado con el cliente (Moisés Luque) el 10-nov-2026, con los pendientes confirmados el mismo día. Versión anterior: `Historias_de_usuario_Must_v0.1.md`.
Formato: Como [rol], quiero [acción] para [beneficio]. Criterios en Dado / Cuando / Entonces.

**[P]** = regla propuesta por el equipo. El cliente no la dio. Hay que validarla.
**Δ v0.2** = historia cambiada en esta versión.
**RF / RNF** = requerimiento de origen. Ver la matriz de trazabilidad al final.

---

## Cambios respecto a v0.1

| Historia | Cambio | Requerimiento |
|---|---|---|
| HU-05 | Funciones "designadas" al rol, no "limitadas". | RF-05 |
| HU-06 | El formulario incluye tipo de factoring y modalidad, ambos obligatorios. | RF-16, RF-44 |
| HU-07 | Nuevo campo: plazo en días (CA4). | RF-08 |
| HU-14 | "marcar" → "registrar el estado" del documento. | RF-18 |
| HU-18 | El motivo de rechazo es opcional. | RF-23 |
| HU-19 | Notificación dentro del sistema; motivo solo si se ingresó. | RF-24 |
| HU-20 | El aprobador también puede enviar contrato y endoso. | RF-25 |
| HU-21 | Reescrita: el sistema genera la preliquidación. | RF-28 (fusión con RF-29) |
| Matriz | Administrador consulta solicitudes; aprobador envía contrato y endoso. | RF-25, RF-46 |
| HU-01 | El registro exige aceptar la declaración de datos (CA4). | RF-02, RNF-03 |
| HU-09, HU-16 | Adjuntos: solo PDF, hasta 20 MB. | RNF-09 |
| HU-18 | Motivo en texto libre. | RF-23 |

---

## Matriz de permisos por rol (revisada con el cliente)

| Función | Exportador | Operador | Aprobador | Administrador |
|---|---|---|---|---|
| Crear y ver sus propias solicitudes | ✓ | – | – | ✓ (consulta de todas) Δ |
| Ver bandeja de solicitudes | – | ✓ | ✓ (solo "En aprobación") | ✓ (consulta) |
| Registrar estado de documentos y pedir adicionales | – | ✓ | – | – |
| Enviar a aprobación | – | ✓ | – | – |
| Aprobar o rechazar | – | – | ✓ | – |
| Enviar contrato y endoso / ver preliquidación | Ve la suya | ✓ | ✓ Δ | – |
| Usuarios y mantenimientos | – | – | – | ✓ |
| Ver historial de una operación | Solo la suya | ✓ | ✓ | ✓ |

---

## Épica 1 — Cuentas y acceso

### HU-01 Registrarme como exportador Δ
Como **exportador**, quiero crear mi cuenta con mis datos legales para solicitar factoring en línea.
*RF-01, RF-02 · RNF-03*

- **CA1.** Dado que estoy en la pantalla de registro, cuando ingreso nombre legal, cédula o RUC, domicilio legal, correo, código postal, usuario y contraseña, y envío, entonces se crea mi cuenta y veo un mensaje de confirmación.
- **CA2.** Dado que dejo un campo obligatorio vacío, cuando envío, entonces el sistema marca ese campo y no crea la cuenta.
- **CA3 [P].** Dado que la cédula o RUC ya está registrada, cuando envío, entonces el sistema no crea la cuenta y lo informa.
- **CA4.** Dado que no he aceptado la declaración de uso de datos, cuando intento crear la cuenta, entonces el botón "Crear cuenta" está deshabilitado.

> Una cuenta = un usuario por exportador (cliente).
> Código de verificación por correo: fase futura (acordado con el cliente).

### HU-02 Iniciar sesión
Como **usuario del sistema**, quiero iniciar sesión con mi usuario y contraseña para acceder a mis funciones.
*RF-03 · RNF-05*

- **CA1.** Dado que mi cuenta está activa, cuando ingreso credenciales válidas, entonces entro a la pantalla de inicio de mi rol.
- **CA2.** Dado que ingreso credenciales incorrectas, cuando envío, entonces veo un mensaje de error que no indica cuál dato falló.
- **CA3.** Dado que fallé 5 veces seguidas, cuando intento de nuevo, entonces la cuenta queda bloqueada 15 minutos. (Aceptado por el cliente.)

### HU-03 Crear usuarios internos con rol
Como **administrador**, quiero crear usuarios internos del factor y asignarles un rol para dar acceso a nuevos empleados.
*RF-04*

- **CA1.** Dado que estoy en "Usuarios", cuando ingreso nombre, correo y rol (operador, aprobador o administrador) y guardo, entonces el usuario aparece en la lista como activo.
- **CA2.** Dado que falta el rol o el correo, cuando guardo, entonces el sistema no crea el usuario y marca el campo.

> El administrador no crea cuentas de exportadores: cada exportador crea la suya (HU-01).

### HU-04 Desactivar usuarios internos
Como **administrador**, quiero desactivar un usuario interno para impedir el acceso de quien ya no trabaja en el factor.
*RF-04*

- **CA1.** Dado un usuario activo, cuando lo desactivo, entonces aparece como inactivo y ya no puede iniciar sesión.
- **CA2.** Dado un usuario desactivado, cuando reviso operaciones que gestionó, entonces su nombre sigue en el historial.

### HU-05 Ver las funciones designadas a mi rol Δ
Como **administrador**, quiero que cada rol vea las funciones designadas para él para evitar acciones no autorizadas.
*RF-05 (aplica a todas las pantallas)*

- **CA1.** Dado que inicio sesión como exportador, operador, aprobador o administrador, cuando veo el menú, entonces solo aparecen las funciones de mi columna en la matriz de permisos.
- **CA2.** Dado que escribo la dirección de una pantalla que no es de mi rol, cuando intento abrirla, entonces veo "Sin permiso" y no se muestra su contenido.

---

## Épica 2 — Solicitud del exportador

### HU-06 Iniciar una solicitud de factoring Δ
Como **exportador**, quiero iniciar una solicitud describiendo mi negocio para que el factor entienda mi operación.
*RF-07, RF-16, RF-44*

- **CA1.** Dado que inicié sesión, cuando elijo "Nueva solicitud", entonces veo el formulario con descripción del negocio, tipo de factoring (nacional o internacional), modalidad (con o sin recurso), facturas, comprador, documentos y declaraciones.
- **CA2.** Dado que la descripción del negocio, el tipo o la modalidad están vacíos, cuando intento enviar, entonces el sistema marca los campos como obligatorios.

### HU-07 Ingresar los datos de la factura Δ
Como **exportador**, quiero ingresar los datos de mi factura para que el factor sepa qué documento se va a descontar.
*RF-08*

- **CA1.** Dado el formulario de solicitud, cuando ingreso número de factura, fecha de emisión, monto, descripción del producto y plazo en días, entonces los datos quedan en la solicitud.
- **CA2 [P].** Dado que ingreso un monto igual o menor a cero, cuando avanzo, entonces el sistema lo rechaza con un mensaje.
- **CA3 [P].** Dado que ingreso una fecha de emisión futura, cuando avanzo, entonces el sistema la rechaza.
- **CA4 [P].** Dado que el plazo está vacío o es menor o igual a cero, cuando avanzo, entonces el sistema lo rechaza.

> El plazo se escribe libremente en días (cliente).

### HU-08 Ingresar los datos del comprador
Como **exportador**, quiero registrar a quién emití la factura para que el factor identifique al comprador.
*RF-10*

- **CA1.** Dado el formulario de solicitud, cuando ingreso nombre, dirección, ciudad, país, correo, teléfono e identificación tributaria del comprador, entonces los datos quedan en la solicitud.
- **CA2.** Dado que el correo del comprador no tiene formato válido, cuando avanzo, entonces el sistema marca el campo.

### HU-09 Adjuntar documentos Δ
Como **exportador**, quiero adjuntar la factura y otros documentos para respaldar mi solicitud.
*RF-11 · RNF-09*

- **CA1.** Dado un archivo PDF de hasta 20 MB, cuando lo adjunto, entonces aparece en la lista con su nombre.
- **CA2.** Dado un archivo que no es PDF o pesa más de 20 MB, cuando intento adjuntarlo, entonces el sistema no lo agrega y muestra "Solo PDF, máximo 20 MB".
- **CA3 [P].** Dado un archivo adjuntado, cuando lo quito antes de enviar, entonces desaparece de la lista.

### HU-10 Aceptar la declaración de datos y los términos
Como **exportador**, quiero aceptar la declaración de uso de datos y los términos del factor para continuar con mi solicitud de forma legal.
*RF-12 · RNF-03*

- **CA1.** Dado el formulario de solicitud, cuando no he marcado ambas aceptaciones, entonces el botón "Enviar" está deshabilitado.
- **CA2.** Dado el formulario de solicitud, cuando selecciono el enlace de cada texto, entonces puedo leerlo completo antes de aceptar.

### HU-11 Enviar la solicitud
Como **exportador**, quiero enviar mi solicitud completa para que el factor la revise.
*RF-13, RF-35 · RNF-06*

- **CA1.** Dado que completé todo y acepté las declaraciones, cuando envío, entonces la solicitud queda en estado "Registrada" y veo el mensaje "Solicitud enviada" con su número.
- **CA2.** Dado que falta un dato obligatorio, cuando envío, entonces no se envía y se marcan los campos faltantes.
- **CA3 [P].** Dado un exportador nuevo, cuando completa la solicitud en pruebas con al menos 5 usuarios, entonces tarda 10 minutos o menos, sin ayuda.

### HU-12 Consultar el estado de mis solicitudes
Como **exportador**, quiero ver el estado y el historial de mis solicitudes para saber en qué etapa están.
*RF-14, RF-35*

- **CA1.** Dado que inicié sesión, cuando abro "Mis solicitudes", entonces veo una lista con número, fecha, monto y estado.
- **CA2.** Dado que abro una solicitud, cuando miro su detalle, entonces veo los cambios de estado con fecha.
- **CA3.** Dado que hay solicitudes de otros exportadores, cuando consulto la lista, entonces solo aparecen las mías.

---

## Épica 3 — Revisión y aprobación

### HU-13 Ver la bandeja de solicitudes
Como **operador**, quiero ver las solicitudes recibidas para atenderlas.
*RF-17*

- **CA1 [P].** Dado que inicié sesión como operador, cuando abro la bandeja, entonces veo exportador, monto, fecha de recepción y estado, con las más antiguas primero.
- **CA2.** Dado una solicitud de la lista, cuando la abro, entonces veo sus datos, facturas y documentos.

### HU-14 Validar los documentos Δ
Como **operador**, quiero registrar el estado de cada documento (recibido, validado u observado) para controlar la documentación de la operación.
*RF-18*

- **CA1.** Dado una solicitud con documentos, cuando reviso uno, entonces puedo registrar su estado: recibido, validado u observado.
- **CA2 [P].** Dado que registro un documento como observado, cuando guardo, entonces debo escribir la observación.

### HU-15 Pedir documentos adicionales
Como **operador**, quiero pedir documentos o una justificación al exportador, desde la plataforma, para completar la revisión sin rechazar la operación.
*RF-19, RF-35*

- **CA1.** Dado una solicitud en revisión, cuando escribo el mensaje y lo envío, entonces la solicitud pasa a "Pendiente de documentos" y el exportador recibe una notificación.
- **CA2.** Dado una solicitud "Pendiente de documentos", cuando consulto su estado, entonces no aparece como rechazada.

> El exportador tiene hasta 10 días para responder. Si no responde, aplica RF-45 (Should, sin historia todavía).

### HU-16 Responder con los documentos pedidos
Como **exportador**, quiero cargar los documentos que me piden para que mi solicitud continúe.
*RF-20, RF-11, RF-35 · RNF-09*

- **CA1.** Dado que el operador pidió documentos, cuando abro mi solicitud, entonces veo su mensaje.
- **CA2.** Dado que adjunto los archivos (PDF, hasta 20 MB) y envío, cuando termina el envío, entonces la solicitud vuelve a "En revisión" y el operador ve los nuevos archivos.

### HU-17 Enviar la operación a aprobación
Como **operador**, quiero enviar la operación a aprobación cuando termino la revisión para que otra persona la autorice.
*RF-21, RF-35*

- **CA1.** Dado que todos los documentos están validados, cuando envío a aprobación, entonces el estado cambia a "En aprobación" y aparece en la bandeja del aprobador.
- **CA2 [P].** Dado que hay documentos observados sin resolver, cuando intento enviar a aprobación, entonces el sistema no lo permite y lo explica.

### HU-18 Aprobar o rechazar una operación Δ
Como **aprobador**, quiero aprobar o rechazar una operación y, si lo deseo, indicar el motivo para dejar constancia de la decisión.
*RF-23, RF-35*

- **CA1.** Dado una operación "En aprobación", cuando la apruebo, entonces el estado pasa a "Aprobada".
- **CA2.** Dado una operación "En aprobación", cuando la rechazo, entonces puedo escribir el motivo en texto libre (por ejemplo, "riesgo no aprobado").
- **CA3.** Dado que dejo el motivo vacío, cuando rechazo, entonces el sistema guarda el rechazo igualmente.

> El motivo es texto libre y opcional (cliente).

### HU-19 Recibir el resultado de mi solicitud Δ
Como **exportador**, quiero recibir el resultado de la aprobación para saber si puedo continuar.
*RF-24*

- **CA1.** Dado que el aprobador decidió, cuando se guarda la decisión, entonces recibo una notificación dentro del sistema con el resultado.
- **CA2.** Dado que la operación fue rechazada con motivo, cuando leo la notificación, entonces incluye el motivo.

> Notificación por correo o SMS: stand-by. Notificar al comprador cuando se aprueba es RF-15 (Should).

---

## Épica 4 — Contrato y endoso

### HU-20 Enviar el contrato y el endoso Δ
Como **operador o aprobador**, quiero enviar al exportador el contrato de factoring y el formato de endoso para formalizar la operación.
*RF-25, RF-35*

- **CA1.** Dado una operación "Aprobada", cuando envío los dos documentos, entonces el exportador los ve en su solicitud y recibe una notificación.
- **CA2.** Dado una operación que no está "Aprobada", cuando intento enviarlos, entonces el sistema no lo permite.

---

## Épica 5 — Preliquidación

### HU-21 Ver la preliquidación Δ
Como **operador o aprobador**, quiero que el sistema genere la preliquidación con los datos de la solicitud y las condiciones aprobadas para dejar constancia de los valores finales.
*RF-28*

- **CA1.** Dado una operación aprobada, cuando abro "Preliquidación", entonces veo valor de factura y plazo (tomados de la solicitud), % de anticipo, tasa de descuento, gastos y comisiones (condiciones aprobadas), y el cálculo de anticipo neto, descuento, saldo a reembolsar, total neto al exportador y fecha de pago.
- **CA2 [P].** Dado que el porcentaje de anticipo está fuera de 0 a 100, cuando se registran las condiciones, entonces el sistema lo rechaza.
- **CA3.** Dado que la preliquidación está generada, cuando el exportador abre su solicitud, entonces también la ve.

> No es un formulario que alguien llena (cliente). Cálculo con base 360 días y descuento sobre el anticipo (confirmado). Ejemplo numérico: sección E de `Requerimientos_v0.2.md`.

---

## Épica 6 — Mantenimientos

### HU-22 Administrar exportadores
Como **administrador**, quiero crear, consultar, modificar y desactivar exportadores para mantener actualizado el listado de clientes del factor.
*RF-30*

- **CA1.** Dado que estoy en "Exportadores", cuando creo uno con sus datos legales, entonces aparece en la lista como activo.
- **CA2.** Dado un exportador existente, cuando modifico sus datos y guardo, entonces la lista muestra los datos nuevos.
- **CA3.** Dado un exportador, cuando lo desactivo, entonces no puede crear nuevas solicitudes y su historial se conserva.

### HU-23 Administrar compradores
Como **administrador**, quiero crear, consultar, modificar y desactivar compradores para mantener actualizado el listado de importadores.
*RF-31*

- **CA1.** Dado que estoy en "Compradores", cuando creo uno con nombre, dirección, ciudad, país, correo, teléfono e identificación tributaria, entonces aparece en la lista como activo.
- **CA2.** Dado un comprador existente, cuando modifico sus datos y guardo, entonces la lista muestra los datos nuevos.
- **CA3.** Dado un comprador, cuando lo desactivo, entonces no se puede elegir en nuevas solicitudes y su historial se conserva.

---

## Épica 7 — Trazabilidad

### HU-24 Ver el historial de una operación
Como **operador, aprobador o administrador**, quiero ver el historial de cada operación para saber quién hizo cada cambio y cuándo.
*RF-35*

- **CA1.** Dado que cambia el estado de una operación, cuando se guarda el cambio, entonces el historial agrega usuario, fecha, hora, estado anterior y estado nuevo.
- **CA2 [P].** Dado el historial de una operación, cuando intento editar o borrar un registro, entonces el sistema no lo permite.

---

## Definición de Hecho para la maqueta [P]

Aplica a todas las historias (S05). Debe acordarla el equipo.
- Pantalla diseñada en Figma y enlazada en un prototipo navegable.
- Textos en español y en el vocabulario del cliente (exportador, factor, endoso, preliquidación).
- Revisada por otro integrante con la lista de calidad de la S06.
- Mostrada al cliente y sin observaciones pendientes.
- Se ve bien en pantalla de celular y en las dos últimas versiones de Chrome, Edge y Firefox (RNF-10).

---

## Mapa de historias (orden sugerido)

| Registrarse y entrar | Solicitar | Revisar | Aprobar | Formalizar | Administrar |
|---|---|---|---|---|---|
| HU-01 Registro | HU-06 Iniciar | HU-13 Bandeja | HU-17 Enviar a aprobación | HU-20 Contrato y endoso | HU-03 Crear usuarios |
| HU-02 Sesión | HU-07 Factura | HU-14 Validar documentos | HU-18 Aprobar o rechazar | HU-21 Preliquidación | HU-04 Desactivar usuarios |
| HU-05 Permisos | HU-08 Comprador | HU-15 Pedir documentos | HU-19 Recibir resultado | | HU-22 Exportadores |
| | HU-09 Adjuntos | HU-16 Responder | | | HU-23 Compradores |
| | HU-10 Declaraciones | | | | HU-24 Historial |
| | HU-11 Enviar | | | | |
| | HU-12 Estado | | | | |

**Primera versión recorrible de punta a punta:** HU-01, 02, 05, 06 a 12, 13 a 19, 20 y 21. Administrar entra después, salvo HU-03, que se necesita para crear a los usuarios internos.

---

## Matriz de trazabilidad

### Requerimientos funcionales Must → historias

| RF | Historias | Nota |
|---|---|---|
| RF-01 | HU-01 | Comparte historia con RF-02 |
| RF-02 | HU-01 | Incluye aceptación de datos |
| RF-03 | HU-02 | |
| RF-04 | HU-03, HU-04 | Dividido por operación |
| RF-05 | HU-05 | Aplica a todas las pantallas |
| RF-07 | HU-06 | |
| RF-08 | HU-07 | Incluye plazo |
| RF-10 | HU-08 | |
| RF-11 | HU-09, HU-16 | Adjuntar en la solicitud y al responder al operador |
| RF-12 | HU-10 | |
| RF-13 | HU-11 | |
| RF-14 | HU-12 | |
| RF-16 Δ | HU-06 | Subió a Must |
| RF-17 | HU-13 | |
| RF-18 | HU-14 | |
| RF-19 | HU-15 | |
| RF-20 | HU-16 | |
| RF-21 | HU-17 | |
| RF-23 | HU-18 | |
| RF-24 | HU-19 | |
| RF-25 | HU-20 | |
| RF-28 | HU-21 | Absorbe RF-29 |
| RF-30 | HU-22 | |
| RF-31 | HU-23 | |
| RF-35 | HU-24 (principal), HU-11, HU-12, HU-15, HU-16, HU-17, HU-18, HU-20 | Cada cambio de estado queda en el historial |
| RF-44 Δ | HU-06 | Nuevo |

Los 26 Must tienen al menos una historia. Los 19 requerimientos vigentes Should, Could y Won't no tienen historia todavía (incluye RF-45 y RF-46).

### Requerimientos no funcionales → historias

| RNF | Prior. | Historias | Nota |
|---|---|---|---|
| RNF-01 Nube u on-premise | M | — | Restricción de despliegue. No genera pantalla. |
| RNF-02 Enlazable desde el sitio del factor | S | — | Sin historia (Should). |
| RNF-03 Consentimiento (LOPDP) | M | HU-01, HU-10 | Al registrarse y al enviar cada solicitud. |
| RNF-04 Ente de control configurable | M | — | Se ve en la pantalla de datos del factor (RF-32, Should). Controles comunes cubiertos por HU-10, HU-24 y RF-22. |
| RNF-05 Seguridad de acceso | M | HU-02 | Aceptado por el cliente. |
| RNF-06 Usabilidad | M | HU-11 | CA3 |
| RNF-07 Rendimiento | S | — | Sin historia (Should). |
| RNF-08 Disponibilidad | S | — | Sin historia (Should). |
| RNF-09 Archivos adjuntos | M | HU-09, HU-16 | Solo PDF, hasta 20 MB. |
| RNF-10 Compatibilidad | S | Definición de Hecho | Global. |

---

## Revisión INVEST

- **Valiosa, testeable, negociable:** todas tienen beneficio y criterios verificables.
- **Independiente:** HU-11 necesita HU-06 a 10. HU-16 necesita HU-15. HU-17 necesita HU-14. HU-20 y 21 necesitan HU-18. El mapa las ordena.
- **Pequeña:** HU-22 y HU-23 juntan cuatro operaciones cada una. Se dividen si el equipo las estima grandes.
- **Estimable:** todas las historias Must tienen sus reglas definidas.

## Pendientes

- Validar con el equipo las reglas **[P]** restantes y la Definición de Hecho.
- Redactar historias Should prioritarias si entran en la maqueta: RF-15 (aviso al comprador), RF-37 (reportes), RF-45 (baja automática a los 10 días).
- Estados de la operación: usar la lista de la sección 2-H de `Requerimientos_v0.2.md`.
