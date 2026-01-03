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

#### **Opción A: Creación por Plantilla (Recomendado)**   
Se envía el código de la plantilla. El sistema autocompleta el nombre, tipo de dato y crea automáticamente las reglas de validación (ej: Regex de email).

**Body:**

```json
{
  "field_template_code": "FIRST_NAME",
  "campaign_id": 1,
  "order": 1,
  "required": true,
  "is_primary": false
}

```

* **`field_template_code`** (str): Código obtenido del endpoint `/templates`.
* *Nota:* Puedes sobrescribir el `name` si quieres uno distinto al de la plantilla.

#### **Opción B: Creación Manual**  
Se definen todos los atributos manualmente. No incluye validaciones automáticas (se deben agregar aparte en `/validation_rules`).

**Body:**

```json
{
    "name": "Patente",
    "required": false,
    "is_primary": false,
    "input_mask": "AAA-###", 
    "campaign_id": 1,
    "field_type_code": "STRING",
    "order": 1
}
```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `name` | `str` | Sí* | Nombre visible del campo (Label). (*Opcional si se usa plantilla). |
| `field_type_code` | `str` | Sí* | Tipo de dato (`STRING`, `INT`, `DATE`, `BOOL`). (*Opcional si se usa plantilla). |
| `default_value` | `str` | No | Valor por defecto si el usuario no completa nada. |
| `is_primary` | `bool` | No | `true` se valida para evitar repetidos y funciona como identificador, pueden definirse más de un field con este valor en True. |
| `required` | `bool` | No | `true` si el campo es obligatorio. |
| `input_mask` | `str` | No | Indica si la entrada debe cumplir un formato.  |
| `order` | `int` | Si | Orden en que se muestran el campo |
| `campaign_id` | `int` | Si | Campaña a la cual pertenece el campo |

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

**Body:**

```json
{
  "name": "Email Personal",
  "required": true
}

```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /lead_fields/{id}`  
Elimina físicamente el campo y **todas sus validaciones asociadas**.

> ⚠️ **Cuidado:** Esto también borrará los valores (`LeadValue`) guardados en los leads para este campo.

---

### 🟧 `PUT /lead_fields/disable/{id}`  
Desactivación lógica (Soft Delete).

* El campo deja de aparecer en los formularios y listados de Leads activos.
* Los datos históricos se conservan.

---

### 🟩 `PUT /lead_fields/active/{id}`  
Restaura un campo previamente desactivado.

* El campo vuelve a ser visible y operativo.

```

```
