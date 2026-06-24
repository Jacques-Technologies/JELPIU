# Progra Handoff — Jelpiu
**Sesión:** Jelpiu - Recorrido de pantallas  
**Grabada por:** Naomi Jardon · 24 Jun 2026  
**Fuente:** app.fireflies.ai/view/Jelpiu-Recorrido-de-pantallas::01KVXNH1PJHA0V5861Y6WY6YSD

> **Nota para el diseñador:** Los códigos de flujo (ej. `C-01`, `I-03`) deben aparecer como etiquetas o títulos en los frames correspondientes de Pencil. Esto permite al desarrollador identificar inequívocamente qué frame corresponde a qué especificación.

---

## Índice de flujos

### CRM (C)
- `C-01` Tablero de prospectos (estado vacío y listado)
- `C-02` Crear prospecto
- `C-03` Revisar / editar prospecto
- `C-04` Gestionar documentos de prospecto
- `C-05` Convertir prospecto a proyecto

### Proyectos (P)
- `P-01` Listado de proyectos
- `P-02` Crear proyecto
- `P-03` Detalle de proyecto
- `P-04` Descargable proyectos (XLS)

### Ingresos (I)
- `I-01` Listado de ingresos
- `I-02` Crear ingreso
- `I-03` Registrar abono
- `I-04` Revisar / editar ingreso
- `I-05` Cancelar ingreso
- `I-06` Marca automática de atrasado
- `I-07` Descargable ingresos (XLS)

### Gastos (G)
- `G-01` Listado de gastos
- `G-02` Crear gasto
- `G-03` Cambio de estado manual
- `G-04` Revisar / editar gasto
- `G-05` Cancelar gasto
- `G-06` Descargable gastos (XLS)

### Nóminas (N)
- `N-01` Listado de nóminas
- `N-02` Crear nómina
- `N-03` Revisar / editar nómina
- `N-04` Cancelar nómina
- `N-05` Descargable nóminas (XLS)

### Comisiones (K)
- `K-01` Listado de comisiones
- `K-02` Crear comisión
- `K-03` Revisar / editar comisión
- `K-04` Cancelar comisión
- `K-05` Descargable comisiones (XLS)

### Ajustes (A)
- `A-01` Gestión de clientes
- `A-02` Gestión de razones sociales
- `A-03` Gestión de proveedores
- `A-04` Gestión de usuarios y permisos

### Reporte gerencial (R)
- `R-01` Visualizar reporte consolidado

---

## CRM (C)

## C-01 · Tablero de prospectos

**Actor:** Usuario admin  
Pantalla principal del módulo CRM. Muestra el tablero Kanban con los prospectos organizados en sus fases. Si no hay prospectos, muestra estado vacío.

### Paso a paso
1. El usuario accede al módulo CRM
2. Ve el tablero Kanban con las cinco fases
3. Puede filtrar prospectos con los controles superiores
4. Puede hacer clic en una card para ver su detalle
5. Puede arrastrar una card entre fases (drag and drop)

### Campos (columnas de la card)
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del prospecto | Texto | solo lectura |
| Responsable | Texto | solo lectura |
| Fase de venta | Etiqueta | solo lectura |

### Filtros de lista
- **Nombre del prospecto** · _fijo_ — Searchbox de texto libre
- **Responsable** · _dinámico_ — Dropdown, valores desde tabla Usuarios de la plataforma
- **Fecha de registro** · _fijo_ — Rango de fechas: desde / hasta, formato DD-MMM-YYYY

### Notas para programación
1. Las cinco fases son: Idea, Contactado, En consideración, Aceptado, Rechazado. Son valores fijos del sistema.
2. El drag and drop entre columnas actualiza la fase del prospecto en tiempo real.
3. El cambio de fase también puede hacerse manualmente desde el detalle del prospecto.

---

## C-02 · Crear prospecto

**Actor:** Usuario admin  
El usuario registra un nuevo prospecto en la plataforma. Al guardar, el prospecto aparece en la fase Idea del tablero.

### Paso a paso
1. Hace clic en "Nuevo prospecto" desde el tablero
2. Llena los datos del prospecto en el formulario (tres secciones: Datos del prospecto, Contacto, Documentos)
3. Hace clic en "Guardar" para crear el prospecto, "Convertir a proyecto" para convertirlo directamente, o "Cancelar" para descartar

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del prospecto | Texto libre | obligatorio |
| Fase de venta | Dropdown (5 opciones) | obligatorio — default: Idea |
| Responsable | Dropdown usuarios | opcional |
| Ubicación | Texto libre | opcional |
| Giro | Texto libre | opcional |
| Origen de contacto | Texto libre | opcional |
| Servicio de interés | Texto libre | opcional |
| Fecha de primer contacto | Fecha DD-MMM-YYYY | opcional |
| Presentación de credenciales | Fecha DD-MMM-YYYY | opcional |
| Cierre estimado | Fecha DD-MMM-YYYY | opcional |
| Nombre de contacto | Texto libre | opcional |
| Correo electrónico | Texto libre (email) | opcional |
| Teléfono | Solo números | opcional |

### Notas para programación
1. Al guardar aparece un modal de confirmación "Prospecto creado en la fase Idea" con opciones: "Ver prospecto" o "Cerrar".
2. La fase default al crear es siempre Idea, independientemente del estado del pipeline.
3. La sección Documentos en el formulario de creación permite subir archivos, pero puede estar vacía.

---

## C-03 · Revisar / editar prospecto

**Actor:** Usuario admin  
El usuario abre el detalle de un prospecto existente para revisar o editar su información.

### Paso a paso
1. Hace clic en la card del prospecto en el tablero
2. Se abre el detalle con dos tabs: Datos y Documentos
3. La tab Datos muestra todos los campos capturados, editables
4. Modifica los campos que necesite
5. Hace clic en "Guardar" para confirmar los cambios

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Todos los campos de C-02 | — | editables |
| Fase de venta | Dropdown | editable — permite cambio manual de fase |

### Notas para programación
1. El nombre del prospecto y su fase actual se muestran en el header del modal.
2. Cambiar la fase desde el detalle actualiza la posición de la card en el tablero Kanban.

---

## C-04 · Gestionar documentos de prospecto

**Actor:** Usuario admin  
El usuario sube, lista, descarga o elimina documentos asociados a un prospecto.

### Paso a paso
1. Abre el detalle del prospecto (C-03) y hace clic en la tab "Documentos"
2. Ve el listado de documentos subidos (o empty state si no hay ninguno)
3. Para subir: hace clic en "Agregar documento", captura el nombre y selecciona/arrastra el archivo
4. Para descargar: hace clic en el ícono de descarga del documento
5. Para eliminar: hace clic en el ícono de eliminar y confirma en el modal

### Campos (formulario de subida)
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del documento | Texto libre | obligatorio |
| Archivo | File upload | obligatorio |

### Campos (columnas del listado)
| Campo | Tipo | Estado |
|---|---|---|
| Nombre | Texto capturado por usuario | solo lectura |
| Tipo de archivo | Auto-detectado | auto |
| Autor | Usuario que lo sube | auto |
| Fecha de subida | Fecha | auto |

### Notas para programación
1. El autor y la fecha de subida son automáticos, el sistema los registra sin input del usuario.
2. El modal de eliminar pide confirmación antes de borrar el documento.

---

## C-05 · Convertir prospecto a proyecto

**Actor:** Usuario admin  
El usuario convierte un prospecto aceptado en un proyecto. El sistema prellena los datos disponibles.

### Paso a paso
1. Desde el detalle del prospecto, hace clic en "Convertir a proyecto"
2. Se abre un modal con los datos del nuevo proyecto prellenados (nombre del prospecto → nombre del proyecto)
3. El usuario completa o corrige los campos restantes
4. Si el cliente o razón social no existe, puede crearlos desde este mismo modal (shortcut)
5. Hace clic en "Guardar" — se crea el proyecto y queda disponible en el módulo Proyectos

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del proyecto | Texto libre | obligatorio — prellenado con nombre del prospecto |
| Número de proyecto | Texto libre | obligatorio |
| Unidad de negocio | Dropdown | obligatorio |
| Líder de proyecto | Dropdown usuarios | obligatorio |
| Cliente | Dropdown catálogo Ajustes | obligatorio |
| Razón social | Dropdown catálogo Ajustes | obligatorio |

### Notas para programación
1. El modal incluye botones secundarios "Crear cliente nuevo" y "Crear razón social nueva" que abren un mini-modal con solo el campo Nombre (texto libre, obligatorio) para dar de alta el catálogo sin salir del flujo.
2. El proyecto creado queda vinculado al prospecto de origen. Si viene de prospecto, debe mostrar una nota informativa "Creado desde prospecto [nombre]".
3. Un cliente puede tener varios proyectos.

---

## Proyectos (P)

## P-01 · Listado de proyectos

**Actor:** Usuario admin  
Vista principal del módulo. Lista todos los proyectos con sus totales de ingresos y utilidad neta.

### Paso a paso
1. El usuario accede al módulo Proyectos
2. Ve el listado con filtros en la parte superior
3. Puede filtrar para acotar los resultados
4. Los contadores de totales se actualizan según filtros aplicados
5. Hace clic en un proyecto para ver su detalle

### Campos (columnas del listado)
| Campo | Tipo | Estado |
|---|---|---|
| UDN (Unidad de negocio) | Texto | solo lectura |
| Número de proyecto | Texto | solo lectura |
| Nombre del proyecto | Texto | solo lectura |
| Cliente | Texto | solo lectura |
| Razón social | Texto | solo lectura |
| Líder | Texto | solo lectura |
| Ingresos | Número | solo lectura |
| Utilidad neta | Número | solo lectura |

### Filtros de lista
- **Cliente** · _dinámico_ — Searchbox, valores desde tabla Clientes (Ajustes)
- **Número de proyecto** · _fijo_ — Searchbox de texto libre
- **Líder** · _dinámico_ — Dropdown, valores desde tabla Usuarios de la plataforma
- **UDN** · _dinámico_ — Dropdown, valores desde catálogo de unidades de negocio

### Notas para programación
1. Los contadores de "Total ingresos" y "Total utilidad neta" en la parte superior responden a los filtros aplicados — no siempre muestran el global.
2. El botón de descarga XLS exporta las mismas columnas visibles en pantalla, respetando los filtros activos.

### Output descargable
- **XLS** → plantilla: `proyectos_template.xlsx`

---

## P-02 · Crear proyecto

**Actor:** Usuario admin  
El usuario registra un nuevo proyecto directamente en el módulo (sin venir de un prospecto).

### Paso a paso
1. Hace clic en "Nuevo proyecto" desde el listado
2. Captura los datos generales del proyecto
3. Selecciona cliente y razón social de los catálogos
4. Hace clic en "Guardar" — el proyecto queda disponible como contenedor de ingresos, gastos, nóminas y comisiones

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del proyecto | Texto libre | obligatorio |
| Número de proyecto | Texto libre | obligatorio |
| Unidad de negocio | Dropdown catálogo | obligatorio |
| Líder de proyecto | Dropdown usuarios | obligatorio |
| Cliente | Dropdown catálogo Ajustes | obligatorio |
| Razón social | Dropdown catálogo Ajustes | obligatorio |

---

## P-03 · Detalle de proyecto

**Actor:** Usuario admin  
Vista detallada de un proyecto con sus totales calculados y los listados anidados de ingresos, gastos, nóminas y comisiones.

### Paso a paso
1. Hace clic en un proyecto del listado (P-01)
2. Ve el resumen con totales calculados
3. Navega entre las pestañas: Ingresos, Gastos, Nómina, Comisiones
4. Desde cada pestaña puede ver el listado filtrado de registros de ese proyecto y crear nuevos registros

### Campos (resumen)
| Campo | Tipo | Estado |
|---|---|---|
| Ingresos | Número | auto-calculado |
| Gastos | Número | auto-calculado |
| Utilidad bruta | Número | auto-calculado |
| Gastos fijos | Número | auto-calculado |
| Utilidad sin fijos | Número | auto-calculado |
| Comisiones | Número | auto-calculado |
| Nómina | Número | auto-calculado |
| Utilidad neta | Número | auto-calculado |
| Porcentaje de utilidad neta | Porcentaje | auto-calculado |

### Campos (datos generales)
| Campo | Tipo | Estado |
|---|---|---|
| Unidad de negocio | Texto | solo lectura |
| Líder | Texto | solo lectura |
| Número de proyecto | Texto | solo lectura |
| Nombre del proyecto | Texto | solo lectura |
| Cliente | Texto | solo lectura |
| Razón social | Texto | solo lectura |

### Notas para programación
1. Cada pestaña muestra solo los registros vinculados a ese proyecto.
2. Desde la pestaña Ingresos se muestra el contador total de ingresos del proyecto y el botón "Nuevo ingreso".
3. La pestaña Gastos muestra contador total de gastos y botón "Nuevo gasto".
4. La pestaña Nómina muestra contador total de nómina y botón "Nueva nómina".
5. La pestaña Comisiones muestra contador total y botón "Nueva comisión".
6. El título del evento aparece en la parte superior del detalle.

---

## P-04 · Descargable proyectos

**Actor:** Usuario admin  
El usuario descarga el listado de proyectos en formato XLS con los filtros aplicados.

### Paso a paso
1. Aplica los filtros deseados en el listado (P-01)
2. Hace clic en el botón de descarga
3. Se descarga el archivo XLS con las mismas columnas visibles y los filtros activos

### Notas para programación
1. Las columnas del XLS son: UDN, Número de proyecto, Cliente, Razón social, Líder, Ingresos, Utilidad neta.
2. El archivo responde a los filtros aplicados al momento de la descarga.

### Output descargable
- **XLS** → plantilla: `proyectos_template.xlsx`

---

## Ingresos (I)

## I-01 · Listado de ingresos

**Actor:** Usuario admin  
Vista principal del módulo. Lista todos los ingresos con contadores de subtotal y total.

### Paso a paso
1. El usuario accede al módulo Ingresos
2. Ve el listado con los contadores en la parte superior
3. Aplica filtros para acotar resultados
4. Los contadores responden a los filtros activos

### Campos (columnas del listado)
| Campo | Tipo | Estado |
|---|---|---|
| Fecha de factura | Fecha | solo lectura |
| Cliente | Texto | solo lectura |
| Proyecto | Texto | solo lectura |
| Concepto | Texto | solo lectura |
| Razón social | Texto | solo lectura |
| Orden de compra | Texto | solo lectura |
| Número de factura | Texto | solo lectura |
| Subtotal | Número | solo lectura |
| IVA | Número | solo lectura |
| Total | Número | solo lectura |
| Fecha límite de pago | Fecha | solo lectura |
| Estado | Etiqueta | solo lectura |
| Fecha de pago | Fecha | solo lectura |

### Filtros de lista
- **Cliente** · _dinámico_ — Searchbox, valores desde tabla Clientes
- **Razón social** · _dinámico_ — Searchbox, valores desde tabla Razones sociales
- **Proyecto** · _dinámico_ — Searchbox, valores desde tabla Proyectos
- **Estado** · _fijo_ — Dropdown: Por facturar, Pendiente de pago, En abonos, Pagado, Atrasado
- **Fecha límite** · _fijo_ — Rango de fechas: desde / hasta, formato DD-MMM-YYYY
- **Ver cancelados** · _fijo_ — Toggle: muestra solo ingresos en estado Cancelado

### Notas para programación
1. Los ingresos cancelados NO aparecen en el listado principal ni se suman a los contadores. Solo son visibles activando el toggle "Ver cancelados".
2. Los contadores de Subtotal y Total responden a los filtros activos.

### Output descargable
- **XLS** → plantilla: `ingresos_template.xlsx`

---

## I-02 · Crear ingreso

**Actor:** Usuario admin  
El usuario registra un nuevo ingreso. IVA y Total se calculan automáticamente a partir del Subtotal.

### Paso a paso
1. Hace clic en "Nuevo ingreso" desde el listado o desde la pestaña de ingresos de un proyecto
2. Captura los datos del formulario
3. El sistema calcula IVA y Total automáticamente (campos con candado, no editables)
4. Opcionalmente adjunta un archivo
5. Hace clic en "Guardar ingreso" — el ingreso entra con estado inicial "Por facturar"

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Proyecto | Dropdown catálogo Proyectos | opcional |
| Concepto | Texto libre | obligatorio |
| Orden de compra | Texto libre | opcional |
| Número de factura | Texto libre | opcional |
| Subtotal | Número (moneda) | obligatorio |
| IVA | Número | auto-calculado — no editable |
| Total | Número | auto-calculado — no editable |
| Fecha de factura | Fecha DD-MMM-YYYY | opcional |
| Fecha límite de pago | Fecha DD-MMM-YYYY | obligatorio |
| Fecha de pago | Fecha DD-MMM-YYYY | opcional |
| Estado | Dropdown | default: Por facturar |
| Adjunto | File upload | opcional |

### Notas para programación
1. IVA = Subtotal × 0.16. Total = Subtotal + IVA. Ambos son campos de solo lectura, se muestran con candado en el formulario.
2. Al guardar aparece modal con opciones: "Ver ingreso" o "Cerrar".
3. El estado inicial es siempre "Por facturar" al crear.

---

## I-03 · Registrar abono

**Actor:** Usuario admin  
El usuario registra pagos parciales sobre un ingreso. El sistema actualiza automáticamente el saldo restante y el estado.

### Paso a paso
1. Abre el detalle del ingreso y hace clic en la tab "Abonos"
2. Ve los contadores: Facturado, Pagado, Restante
3. Hace clic en "Registrar abono"
4. Captura la fecha y el monto del abono
5. El sistema recalcula Pagado y Restante automáticamente
6. Si el monto acumulado cubre el total, el estado cambia automáticamente a "Pagado"

### Campos (formulario de abono)
| Campo | Tipo | Estado |
|---|---|---|
| Fecha de abono | Fecha DD-MMM-YYYY | obligatorio |
| Monto del abono | Número (moneda) | obligatorio |

### Notas para programación
1. Al registrar el primer abono parcial, el estado del ingreso cambia automáticamente a "En abonos".
2. Cuando los abonos acumulados cubren el total, el estado cambia automáticamente a "Pagado".
3. Los abonos pueden eliminarse individualmente. Al eliminar un abono, el sistema recalcula los contadores.
4. Si el ingreso está "En abonos" y vence la fecha límite, pasa automáticamente a "Atrasado" (ver I-06).

---

## I-04 · Revisar / editar ingreso

**Actor:** Usuario admin  
El usuario abre el detalle de un ingreso para revisar o editar sus datos y agregar notas.

### Paso a paso
1. Hace clic en un ingreso del listado
2. Se abre el modal con tres tabs: Datos, Abonos, Notas
3. En la tab Datos puede editar los campos y guardar
4. En la tab Notas puede agregar comentarios en formato conversación

### Campos (tab Notas)
| Campo | Tipo | Estado |
|---|---|---|
| Texto de la nota | Textarea | obligatorio |
| Adjunto | File upload | opcional |
| Autor | Automático | auto |
| Fecha | Automático (fecha actual) | auto |

### Notas para programación
1. Las notas son inmutables una vez publicadas — no se editan ni eliminan.
2. El autor y la fecha se registran automáticamente al publicar la nota.

---

## I-05 · Cancelar ingreso

**Actor:** Usuario admin  
El usuario cancela manualmente un ingreso. Este deja de aparecer en el listado y se excluye de los totales.

### Paso a paso
1. Desde el detalle del ingreso, hace clic en "Cancelar ingreso"
2. Se abre un modal de confirmación
3. Confirma la cancelación
4. El ingreso pasa a estado Cancelado, desaparece del listado principal y se excluye de los contadores

### Notas para programación
1. La cancelación es manual e irreversible desde la UI. El ingreso no se elimina de la base de datos.
2. Los ingresos cancelados solo son visibles activando el toggle "Ver cancelados" en el listado.
3. Los cancelados no se suman a ningún contador ni sumatoria.

---

## I-06 · Marca automática de atrasado

**Actor:** Sistema  
El sistema cambia automáticamente el estado de un ingreso a "Atrasado" cuando vence la fecha límite de pago sin haberse pagado.

### Paso a paso
1. El sistema evalúa diariamente (o en cada carga) si la fecha actual supera la Fecha límite de pago
2. Si el ingreso no está en estado Pagado y la fecha venció, cambia el estado a Atrasado automáticamente
3. Se muestra un recuadro informativo en el detalle del ingreso indicando la razón del cambio

### Notas para programación
1. Aplica a ingresos en estados: Por facturar, Pendiente de pago, En abonos.
2. NO aplica si el ingreso está en Pagado o Cancelado.
3. El recuadro informativo debe decir algo como: "Actualizado automáticamente a Atrasado — la fecha límite de pago [fecha] ya venció y no se ha registrado ningún pago."
4. El cambio debe ocurrir sin acción del usuario.

---

## I-07 · Descargable ingresos

**Actor:** Usuario admin  
El usuario descarga el listado de ingresos en formato XLS con los filtros aplicados.

### Paso a paso
1. Aplica los filtros deseados en el listado (I-01)
2. Hace clic en el botón de descarga
3. Se descarga el archivo XLS

### Notas para programación
1. Columnas del XLS: Fecha de factura, Cliente, Proyecto, Concepto, Razón social, OC, Número de factura, Subtotal, IVA, Total, Fecha límite, Estado, Fecha de pago.
2. El archivo responde a los filtros aplicados al momento de la descarga.

### Output descargable
- **XLS** → plantilla: `ingresos_template.xlsx`

---

## Gastos (G)

## G-01 · Listado de gastos

**Actor:** Usuario admin  
Vista principal del módulo. Lista todos los gastos con contadores de subtotal y total.

### Paso a paso
1. El usuario accede al módulo Gastos
2. Ve el listado con contadores en la parte superior
3. Aplica filtros para acotar resultados

### Campos (columnas del listado)
| Campo | Tipo | Estado |
|---|---|---|
| Fecha de factura | Fecha | solo lectura |
| Proveedor | Texto | solo lectura |
| Proyecto | Texto | solo lectura |
| Concepto | Texto | solo lectura |
| Orden de compra | Texto | solo lectura |
| Número de factura | Texto | solo lectura |
| Forma de pago | Texto | solo lectura |
| Subtotal | Número | solo lectura |
| IVA | Número | solo lectura |
| Total | Número | solo lectura |
| Fecha límite de pago | Fecha | solo lectura |
| Estado | Etiqueta | solo lectura |
| Fecha de pago | Fecha | solo lectura |

### Filtros de lista
- **Proveedor** · _dinámico_ — Searchbox, valores desde tabla Proveedores (Ajustes)
- **Proyecto** · _dinámico_ — Searchbox, valores desde tabla Proyectos (incluye opción "Sin proyecto" para gastos generales)
- **Estado** · _fijo_ — Dropdown: Pendiente, Anticipo, Pagado
- **Forma de pago** · _fijo_ — Dropdown: Transferencia bancaria, Efectivo, Tarjeta de crédito, Cheque, Débito
- **Fecha límite** · _fijo_ — Rango de fechas: desde / hasta, formato DD-MMM-YYYY
- **Ver cancelados** · _fijo_ — Toggle: muestra solo gastos en estado Cancelado

### Notas para programación
1. El estado Cancelado no aparece en el dropdown de estado — solo se accede vía toggle "Ver cancelados".
2. La opción "Sin proyecto" en el filtro de Proyecto filtra los gastos generales (sin proyecto asignado).
3. Los gastos cancelados se excluyen de todos los contadores y sumatorias.
4. Los contadores de Subtotal y Total responden a los filtros activos.

### Output descargable
- **XLS** → plantilla: `gastos_template.xlsx`

---

## G-02 · Crear gasto

**Actor:** Usuario admin  
El usuario registra un nuevo gasto. Admite múltiples combinaciones: con/sin factura, con/sin proveedor, con/sin IVA, dentro/fuera de proyecto.

### Paso a paso
1. Hace clic en "Nuevo gasto" desde el listado o desde la pestaña de gastos de un proyecto
2. Captura los datos del formulario según aplique
3. Selecciona si tiene IVA (sí/no) — esto controla el cálculo
4. Si el estado elegido es "Anticipo", el sistema muestra obligatoriamente el campo de monto anticipado
5. Opcionalmente adjunta un archivo
6. Hace clic en "Guardar gasto"

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Proveedor | Dropdown catálogo Ajustes | opcional |
| Proyecto | Dropdown catálogo Proyectos | opcional |
| Concepto | Texto libre | obligatorio |
| Orden de compra | Texto libre | opcional |
| Número de factura | Texto libre | opcional |
| ¿Tiene IVA? | Toggle Sí / No | obligatorio |
| Subtotal | Número (moneda) | obligatorio |
| IVA | Número | auto-calculado — no editable |
| Total | Número | auto-calculado — no editable |
| Forma de pago | Dropdown | obligatorio |
| Fecha de factura | Fecha DD-MMM-YYYY | opcional |
| Fecha límite de pago | Fecha DD-MMM-YYYY | obligatorio |
| Fecha de pago | Fecha DD-MMM-YYYY | opcional |
| Estado | Dropdown | obligatorio — default: Pendiente |
| Monto anticipado | Número (moneda) | condicional — solo visible si Estado = Anticipo |
| Adjunto | File upload | opcional |

### Notas para programación
1. Si "¿Tiene IVA?" = Sí: IVA = Subtotal × 0.16, Total = Subtotal + IVA.
2. Si "¿Tiene IVA?" = No: IVA = 0, Total = Subtotal.
3. Cuando el usuario selecciona Estado = "Anticipo", aparece automáticamente el campo "Monto anticipado" (numérico, obligatorio).
4. Un gasto sin proyecto asignado es un "gasto general" y se refleja en el Reporte gerencial.
5. Al guardar aparece modal con opciones: "Ver gasto" o "Cerrar".

---

## G-03 · Cambio de estado manual

**Actor:** Usuario admin  
El usuario cambia manualmente el estado de un gasto entre Pendiente, Anticipo y Pagado.

### Paso a paso
1. Abre el detalle del gasto (G-04)
2. Cambia el campo Estado en el dropdown
3. Si cambia a "Anticipo", el sistema solicita obligatoriamente el monto anticipado
4. Si cambia a "Pagado", el sistema toma el monto total completo como pagado
5. Hace clic en "Guardar gasto"

### Notas para programación
1. A diferencia de Ingresos, el estado de los gastos NO cambia automáticamente — siempre es manual.
2. Al pasar de Anticipo a Pagado, se toma el monto total (no el anticipado) como monto saldado.
3. El cambio de estado se refleja inmediatamente en el header del modal y en el campo de estado.

---

## G-04 · Revisar / editar gasto

**Actor:** Usuario admin  
El usuario abre el detalle de un gasto para revisar o editar sus datos y agregar notas.

### Paso a paso
1. Hace clic en un gasto del listado
2. Se abre el modal con dos tabs: Datos, Notas
3. En Datos puede editar campos y guardar
4. En Notas puede agregar comentarios en formato conversación

### Notas para programación
1. El archivo adjunto (si existe) se muestra en la tab Datos.
2. Las notas siguen el mismo formato que Ingresos: autor y fecha automáticos, texto libre, adjunto opcional.

---

## G-05 · Cancelar gasto

**Actor:** Usuario admin  
El usuario cancela manualmente un gasto. Este deja de aparecer en el listado y se excluye de los totales.

### Paso a paso
1. Desde el detalle del gasto, hace clic en "Cancelar gasto"
2. Se abre un modal de confirmación
3. Confirma la cancelación
4. El gasto pasa a estado Cancelado, desaparece del listado principal y se excluye de los contadores

### Notas para programación
1. La cancelación es manual. El gasto no se elimina de la base de datos.
2. Los gastos cancelados solo son visibles activando el toggle "Ver cancelados".
3. Los cancelados no se suman a ningún contador ni sumatoria.

---

## G-06 · Descargable gastos

**Actor:** Usuario admin

### Paso a paso
1. Aplica filtros en el listado (G-01)
2. Hace clic en el botón de descarga

### Notas para programación
1. Columnas del XLS: Fecha de factura, Proveedor, Proyecto, Concepto, OC, Número de factura, Forma de pago, Subtotal, IVA, Total, Fecha límite, Estado, Fecha de pago.

### Output descargable
- **XLS** → plantilla: `gastos_template.xlsx`

---

## Nóminas (N)

## N-01 · Listado de nóminas

**Actor:** Usuario admin  
Vista principal del módulo. Lista todas las nóminas con su contador total.

### Campos (columnas del listado)
| Campo | Tipo | Estado |
|---|---|---|
| UDN | Texto | solo lectura |
| Número de proyecto | Texto | solo lectura |
| Nombre de proyecto | Texto | solo lectura |
| Cliente | Texto | solo lectura |
| Líder | Texto | solo lectura |
| Fecha de evento | Fecha | solo lectura |
| Número de registros (renglones) | Número | solo lectura |
| Total de nómina | Número | solo lectura |
| Fecha de pago | Fecha | solo lectura |
| Estado | Etiqueta | solo lectura |

### Filtros de lista
- **UDN** · _dinámico_ — Dropdown, valores desde catálogo de unidades de negocio
- **Cliente** · _dinámico_ — Searchbox, valores desde tabla Clientes
- **Proyecto** · _dinámico_ — Searchbox, valores desde tabla Proyectos
- **Líder** · _dinámico_ — Searchbox, valores desde tabla Usuarios
- **Estado** · _fijo_ — Dropdown: Pendiente autorizar, Pendiente pagar, Pagada
- **Ver cancelados** · _fijo_ — Toggle: muestra solo nóminas canceladas

### Notas para programación
1. "Número de registros" = cantidad de renglones de empleados que contiene la nómina.
2. El contador de "Total nóminas" responde a los filtros aplicados.
3. El estado Cancelada solo se accede vía toggle.

### Output descargable
- **XLS** → plantilla: `nominas_template.xlsx`

---

## N-02 · Crear nómina

**Actor:** Usuario admin  
El usuario crea una nómina vinculada a un proyecto, agregando uno o varios renglones de empleados.

### Paso a paso
1. Hace clic en "Nueva nómina" desde el listado o desde la pestaña Nómina de un proyecto
2. Selecciona el proyecto obligatoriamente
3. Captura los datos de cabecera (fechas, estado)
4. Hace clic en "Agregar renglón" para añadir empleados
5. Completa los datos de cada renglón — el monto por día se calcula automáticamente
6. El total de la nómina suma todos los renglones automáticamente
7. Hace clic en "Guardar nómina" — entra en estado "Pendiente autorizar"

### Campos (cabecera)
| Campo | Tipo | Estado |
|---|---|---|
| Proyecto | Dropdown catálogo Proyectos | obligatorio |
| Estado | Dropdown | default: Pendiente autorizar |
| Fecha de evento | Fecha DD-MMM-YYYY | obligatorio |
| Fecha de pago | Fecha DD-MMM-YYYY | opcional — se pide al pasar a Pagada |
| Total de nómina | Número | auto-calculado (suma de renglones) |

### Campos (renglón de empleado)
| Campo | Tipo | Estado |
|---|---|---|
| Rol | Dropdown (por definir) | obligatorio |
| Tipo de pago | Dropdown: Interno / Externo | obligatorio |
| Número de empleados | Número | obligatorio |
| Días trabajados | Número | obligatorio |
| Monto total | Número (moneda) | obligatorio |
| Monto por día | Número | auto-calculado = Monto total / Días trabajados |

### Notas para programación
1. Una nómina siempre pertenece a un proyecto — el campo Proyecto es obligatorio.
2. El monto por día se calcula automáticamente: Monto total ÷ Días trabajados.
3. El total de la nómina es la suma de todos los montos totales de los renglones.
4. Se pueden agregar y eliminar renglones antes de guardar.
5. Los roles están por definirse. Ejemplos vistos en demo: Coordinador general, Montaje, Stand, Catering, Logística.
6. Al guardar aparece modal con opciones: "Ver nómina" o "Cerrar".

---

## N-03 · Revisar / editar nómina

**Actor:** Usuario admin  
El usuario abre el detalle de una nómina para editar datos, cambiar estado o agregar notas.

### Paso a paso
1. Hace clic en una nómina del listado
2. Se abre el modal con dos tabs: Datos, Notas
3. En Datos ve cabecera y listado de renglones
4. Puede editar campos, agregar/eliminar renglones
5. Cambia el estado en el dropdown — al pasar a Pagada se registra la fecha de pago
6. Hace clic en "Guardar nómina"

### Notas para programación
1. El estado se mueve a nivel de la nómina completa (no por renglón): Pendiente autorizar → Pendiente pagar → Pagada / Rechazada.
2. Al pasar a estado "Pagada", el sistema debe solicitar o registrar automáticamente la fecha de pago.
3. Se pueden eliminar renglones existentes y agregar nuevos desde el detalle.

---

## N-04 · Cancelar nómina

**Actor:** Usuario admin

### Paso a paso
1. Desde el detalle de la nómina, hace clic en "Eliminar nómina"
2. Se abre modal de confirmación
3. Confirma — la nómina pasa a estado Cancelada, se oculta del listado y sale de las sumatorias

### Notas para programación
1. "Eliminar" en el contexto de nóminas equivale a "Cancelar" — el registro no se borra de la BD.
2. Las nóminas canceladas solo son visibles activando el toggle "Ver cancelados".

---

## N-05 · Descargable nóminas

**Actor:** Usuario admin

### Output descargable
- **XLS** → plantilla: `nominas_template.xlsx`

### Notas para programación
1. Columnas del XLS: UDN, Número de proyecto, Nombre del proyecto, Cliente, Líder, Fecha de evento, Número de registros, Total, Fecha de pago, Estado.
2. El archivo responde a los filtros aplicados.

---

## Comisiones (K)

## K-01 · Listado de comisiones

**Actor:** Usuario admin  
Vista principal del módulo. Lista todas las comisiones con su contador total.

### Campos (columnas del listado)
| Campo | Tipo | Estado |
|---|---|---|
| Fecha de evento | Fecha | solo lectura |
| UDN | Texto | solo lectura |
| Número de proyecto | Texto | solo lectura |
| Nombre de proyecto | Texto | solo lectura |
| Cliente | Texto | solo lectura |
| Razón social | Texto | solo lectura |
| Número de registros (renglones) | Número | solo lectura |
| Total de comisión | Número | solo lectura |
| Fecha de pago | Fecha | solo lectura |
| Estado | Etiqueta | solo lectura |

### Filtros de lista
- **UDN** · _dinámico_ — Dropdown, valores desde catálogo de unidades de negocio
- **Cliente** · _dinámico_ — Searchbox, valores desde tabla Clientes
- **Proyecto** · _dinámico_ — Searchbox, valores desde tabla Proyectos
- **Razón social** · _dinámico_ — Searchbox, valores desde tabla Razones sociales
- **Tipo** · _fijo_ — Dropdown: Diseño gráfico, Diseño industrial, Cuentas (y otros por definir)
- **Estado** · _fijo_ — Dropdown: Pendiente autorizar, Pendiente pagar, Pagada, Rechazada
- **Fecha de evento** · _fijo_ — Rango de fechas: desde / hasta, formato DD-MMM-YYYY
- **Ver cancelados** · _fijo_ — Toggle: muestra solo comisiones canceladas

### Notas para programación
1. El contador de total responde a los filtros aplicados.
2. Una comisión siempre pertenece a un proyecto.

### Output descargable
- **XLS** → plantilla: `comisiones_template.xlsx`

---

## K-02 · Crear comisión

**Actor:** Usuario admin  
El usuario crea una comisión vinculada a un proyecto, agregando renglones por empleado con monto capturado manualmente (sin cálculo por días).

### Paso a paso
1. Hace clic en "Nueva comisión" desde el listado o desde la pestaña Comisiones de un proyecto
2. Selecciona el proyecto obligatoriamente
3. Captura los datos de cabecera
4. Hace clic en "Agregar renglón" para añadir empleados
5. Para cada renglón: selecciona el empleado, el tipo de servicio y captura el monto manualmente
6. El total de la comisión suma todos los renglones
7. Hace clic en "Guardar comisión" — entra en estado "Pendiente autorizar"

### Campos (cabecera)
| Campo | Tipo | Estado |
|---|---|---|
| Proyecto | Dropdown catálogo Proyectos | obligatorio |
| Estado | Dropdown | default: Pendiente autorizar |
| Fecha de evento | Fecha DD-MMM-YYYY | obligatorio |
| Fecha de pago | Fecha DD-MMM-YYYY | opcional — se registra automáticamente al pasar a Pagada |
| Total de comisión | Número | auto-calculado (suma de renglones) |

### Campos (renglón de empleado)
| Campo | Tipo | Estado |
|---|---|---|
| Empleado | Dropdown (usuarios de la plataforma) | obligatorio |
| Tipo de servicio | Dropdown: Diseño gráfico, Diseño industrial, Cuentas, etc. | obligatorio |
| Monto total | Número (moneda) | obligatorio — capturado manualmente |

### Notas para programación
1. A diferencia de Nóminas, el monto de cada renglón en Comisiones es capturado manualmente — no hay cálculo por días ni por número de empleados.
2. Los empleados se seleccionan desde los usuarios registrados en la plataforma.
3. Los tipos de servicio están por definirse. Ejemplos: Diseño gráfico, Diseño industrial, Cuentas.
4. El total de la comisión = suma de todos los montos de los renglones.
5. Los montos de los renglones son editables después de agregar el renglón.
6. Al guardar aparece modal con opciones: "Ver comisión" o "Cerrar".

---

## K-03 · Revisar / editar comisión

**Actor:** Usuario admin  
El usuario abre el detalle de una comisión para editar datos, cambiar estado o agregar notas.

### Paso a paso
1. Hace clic en una comisión del listado
2. Se abre el modal con dos tabs: Datos, Notas
3. En Datos ve cabecera y listado de renglones (editables)
4. Puede editar montos, agregar/eliminar renglones
5. Cambia el estado en el dropdown
6. Hace clic en "Guardar comisión"

### Notas para programación
1. El estado se mueve a nivel de la comisión completa: Pendiente autorizar → Pendiente pagar → Pagada / Rechazada.
2. Al pasar a "Pagada", la fecha de pago se registra automáticamente.
3. Los montos de los renglones son editables desde el detalle.
4. Se pueden eliminar renglones y agregar nuevos.

---

## K-04 · Cancelar comisión

**Actor:** Usuario admin

### Paso a paso
1. Desde el detalle de la comisión, hace clic en "Eliminar comisión"
2. Se abre modal de confirmación
3. Confirma — la comisión pasa a estado Cancelada, se oculta del listado y sale de las sumatorias

### Notas para programación
1. "Eliminar" equivale a cancelar — el registro no se borra de la BD.
2. Las comisiones canceladas solo son visibles activando el toggle "Ver cancelados".

---

## K-05 · Descargable comisiones

**Actor:** Usuario admin

### Output descargable
- **XLS** → plantilla: `comisiones_template.xlsx`

### Notas para programación
1. Columnas del XLS: Fecha de evento, UDN, Nombre del proyecto, Cliente, Razón social, Número de registros, Total de comisión, Fecha de pago, Estado.
2. El archivo responde a los filtros aplicados.

---

## Ajustes (A)

## A-01 · Gestión de clientes

**Actor:** Usuario admin  
El usuario administra el catálogo de clientes que alimenta los dropdowns del resto de la plataforma.

### Paso a paso
1. Accede a Ajustes y selecciona la tab "Clientes"
2. Ve el listado de clientes con opción de buscar por nombre
3. Para crear: hace clic en "Nuevo cliente", captura el nombre y guarda
4. Para editar: hace clic en el ícono editar, modifica el nombre y guarda
5. Para eliminar: hace clic en el ícono eliminar y confirma

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del cliente | Texto libre | obligatorio |

### Filtros de lista
- **Nombre** · _fijo_ — Searchbox de texto libre

### Notas para programación
1. Al eliminar un cliente se pide confirmación — la eliminación es permanente de este catálogo.
2. Este catálogo alimenta el dropdown de Cliente en Proyectos y en el formulario de conversión de prospecto.
3. Un cliente puede estar asociado a múltiples proyectos.

---

## A-02 · Gestión de razones sociales

**Actor:** Usuario admin  
Mismo funcionamiento que A-01 pero para el catálogo de Razones sociales.

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Nombre de la razón social | Texto libre | obligatorio |

### Notas para programación
1. Este catálogo alimenta el dropdown de Razón social en Proyectos, Ingresos, Gastos y Comisiones.
2. Desde el formulario de creación de Proyectos y desde Convertir prospecto a proyecto (C-05) existe un shortcut para dar de alta una razón social nueva sin salir del flujo.

---

## A-03 · Gestión de proveedores

**Actor:** Usuario admin  
Mismo funcionamiento que A-01 pero para el catálogo de Proveedores.

### Campos
| Campo | Tipo | Estado |
|---|---|---|
| Nombre del proveedor | Texto libre | obligatorio |

### Notas para programación
1. Este catálogo alimenta el dropdown de Proveedor en el módulo de Gastos.

---

## A-04 · Gestión de usuarios y permisos

**Actor:** Usuario admin  
El usuario administra las cuentas de la plataforma y configura la matriz de permisos de cada usuario.

### Paso a paso
1. Accede a Ajustes y selecciona la tab "Usuarios"
2. Ve el listado de usuarios
3. Para crear: hace clic en "Nuevo usuario", captura nombre y correo, guarda — el sistema genera contraseña temporal automáticamente
4. Para ver/editar: hace clic en el ícono de editar, accede al detalle con datos y matriz de permisos
5. Configura los permisos por módulo/submódulo
6. Guarda los cambios

### Campos (formulario de usuario)
| Campo | Tipo | Estado |
|---|---|---|
| Nombre | Texto libre | obligatorio |
| Correo electrónico | Email | obligatorio |
| Contraseña temporal | Texto | auto-generado — visible con opción de copiar al portapapeles |

### Campos (matriz de permisos)
| Módulo / Submódulo | Permiso Ver | Permiso Editar |
|---|---|---|
| CRM | Toggle | Toggle |
| Proyectos | Toggle | Toggle |
| Ingresos | Toggle | Toggle |
| Gastos | Toggle | Toggle |
| Nóminas | Toggle | Toggle |
| Comisiones | Toggle | Toggle |
| Soporte | Toggle | Toggle |
| Ajustes | Toggle | Toggle |
| Usuarios | Toggle | Toggle |

### Filtros de lista
- **Nombre o correo** · _fijo_ — Searchbox de texto libre

### Notas para programación
1. Al crear un usuario, el sistema genera automáticamente una contraseña temporal que se muestra en pantalla con opción de copiar al portapapeles.
2. El botón "Restablecer contraseña" envía un correo al usuario con un link para cambiar su contraseña.
3. Regla de permisos: si el usuario no tiene permiso "Ver", automáticamente tampoco puede "Editar".
4. Los usuarios de la plataforma alimentan los dropdowns de Responsable (CRM), Líder (Proyectos) y Empleado (Comisiones).

---

## Reporte gerencial (R)

## R-01 · Visualizar reporte consolidado

**Actor:** Usuario admin (solo lectura — vista para dirección)  
El reporte consolida ingresos, egresos, nóminas y comisiones de un periodo seleccionado. No captura datos, solo lee y resume lo que generan los demás módulos.

### Paso a paso
1. El usuario accede al módulo Reporte gerencial
2. Selecciona el rango de fechas del periodo a consultar
3. Opcionalmente aplica otros filtros (UDN, proyecto, cliente, proveedor)
4. El sistema muestra los cuatro grandes totales del periodo y el resultado neto
5. Ve el listado de movimientos del periodo (scroll si es extenso)
6. Ve las gráficas de tendencia anual

### Filtros de lista
- **Periodo** · _fijo_ — Rango de fechas: desde / hasta, formato DD-MMM-YYYY (obligatorio para generar la vista)
- **UDN** · _dinámico_ — Dropdown, valores desde catálogo de unidades de negocio
- **Proyecto** · _dinámico_ — Searchbox, valores desde tabla Proyectos
- **Cliente** · _dinámico_ — Searchbox, valores desde tabla Clientes
- **Proveedor** · _dinámico_ — Searchbox, valores desde tabla Proveedores

### Campos (contadores principales)
| Campo | Tipo | Estado |
|---|---|---|
| Total de ingresos | Número | auto-calculado — responde a filtros |
| Total de egresos | Número | auto-calculado — responde a filtros |
| Total de nóminas | Número | auto-calculado — responde a filtros |
| Total de comisiones | Número | auto-calculado — responde a filtros |
| Resultado del periodo | Número | auto-calculado = Ingresos − Egresos − Nóminas − Comisiones |

### Campos (listado de movimientos)
| Campo | Tipo | Estado |
|---|---|---|
| Tipo | Etiqueta: Ingreso / Gasto general / Nómina / Comisión | solo lectura |
| Monto | Número (positivo para ingresos, negativo para gastos) | solo lectura |

### Notas para programación
1. El resultado neto se calcula como: Ingresos − Egresos − Nóminas − Comisiones.
2. Los ingresos aparecen como valores positivos en el listado de movimientos. Todos los egresos (gastos, nóminas, comisiones) aparecen como valores negativos.
3. El listado de movimientos puede ser muy extenso — debe tener scroll.
4. Las gráficas de tendencia anual 2025 muestran: gráfica izquierda (ingresos) y gráfica derecha (egresos + nóminas + comisiones).
5. El sub-listado inferior permite ver por separado: todos los ingresos del periodo, todos los egresos, todas las nóminas, todas las comisiones — también responden a los filtros.
6. El módulo es de solo lectura — no hay formularios de captura.
7. La descarga de plantilla XLS está **pendiente de entregar**.

### Output descargable
- **XLS** → plantilla: `reporte_gerencial_template.xlsx` ⚠️ pendiente de entregar

---

*Documento generado desde grabación Fireflies · Naomi Jardon · Jtech*
