# 🗂️ API Reference: Campos de Lead (`/lead_fields`)

El recurso `lead_fields` administra la estructura dinámica de los Leads. Permite definir qué datos se guardan (ej: Nombre, Edad, CBU, Instagram). Estos campos pueden crearse desde cero o basarse en plantillas predefinidas que incluyen reglas de validación automáticas.

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /lead_fields`
Obtiene el listado de campos configurados en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo los campos activos (visibles en formularios). Si es `false`, incluye también los deshabilitados. |
| `campaign_id` | `int` | `null` | Se indica el ID de la campaña para filtrar por esta. |
| `detailed` | `bool` | `False` | Si es `true`, devuelve todo el detalle de los campos. |

---

### 🟦 `GET /lead_fields/{id}`
Obtiene el detalle de un solo campo por su ID.

**Parámetros (Path)**
* `id` (int): ID único del campo.

---

### 🟦 `GET /lead_fields/templates`
Devuelve el catálogo de plantillas de campos (`STANDARD_FIELD_TEMPLATES`).
Útil para que el Frontend muestre un selector rápido de campos comunes (ej: "Email", "DNI", "CBU") y el usuario no tenga que configurarlos manualmente.

**Respuesta de Ejemplo:**
```json
[
  {
    "code": "EMAIL",
    "name": "Correo Electrónico",
    "field_type_code": "STRING",
    "rules": [...]
  },
  {
    "code": "DNI_ARG",
    "name": "DNI (Argentina)",
    "field_type_code": "STRING",
    "rules": [...]
  }
]

```

---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /lead_fields`  
Crea un nuevo campo para los Leads. Existen dos formas de hacerlo:

#### **Opción A: Creación por Plantilla**   
Se envía el código de la plantilla. El sistema autocompleta el nombre, tipo de dato y crea automáticamente las reglas de validación (ej: Regex de email).

**Body:**

```json
{
  "name": "Patente", //Opcional
  "campaign_id": 1,
  "order": 1,
  "required": true,
  "is_primary": false,
  "is_visible": true,
  "lead_field_section_id": 1
  "field_template_code": "FIRST_NAME",
}

```

* **`field_template_code`** (str): Código obtenido del endpoint `/templates`.
* *Nota:* Puedes sobrescribir el `name` si quieres uno distinto al de la plantilla.

#### **Opción B: Creación Manual**  
Se definen todos los atributos manualmente. No incluye validaciones automáticas (se deben agregar aparte en `/validation_rules`).

Opción B.1. Establecemos un campo con input_mask (no es obligatorio).

**Body:**

```json
{
    "name": "Patente",
    "campaign_id": 1,
    "order": 1,
    "required": false,
    "is_primary": false,
    "lead_field_section_id": 1
    "field_type_code": "STRING",
    "input_mask": "AAA-###", 
}
```

Opción B.2. Creamos un campo que refiere a un nomenclador para poder establecer nomencladores items en sus campos.

**Body:**

```json
{
    "campaign_id": 1,
    "order": 1,
    "required": false,
    "is_primary": false,
    "lead_field_section_id": 1
    "nomenclator_id": 2,
    "field_type_code": "SELECTOR", //Puede ser tambien CHECKBOX
    "field_subtype_code": "SELECTOR_MULTIPLE", //Obligatorio si es un nomenclador. Si es checkbox usamos CHECKBOX_MULTIPLE
}
```
Opción B.3. Definimos un campo para relacionar con otros leads.

**Body:**

```json
{   
    "name": "Lead otra campaña",
    "field_type_code": "LEAD",   //Siempre debemos especificar lead cuando usamos related_campaign_id
    "related_campaign_id": 2,   //Establecemos la campaña de cual pertenece el lead a relacionar
    "campaign_id": 1,
    "order": 2,
    "required": true,
    "is_primary": false,
    "lead_field_section_id": 1
}
```

Opción B.4. Creamos un campo calculado. Este campo no recibe valores sino que los calcula. 

**Body:**

```json
{   
    "name": "Lead otra campaña",
    "field_type_code": "CALCULATED",  
    "calculation_expression": "Cantidad * Precio",  //Para referenciar a otros campos simplemente debemos usar sus nombres.    
    "campaign_id": 1,
    "order": 2,
    "required": true,
    "is_primary": false,
    "lead_field_section_id": 1
}
```


| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `name` | `str` | Sí* | Nombre visible del campo (Label). (*Opcional si se usa plantilla). |
| `field_type_code` | `str` | Sí* | Tipo de dato (`STRING`, `INT`, `DATE`, `BOOL`). (*Opcional si se usa plantilla). |
| `order` | `int` | Si* | Orden en que se muestran el campo. |
| `campaign_id` | `int` | Si* | Campaña a la cual pertenece el campo |
| `lead_field_section_id` | `int` | Si* | Se especifica la sección a la cual pertenece. |
| `default_value` | `str` | No | Valor por defecto si el usuario no completa nada. |
| `is_primary` | `bool` | No | `true` se valida para evitar repetidos y funciona como identificador, pueden definirse más de un field con este valor en True. |
| `required` | `bool` | No | `true` si el campo es obligatorio. |
| `input_mask` | `str` | No | Indica si la entrada debe cumplir un formato.  |
| `is_visible` | `bool` | No | Por defecto es `true`, esta para ser utilizado en el front. |
| `field_subtype_code` | `str` | Depende | Se especifica obligatoriamente si usamos un tipo de dato que tiene subtipo. |
| `related_campaign_id` | `int` | No | Se especifica la campaña a la cual pertenece el lead. Este atributo se especifica cuando queremos relacionar leads |
| `calculation_expression` | `str` | No | Expresión en EXCEL utilizada para calcular su valor. Este campo no va a recibir valores de entrada, sino que usa los valores de los demás campos. |

---

La forma de especificar "input_mask" es:
```
# -> Número (\d)
A -> Letra ([a-zA-Z])
* -> Alfanumérico ([a-zA-Z0-9])
Cualquier otro caracter se trata como literal (ej: -, (, ), .)
```
En el caso de "AAA-###" indica que los primeros tres caracteres deben ser letras, luego un guion medio y luego tres números.

### 🟧 `PUT /lead_fields/{id}`  
Actualiza la configuración básica de un campo existente (Nombre, valor por defecto, etc.).

Hay que enviar si o si todos los campos obligatorios. (los que se indican en la tabla anterior).

**Body:**

```json
{   
    "name": "Nombre",
    "field_type_code": "STRING",
    "campaign_id": 2,
    "order": 2,
    "required": false,
    "is_primary": false,
    "lead_field_section_id": 1
}

```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /lead_fields/{id}`  
Elimina físicamente el campo y tambien `validation_rule` asociados

Si creamos al menos un lead de la misma campaña entonces al ejecutar el endpoint era un soft delete, es decir cambiara el atributo `active` a `false`

---

### 🟩 `PUT /lead_fields/active/{id}`  
Restaura un campo previamente desactivado.

* El campo vuelve a ser visible y operativo.

---
