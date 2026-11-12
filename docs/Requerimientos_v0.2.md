# Sistema de Gestión de Factoring — Requerimientos (v0.2)

Estado: **revisado con el cliente** (reunión de revisión de requerimientos, Moisés Luque, 10-nov-2026). Pendientes confirmados el mismo día (CC = confirmación del cliente). Alcance del semestre: **maqueta (frontend)**.
Versión anterior: `Requerimientos_iniciales_v0.1.md`. Excel equivalente: `Gestion_Factoring_Validacion_v0.2.xlsx`.

**Fuentes**
- R1 = Reunión 1 (Moisés Luque, ML Consulting)
- R2 = Reunión 2 (Stalin De La Torre, Royal Technology)
- RV = Reunión de revisión de requerimientos (Moisés Luque)
- PDF-RT = Proyectos de Software Royal Technology
- PDF-F = Factoring Internacional (6.16.2026)
- DESC = descripción del proyecto
- EQ = decisión del equipo

**Prioridad (MoSCoW):** M = Must, S = Should, C = Could, W = Won't (esta entrega).
**[P]** = valor propuesto por el equipo. El cliente no lo dio o lo aceptó sin cifra.
**Δ v0.2** = cambiado o agregado en esta versión.

---

## 0. Cambios respecto a v0.1

| Elemento | Cambio | Origen |
|---|---|---|
| RF-05 | "limitar" → "designar" las funciones visibles por rol. | RV |
| RF-08 | Se agregó el plazo del factoring en días. | RV |
| RF-15 | Al comprador se le notifica solo después de aprobada la operación. Si se rechaza, no. | RV |
| RF-16 | Modalidad con/sin recurso: S → M. Es dato de la solicitud. | RV |
| RF-18 | "marcar" → "registrar el estado" del documento. | RV |
| RF-23, RF-24 | El motivo de rechazo es opcional. | RV |
| RF-25 | Envían operador o aprobador, después de la aprobación. | RV |
| RF-28, RF-29 | Fusionados en la **preliquidación**. RF-29 queda retirado. | RV |
| RF-37 | Reportes con conteos por estado y período. | RV |
| RF-44 | Nuevo (M): tipo de factoring nacional o internacional. | RV |
| RF-45 | Nuevo (S): alerta y baja automática si el exportador no responde. | RV |
| RF-46 | Nuevo (C): el administrador ve todas las solicitudes. | RV |
| RNF-01 | Despliegue en nube u on-premise. La nube es la preferida. | RV |
| RNF-09 | Solo PDF, máximo 20 MB. | CC |
| RF-08 | Plazo libre en días. | CC |
| RF-45 | Plazo de respuesta: 10 días. | CC |
| RF-23 | Motivo de rechazo en texto libre, opcional. | CC |
| RNF-03 / RF-02 | El registro también exige aceptar la declaración de datos. | CC |
| Sección 2-H | Lista de estados de la operación. | CC |
| RNF-04 | El sistema admite factores de ambas superintendencias; el ente de control se configura por factor. | EQ, CC |
| RF-32 | Los datos del factor incluyen el ente de control. | EQ |
| RF-47 | Nuevo (W): reportes regulatorios propios de cada superintendencia. | EQ |

---

## 1. Interesados

| Interesado | Rol en el sistema | Fuente |
|---|---|---|
| Exportador (persona natural o jurídica) | Usuario externo. Crea su propia cuenta (una cuenta = un usuario), registra la solicitud, sube documentos, firma. | R1, RV, CC |
| Operador (back office del factor) | Usuario interno. Recibe y procesa solicitudes. Envía contrato y endoso. | R1, RV |
| Aprobador / autorizador | Usuario interno. Aprueba o rechaza (cuatro ojos). También puede enviar contrato y endoso. | R1, RV |
| Administrador de la plataforma | Usuario interno del factor. Gestiona usuarios internos y mantenimientos. No crea cuentas de exportadores. | R1, RV |
| Comprador / importador | **No es usuario.** Solo recibe notificación si la operación se aprueba. | R1, RV |
| Empresa factor o banco | Cliente que usa el software. Puede estar controlado por la Superintendencia de Bancos (factoring financiero) o por la de Compañías, Valores y Seguros (factoring comercial). | R1, R2, EQ |
| Royal Technology (Stalin De La Torre) | Vende o renta el software con licencia a varios factores. | R2 |
| Moisés Luque (ML Consulting) | Experto del dominio. Valida los requerimientos. | R1, RV |

---

## 2. Requerimientos funcionales

### A. Cuentas y acceso

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-01 | El sistema debe permitir al exportador crear una cuenta con usuario y contraseña. | M | R1, RV |
| RF-02 Δ | El sistema debe registrar, al crear la cuenta, nombre legal, cédula o RUC, domicilio legal, correo electrónico y código postal del exportador, previa aceptación de la declaración de uso de datos. | M | R1, RV, CC |
| RF-03 | El sistema debe permitir iniciar sesión con usuario y contraseña. | M | R1, RV |
| RF-04 | El administrador debe poder crear, desactivar y asignar rol a usuarios internos del factor (operador, aprobador, administrador). | M | R1, DESC, RV |
| RF-05 Δ | El sistema debe **designar** las funciones visibles según el rol (exportador, operador, aprobador, administrador). | M | R1, DESC, RV |
| RF-06 | El sistema debería permitir el ingreso desde el sitio web del factor mediante inicio de sesión único (SSO). | W | R1, RV |

> RF-01: el cliente preguntó por un código de verificación al crear la cuenta. Se acordó dejarlo para una fase futura (RV).
> Cada exportador tiene un solo usuario. Varios usuarios por empresa no aportan valor según el cliente (CC).

### B. Solicitud del exportador

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-07 | El exportador debe poder crear una solicitud de operación de factoring con la descripción de su negocio. | M | R1, RV |
| RF-08 Δ | El exportador debe ingresar por factura: número, fecha de emisión, monto, descripción del producto y **plazo del factoring en días**, escrito libremente (p. ej. 30, 45, 60, 90). | M | R1, RV, CC |
| RF-09 | El exportador debería poder incluir varias facturas en una misma solicitud. | S | R1, RV |
| RF-10 | El exportador debe ingresar los datos del comprador: nombre, dirección, ciudad, país, correo, teléfono e identificación tributaria. | M | R1, RV |
| RF-11 | El exportador debe poder adjuntar la factura y otros documentos (PDF u otro formato permitido). | M | R1, RV |
| RF-12 | El sistema debe exigir aceptar la declaración de uso de datos y los términos y condiciones del factor antes de enviar. | M | R1, RV |
| RF-13 | El exportador debe poder enviar la solicitud y ver un mensaje de confirmación ("Solicitud enviada"). | M | R1, RV |
| RF-14 | El exportador debe poder consultar el estado y el historial de sus solicitudes. | M | DESC, R1, RV |
| RF-15 Δ | El sistema debería notificar al comprador, **solo cuando el factor aprueba la operación**, que el exportador solicitó factoring sobre su factura. Si se rechaza, el comprador no es notificado. | S | R1, RV |
| RF-16 Δ | La solicitud debe indicar la modalidad: con recurso o sin recurso. | **M** | R2, PDF-F, RV |
| RF-44 Δ | La solicitud debe indicar el tipo de factoring: nacional (local) o internacional. | M | RV |

> RF-07 abre el formulario. RF-08, RF-09, RF-10, RF-11, RF-16 y RF-44 son los datos que se ingresan en él (RV).
> RF-15: el cliente aceptó posponer la notificación al comprador si complica la maqueta (p. ej. hasta tener el endoso).

### C. Revisión y aprobación (back office)

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-17 | El operador debe ver una bandeja con las solicitudes recibidas. | M | R1, RV |
| RF-18 Δ | El operador debe poder **registrar el estado** de cada documento: recibido, validado u observado. | M | R2, PDF-F, RV |
| RF-19 | El operador debe poder pedir al exportador documentos adicionales o una justificación, desde la plataforma. | M | R1, RV |
| RF-20 | El exportador debe poder responder esa solicitud cargando documentos. | M | R1, RV |
| RF-45 Δ | El exportador tiene hasta 10 días para responder un pedido de documentos. El sistema debería enviarle una alerta antes de que venza el plazo (al día 7 **[P]**) y, si al día 10 no responde, dar de baja la solicitud automáticamente. | S | RV, CC |
| RF-21 | El operador debe poder enviar la operación a aprobación. | M | R1, RV |
| RF-22 | El sistema debería impedir que el mismo usuario procese y apruebe una operación (cuatro ojos). | S | R1, RV |
| RF-23 Δ | El aprobador debe poder aprobar o rechazar una operación e ingresar **opcionalmente** el motivo en texto libre. | M | R1, RV, CC |
| RF-24 Δ | El sistema debe notificar al exportador el resultado de la aprobación (aprobada o rechazada) y el motivo del rechazo si se ingresó. | M | R1, RV |

> Pedir un documento adicional **no** es rechazar. La operación queda "Pendiente de documentos" (R1).
> RF-18 es una tarea interna del factor. El sistema solo cambia el estado del documento (RV).
> RF-45: la baja automática debe constar en el contrato de factoring (RV).
> Notificaciones: en la maqueta son mensajes dentro del sistema. Correo o SMS quedan en stand-by. Siempre debe existir una notificación (RV).

### D. Contrato y endoso

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-25 Δ | El operador o el aprobador debe poder enviar al exportador, una vez aprobada la operación, el contrato de factoring y el formato de endoso de la factura. | M | R1, RV |
| RF-26 | El exportador debería poder firmar ambos documentos de forma digital. En la maqueta será una pantalla simulada. | S | R1, RV |
| RF-27 | El sistema debería registrar los contratos y endosos asociados a cada operación. | S | R2, RV |

### E. Preliquidación

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-28 Δ | El sistema debe generar y mostrar la **preliquidación** de la operación con los datos ingresados por el exportador y las condiciones aprobadas por el factor: valor de factura, % de anticipo, tasa de descuento, plazo, gastos, comisiones, anticipo neto, descuento, saldo a reembolsar, total neto al exportador y fecha de pago. | M | R2, PDF-F, RV |
| RF-29 Δ | *(Retirado. Fusionado en RF-28.)* | — | RV |

> No es un formulario que alguien llena. El sistema arma la preliquidación con lo que ingresó el exportador y lo que aprobó el factor (RV).

Ejemplo de aceptación para RF-28 (PDF-F, p. 7). Base de 360 días y descuento sobre el anticipo, confirmados por el cliente (CC).
- Factura USD 10,000. Plazo 30 días. Anticipo 80 % = USD 8,000. Gastos USD 205. Tasa 16.75 % anual.
- Anticipo neto = 8,000 − 205 = **USD 7,795.00**
- Descuento = 8,000 × 16.75 % × 30/360 = **USD 111.67**
- Reembolso = 2,000 − 111.67 = **USD 1,888.33**
- Total neto al exportador = **USD 9,683.33**

### F. Mantenimientos

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-30 | El administrador debe poder crear, consultar, modificar y desactivar exportadores. | M | R2, RV |
| RF-31 | El administrador debe poder crear, consultar, modificar y desactivar compradores. | M | R2, RV |
| RF-32 Δ | El administrador debería poder configurar los datos de la empresa factor, incluido su ente de control (Superintendencia de Bancos o Superintendencia de Compañías, Valores y Seguros). | S | R2, RV, EQ |
| RF-33 | El administrador debería poder definir los tipos de documento a validar. | S | R2, RV |
| RF-34 | El administrador podría definir plantillas de contrato y tipos de endoso. | C | R2, RV |
| RF-46 Δ | El administrador podría consultar todas las solicitudes registradas. | C | RV |

### G. Trazabilidad, auditoría y reportes

| ID | Requerimiento | Prior. | Fuente |
|---|---|---|---|
| RF-35 | El sistema debe registrar el estado de cada operación y su historial (usuario, fecha y hora de cada cambio). | M | DESC, R1, RV |
| RF-36 | El administrador debería poder consultar un registro de auditoría de acciones. | S | DESC, RV |
| RF-37 Δ | El sistema debería mostrar reportes estadísticos de solicitudes por estado (ingresadas, en proceso, aprobadas, rechazadas) por período (mes, 6 meses, año), con gráficos. | S | PDF-F, RV |
| RF-38 | El sistema podría mostrar reportes ejecutivos de cartera, desembolsos y cobranza. | C | DESC, PDF-F, RV |
| RF-39 | El sistema podría gestionar cupos o líneas aprobadas por exportador. | C | DESC, PDF-F, RV |
| RF-40 | Reportes de riesgo. | W | DESC, RV |
| RF-41 | Integración bancaria y desembolso automático. | W | DESC, PDF-F, RV |
| RF-42 | Operación multiempresa (un sistema para varios factores con licencia). | W | R2, RV |
| RF-43 | Análisis de riesgo automático (motor o agente de IA). | W | R1, R2, RV |
| RF-47 Δ | Reportes regulatorios propios de cada superintendencia (p. ej. estructuras de datos de la Superintendencia de Bancos). | W | EQ |

> RF-37: los gráficos son opcionales (RV).
> RF-43: confirmado que el análisis de riesgo lo hace el factor internamente o en otra plataforma (RV).

### H. Estados de la operación (CC)

El cliente delegó la lista al equipo. Se usa en la bandeja, el historial (RF-35) y los reportes (RF-37).

| Estado | Significado | Pasa a |
|---|---|---|
| Registrada | El exportador envió la solicitud. | En revisión |
| En revisión | El operador revisa datos y documentos. | Pendiente de documentos, En aprobación |
| Pendiente de documentos | El operador pidió documentos o justificación. Corre el plazo de 10 días. | En revisión, Dada de baja |
| En aprobación | Espera la decisión del aprobador. | Aprobada, Rechazada |
| Aprobada | El factor aprobó. Se genera la preliquidación y se avisa al comprador (RF-15). | Contrato enviado |
| Rechazada | El factor rechazó. Estado final. | — |
| Contrato enviado | El exportador recibió contrato y endoso. | Firmada |
| Firmada | El exportador firmó ambos documentos. Estado final de la maqueta. | — |
| Dada de baja | Venció el plazo de 10 días sin respuesta (RF-45). Estado final. | — |

**Totales:** 47 IDs, 46 vigentes (RF-29 retirado). Must 26 (57 %), Should 10, Could 4, Won't 6. Los Must siguen bajo el 60 % que sugiere S05.

---

## 3. Requerimientos no funcionales

| ID | Requerimiento | Tipo (Sommerville) | Prior. | Fuente |
|---|---|---|---|---|
| RNF-01 Δ | El sistema debe permitir su despliegue en la nube o en servidores propios (on-premise). La nube es la opción preferida. | Organización · entorno | M | R1, DESC, RV |
| RNF-02 | El sistema debería poder enlazarse o embeberse desde el sitio web del factor. | Organización · operacional | S | R1, RV |
| RNF-03 Δ | El sistema debe pedir consentimiento explícito antes de guardar datos personales, conforme a la Ley Orgánica de Protección de Datos Personales: al crear la cuenta y al enviar cada solicitud. | Externo · legal | M | R1, RV, CC |
| RNF-04 Δ | El sistema debe permitir operar a factores controlados por la Superintendencia de Bancos o por la Superintendencia de Compañías, Valores y Seguros. El ente de control se configura por empresa factor (RF-32). | Externo · regulatorio | M | PDF-F, EQ, CC |
| RNF-05 | El sistema debe guardar las contraseñas cifradas y bloquear la cuenta 15 min tras 5 intentos fallidos. **[P]** aceptado por el cliente. | Producto · seguridad | M | DESC, S03, RV |
| RNF-06 | Un exportador nuevo debe completar una solicitud en 10 min o menos, sin ayuda, en pruebas con al menos 5 usuarios. **[P]** | Producto · usabilidad | M | R1, RV |
| RNF-07 | Los listados deben cargar en menos de 3 s para el 95 % de las consultas. **[P]** | Producto · eficiencia | S | RV |
| RNF-08 | El sistema debe estar disponible el 99.5 % del tiempo en horario laboral, medido cada mes. **[P]** | Producto · confiabilidad | S | RV |
| RNF-09 Δ | Los archivos adjuntos deben ser PDF de hasta 20 MB cada uno. | Producto · eficiencia | M | R1, RV, CC |
| RNF-10 | La interfaz debe funcionar en las dos últimas versiones de Chrome, Edge y Firefox, y adaptarse a pantalla de celular. **[P]** | Organización · entorno | S | RV |

> RNF-04: los controles comunes a ambas superintendencias ya están cubiertos por RF-22, RF-27, RF-35, RF-36 y RNF-03. Los controles específicos de cada una son tema legal y quedan fuera de la maqueta (RF-47). Fuente de la distinción: Balladares, *La regulación de las compañías de factoring en Ecuador*, USFQ, 2023.
> RNF-05: el cliente indicó que se pueden usar los valores comunes de otras plataformas (RV).

---

## 4. Restricciones y supuestos

- Entregable del semestre: solo maqueta frontend (DESC). Firma digital y notificaciones se simulan en pantalla (RV).
- El proceso base cubre registro de intervinientes, solicitud, revisión, aprobación, contrato, endoso y preliquidación. El proceso termina en la preliquidación (R2, RV).
- El análisis de riesgo **no** se automatiza. El factor lo hace en otros sistemas (R1, R2, RV).
- Casi toda la interacción es exportador ↔ factor. El comprador solo recibe notificación si se aprueba la operación (R1, RV).
- El flujo es estándar para factoring nacional e internacional (R1, RV).
- El orden de los requerimientos no es el orden del flujo (RV).
- Código de verificación en el registro y notificaciones por correo/SMS: fase futura (RV).

---

## 5. Preguntas abiertas

### Resueltas en RV

| # (v0.1) | Tema | Resolución |
|---|---|---|
| 1 | Riesgo | Fuera del sistema. Lo hace el factor (RF-40, RF-43 en W). |
| 2 | Cupos / líneas | Se mantienen en C (RF-39). El cliente lo aceptó. |
| 3 | Nacional o internacional | Ambos. Nuevo RF-44. |
| 4 | Reportes | Conteos de solicitudes por estado y período, gráficos opcionales (RF-37). |
| 9 | Firma digital | Se simula en la maqueta (RF-26). |

### Confirmadas por el cliente (CC)

| # | Tema | Resolución |
|---|---|---|
| 5 | Usuarios del exportador | Una cuenta = un usuario. |
| 6 | Estados | Lista definida por el equipo (sección 2-H). |
| 7 | Archivos | Solo PDF, hasta 20 MB (RNF-09). |
| 8 | Cálculo | Base 360 días, descuento sobre el anticipo. |
| 11 | Plazo | Libre, en días (RF-08). |
| 12 | Baja automática | 10 días (RF-45). Alerta al día 7 [P]. |
| 13 | Motivos de rechazo | Texto libre, opcional (RF-23). |
| — | Consentimiento en el registro | Sí, se exige al crear la cuenta (RF-02, RNF-03). |
| 10 | Regulación | Se admiten ambas superintendencias como parámetro del factor (RNF-04, RF-32). Propuesta del equipo aceptada por el cliente. |

### Pendientes

Ninguna. Todos los requerimientos están validados por el cliente.

---

## 6. Verificación contra la lista de calidad (S06)

- **Singular, priorizado, trazable:** todos los RF y RNF tienen una idea, prioridad y fuente. RF-28 agrupa cálculo y presentación de la preliquidación, a pedido del cliente.
- **Verificable:** RF-28 tiene ejemplo numérico. RNF-05 a RNF-10 y RF-45 tienen métrica. RNF-04 se verifica con el selector de ente de control.
- **Consistente:** se resolvieron los conflictos de riesgo, cupos y nacional/internacional.
- **Completo:** no quedan preguntas abiertas. Todo validado por el cliente.

## 7. Siguiente paso

Construir las pantallas de la maqueta a partir de las historias Must (`Historias_de_usuario_Must_v0.2.md`) y presentarlas al cliente.
