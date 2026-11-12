# Sistema de Gestión de Factoring — Maqueta

Proyecto de **Ingeniería de Software I** · ESPOL · PAO II 2026

Este repositorio reúne las evidencias del levantamiento de requerimientos, la metodología que seguimos y el prototipo aprobado del sistema.

| | |
|---|---|
| **Cliente** | Royal Technology S.A. |
| **Experto del dominio y validador** | Moisés Luque (ML Consulting) |
| **Profesora** | Vanessa Alexandra Jurado Vite |
| **Alcance** | Solo maqueta frontend. No hay backend real. Las notificaciones y la firma digital se simulan en pantalla. |

## Equipo

- Navarrete Seme Jeycop David
- Verdesoto Franco Victor Alejandro
- Chung Velastegui Kenny Noe
- Falconi Ortiz Valentina Daniela
- Medina Luna Miguel Angel

## Enlaces

- **Prototipo en Figma (flujo principal v0.1):** https://www.figma.com/design/XuY8VA5iAG5RQ6DJ0ywe5q/Flujo-principal-V0.1
- **Documento de especificación de requerimientos (SRS):** [`SRS/SRS_Factoring_v1.4.pdf`](SRS/SRS_Factoring_v1.4.pdf)

## Contenido del repositorio

| Carpeta | Contenido |
|---|---|
| [`SRS/`](SRS/) | Documento de especificación de requerimientos en PDF (en inglés). Incluye el acta de conformidad firmada por el cliente (Apéndice F). |
| [`docs/`](docs/) | Requerimientos v0.2 e historias de usuario Must v0.2, ya validados por el cliente. |
| [`Excel/`](Excel/) | Matriz de validación de requerimientos v0.2 e historias de usuario v0.1. |
| [`Reuniones/`](Reuniones/) | Transcripciones de las tres reuniones con el cliente (Microsoft Teams). |
| [`Evidencias/`](Evidencias/) | Capturas de las reuniones y de la observación etnográfica. |
| [`Documentos_del_cliente/`](Documentos_del_cliente/) | Material que entregó el cliente: presentación "Factoring" y descripción del proyecto de Royal Technology. |
| [`Capturas/`](Capturas/) | Capturas de las 24 pantallas del prototipo (P01 a P15b). |
| [`Prototipo/`](Prototipo/) | Video del recorrido del flujo principal. |

## Levantamiento de requerimientos

| Técnica | Qué hicimos | Evidencia |
|---|---|---|
| **Entrevistas** | 16-oct-2026 con Moisés Luque (ML Consulting): proceso de factoring, actores, documentos, revisión y aprobación.<br>26-oct-2026 con Stalin De La Torre (Royal Technology): modelo de negocio, datos maestros, validación de documentos, contrato y preliquidación. | `Reuniones/`, `Evidencias/` |
| **Etnografía** | 16-oct-2026. Observamos los sitios web de las empresas de factoring de la diapositiva 6 de la presentación del cliente: qué datos y documentos piden al exportador y cómo explican las condiciones. | `Evidencias/` |
| **Análisis de documentos** | Revisamos la presentación "Factoring" del cliente y la descripción del proyecto de Royal Technology. | `Documentos_del_cliente/` |
| **Prototipado** | Confirmamos el flujo de pantallas y el vocabulario con el cliente usando la maqueta en Figma. | Figma, `Capturas/`, `Prototipo/` |
| **Validación** | 10-nov-2026: revisamos cada requerimiento con el experto del dominio. El resultado es la versión 0.2. | `Reuniones/Revisión de requerimientos.vtt`, `docs/` |

## Metodología

- **Proceso:** enfoque ágil basado en Scrum, con 5 sprints. Cada sprint agrupa historias relacionadas:
  1. Cuentas y acceso
  2. Solicitud del exportador
  3. Revisión
  4. Aprobación y contrato
  5. Datos maestros
- **Priorización:** MoSCoW. Los requerimientos Must son el 56.5 % del total (meta: menos del 60 %).
- **Especificación:** las historias de usuario Must tienen criterios de aceptación en formato *Dado / Cuando / Entonces*. Los requerimientos no funcionales están clasificados según Ian Sommerville y cada uno tiene su criterio de validación.
- **Planificación:** estimación por historia en días laborables, red de actividades (AoA) con ruta crítica de 26 días, e histogramas de recursos sin suavizar y suavizado. El detalle está en el capítulo 5 del SRS.

**Definición de Hecho.** Una historia está terminada cuando:

- la pantalla está en Figma y enlazada en el prototipo navegable;
- los textos están en español y usan el vocabulario del cliente;
- otro integrante la revisó;
- se mostró al cliente y no tiene observaciones;
- se adapta a celular y funciona en las dos últimas versiones de Chrome, Edge y Firefox.

## Prototipo

El flujo de la operación es:

**Registrada → En revisión → (Pendiente de documentos ↔ En revisión) → En aprobación → Aprobada / Rechazada → Contrato enviado → Firmada**

Si el exportador no responde un pedido de documentos en 10 días, la operación pasa a *Dada de baja*.

| Rol | Pantallas |
|---|---|
| Todos | P01 Login · P03 Sin permiso · P11 Notificaciones |
| Exportador | P02 Registro · P04 Mis solicitudes · P05 Nueva solicitud (4 pasos) · P06 Solicitud enviada · P07 Detalle · P07b Responder pedido de documentos |
| Operador | P08 Bandeja · P09 Detalle · P13 Enviar contrato y endoso |
| Aprobador | P08 Bandeja · P10 Detalle · P10b Aprobar · P10c Rechazar · P13 Enviar contrato y endoso |
| Administrador | P12 Usuarios internos · P12b Nuevo usuario · P14 Exportadores · P14b Nuevo exportador · P15 Compradores · P15b Nuevo comprador |

**Caso de prueba de la preliquidación.** Factura de USD 10,000 a 30 días, anticipo del 80 %, gastos de USD 205 y tasa anual de 16.75 %, con base de 360 días:

| Concepto | Monto |
|---|---|
| Anticipo neto | USD 7,795.00 |
| Descuento | USD 111.67 |
| Reembolso | USD 1,888.33 |
| **Total neto al exportador** | **USD 9,683.33** |
