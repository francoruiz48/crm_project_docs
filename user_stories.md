### 🟢ÉPICA 1 — Gestión de Campos y Datos de Leads (CAMPOS)

| Código      | User Story                                                                                                                |
| ----------- | ------------------------------------------------------------------------------------------------------------------------- |
| **USCMP1**  | Como usuario, quiero poder definir los campos que tendrán mis leads para tener flexibilidad en el manejo de datos.        |
| **USCMP2**  | Como usuario, quiero poder configurar validaciones en los campos para asegurar la calidad de los datos.                   |
| **USCMP3**  | Como usuario, quiero aplicar máscaras a campos de texto para evitar errores de carga.                                     |
| **USCMP4**  | Como usuario, quiero que un campo dependa de otro (ej. Provincia → Ciudad).                                               |
| **USCMP5**  | Como usuario, quiero que ciertos campos sean obligatorios según el valor de otros campos.                                 |
| **USCMP6**  | Como administrador, quiero definir qué roles pueden ver o editar cada campo.                                              |
| **USCMP7**  | Como usuario, quiero subir archivos en campos del lead (PDF, DOCX, JPG, etc.).                                            |
| **USCMP8**  | Como usuario, quiero cargar una foto del lead para identificarlo visualmente.                                             |
| **USCMP9**  | Como administrador, quiero definir qué tipos de archivo se aceptan en cada campo.                                         |
| **USCMP10** | Como usuario, quiero visualizar archivos subidos sin necesidad de descargarlos.                                           |
| **USCMP11** | Como usuario, quiero ver el historial de modificaciones de los datos del lead.                                            |
| **USCMP12** | Como usuario, quiero ver quién creó, editó o eliminó un campo.                                                            |
| **USCMP13** | Como usuario, quiero definir cuál o cuáles serán las claves primarias del lead.                                           |
| **USCMP14** | Como usuario, quiero que al crear un lead se valide que no exista otro con la misma clave primaria.                       |
| **USCMP15** | Como usuario, quiero definir campos comunes con validaciones preestablecidas para ahorrar tiempo (ej. email, contraseña). |
| **USCMP16** | Como usuario, quiero establecer el orden en que se muestran los campos.                                                   |
| **USCMP17** | Como usuario, quiero disponer de un campo de etiquetas (tags) para clasificar mis leads.                                  |

-------------

### 🟢ÉPICA 2 — Campañas y Estructura Jerárquica (CAMPAÑAS)

| Código     | User Story                                                                         |
| ---------- | ---------------------------------------------------------------------------------- |
| **USCAM1** | Como usuario, quiero agrupar leads en campañas para organizarlos mejor.            |
| **USCAM2** | Como usuario, quiero definir distintos conjuntos de campos según la campaña.       |
| **USCAM3** | Como usuario, quiero organizar campañas en jerarquías (ej. Expo Educativa → 2024). |
| **USCAM4** | Como usuario, quiero ver quién creó y modificó una campaña (auditoría).            |

-------------

### 🟢ÉPICA 3 — Nomencladores y Clasificaciones (NOMENCLADORES)

| Código     | User Story                                                                                       |
| ---------- | ------------------------------------------------------------------------------------------------ |
| **USNOM1** | Como usuario, quiero definir nomencladores globales o específicos por campaña.                   |
| **USNOM2** | Como usuario, quiero definir qué ítems del nomenclador se usan en cada campaña.                  |
| **USNOM3** | Como usuario, quiero organizar nomencladores en jerarquías (ej. Universidad → Provincia → Tipo). |
| **USNOM4** | Como usuario, quiero reutilizar o clonar nomencladores existentes.                               |
| **USNOM5** | Como usuario, quiero activar o desactivar ítems de un nomenclador por campaña o fecha.           |
| **USNOM6** | Como usuario, quiero agrupar la vista de leads según un nomenclador.                             |
| **USNOM7** | Como usuario, quiero permitir múltiples valores en un mismo nomenclador.                         |

-------------

### 🟢ÉPICA 4 — Visualización Personalizable (VISUALIZACIÓN)

| Código     | User Story                                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| **USVIS1** | Como administrador, quiero configurar columnas, orden y formato del listado.                                 |
| **USVIS2** | Como administrador, quiero definir el formato visual por tipo de campo (badge, imagen, fecha, moneda, etc.). |
| **USVIS3** | Como administrador, quiero que cada campaña tenga una vista predeterminada.                                  |
| **USVIS4** | Como usuario, quiero guardar vistas personalizadas y compartirlas.                                           |
| **USVIS5** | Como administrador, quiero definir filtros rápidos visibles por campaña.                                     |
| **USVIS6** | Como usuario, quiero guardar filtros aplicados para reutilizarlos.                                           |
| **USVIS7** | Como usuario, quiero visualizar leads en formato de tarjetas (cards).                                        |
| **USVIS8** | Como usuario, quiero ver la foto del lead junto con sus datos esenciales.                                    |

-------------

### 🟢ÉPICA 5 — Automatizaciones y Workflows (AUTOMATIZACIONES)

| Código     | User Story                                                                                 |
| ---------- | ------------------------------------------------------------------------------------------ |
| **USAUT1** | Como usuario, quiero crear automatizaciones entre campos basadas en reglas.                |
| **USAUT2** | Como usuario, quiero ejecutar acciones automáticas cuando un lead cambie de estado.        |
| **USAUT3** | Como administrador, quiero asignar leads automáticamente según criterios definidos.        |
| **USAUT4** | Como usuario, quiero recibir notificaciones automáticas ante ciertos eventos.              |
| **USAUT5** | Como usuario, quiero que se creen tareas automáticamente al llegar a una etapa específica. |

-------------

### 🟢ÉPICA 6 — Importación, Exportación e Integraciones

| Código     | User Story                                                                          |
| ---------- | ----------------------------------------------------------------------------------- |
| **USIMP1** | Como usuario, quiero migrar datos de forma sencilla para ahorrar tiempo.            |
| **USIMP2** | Como usuario, quiero mapear columnas de Excel a campos personalizados.              |
| **USIMP3** | Como usuario, quiero definir qué hacer ante valores inválidos al importar datos.    |
| **USIMP4** | Como usuario, quiero descargar plantillas Excel con los campos de la campaña.       |
| **USIMP5** | Como usuario, quiero exportar leads a Excel o CSV.                                  |
| **USIMP6** | Como usuario, quiero sincronizar mis leads con sistemas externos.                   |
| **USIMP7** | Como usuario, quiero integrar el sistema con Google Calendar para agendar eventos.  |
| **USIMP8** | Como usuario, quiero integrar el sistema con Gmail para enviar correos rápidamente. |

-------------

### 🟢ÉPICA 7 — Reportes y Análisis (REPORTES)

| Código     | User Story                                                                               |
| ---------- | ---------------------------------------------------------------------------------------- |
| **USREP1** | Como usuario, quiero crear reportes personalizados.                                      |
| **USREP2** | Como usuario, quiero una interfaz visual para crear reportes sin conocimientos técnicos. |
| **USREP3** | Como usuario, quiero definir niveles de agregación y filtros avanzados.                  |
| **USREP4** | Como usuario, quiero definir KPIs por campaña.                                           |
| **USREP5** | Como usuario, quiero analizar datos según nomencladores.                                 |
| **USREP6** | Como usuario, quiero generar gráficos automáticamente según el tipo de campo.            |

-------------

### 🟢ÉPICA 8 — Acceso y Seguridad (SEGURIDAD)

| Código     | User Story                                                                   |
| ---------- | ---------------------------------------------------------------------------- |
| **USSEG1** | Como usuario, quiero iniciar sesión con Google.                              |
| **USSEG2** | Como administrador, quiero definir roles y permisos por usuario.             |
| **USSEG3** | Como administrador, quiero definir qué acciones puede realizar cada usuario. |
| **USSEG4** | Como administrador, quiero invitar usuarios a la organización.               |
| **USSEG5** | Como administrador, quiero restringir el acceso por campaña o grupo.         |
| **USSEG6** | Como administrador, quiero definir permisos por campo.                       |
| **USSEG7** | Como administrador, quiero auditar quién hizo qué y cuándo en el sistema.    |

-------------

### 🟢ÉPICA 9 — Formularios de Ingreso

| Código     | User Story                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------- |
| **USFOR1** | Como usuario, quiero crear formularios para registrar nuevos leads.                               |
| **USFOR2** | Como usuario, quiero diseñar formularios utilizando estilos CSS.                                  |
| **USFOR3** | Como usuario, quiero editar formularios para agregar o eliminar campos.                           |
| **USFOR4** | Como usuario, quiero que ciertos campos se habiliten luego de ingresar un dato clave (ej. email). |

-------------

### 🟢ÉPICA 10 — Interacciones y Seguimiento

| Código     | User Story                                                                    |
| ---------- | ----------------------------------------------------------------------------- |
| **USINT1** | Como usuario, quiero listar todas las interacciones de un lead.               |
| **USINT2** | Como usuario, quiero registrar una interacción con un lead.                   |
| **USINT3** | Como usuario, quiero modificar el estado de una interacción.                  |
| **USINT4** | Como usuario, quiero definir tipos de interacción (correo, llamada, mensaje). |
| **USINT5** | Como usuario, quiero ver el historial de cambios de una interacción.          |
| **USINT6** | Como usuario, quiero escribir notas internas sobre un lead.                   |

-------------

### 🟢ÉPICA 11 — Búsqueda y Organización

| Código     | User Story                                                                                      |
| ---------- | ----------------------------------------------------------------------------------------------- |
| **USBUS1** | Como usuario, quiero una barra de búsqueda global para encontrar cualquier entidad del sistema. |
| **USBUS2** | Como administrador, quiero segmentar leads para que cada vendedor vea solo los asignados.       |
| **USBUS3** | Como usuario, quiero disponer de una lista de tareas (to-do list) asociadas a mis leads.        |
