---

# 📚 Reglas de Validación (`/validation_rules`)

El recurso **`validation_rules`** permite gestionar la lógica de validación dinámica aplicada a los campos de los Leads (`LeadField`).

Las reglas pueden crearse de dos maneras:

* **🧩 Modo Asistente (Template-based)**: basado en plantillas predefinidas (`STANDARD_RULES`)
* **🧠 Modo Experto (Manual)**: usando expresiones lógicas personalizadas en Python

---

## 🟢 Endpoints de Lectura

### 🟦 GET `/validation_rules`

Obtiene el listado de reglas de validación creadas.

#### Query Params

| Parámetro     | Tipo   | Default | Descripción                                                                                                |
| ------------- | ------ | ------- | ---------------------------------------------------------------------------------------------------------- |
| `only_active` | `bool` | `true`  | Si es `true`, devuelve solo reglas activas. Si es `false`, incluye también las desactivadas (soft delete). |

---

### 🟦 GET `/validation_rules/{id}`

Obtiene el detalle de una única regla de validación.

#### Path Params

* `id` (`int`): ID único de la regla de validación.

---

### 🟦 GET `/validation_rules/templates`

Devuelve el catálogo de **plantillas de reglas** (`STANDARD_RULES`) disponibles en el sistema.
Este endpoint es clave para construir formularios dinámicos en el Frontend.

#### Ejemplo de Respuesta

```json
[
  {
    "code": "MIN_VALUE",
    "name": "Valor Mínimo",
    "description": "El número debe ser mayor o igual al límite.",
    "required_params": ["limit"],
    "error_message": "El número debe ser mayor o igual a {limit}."
  },
  {
    "code": "EMAIL_FORMAT",
    "name": "Es Email Válido",
    "description": "Valida formato simple de correo.",
    "required_params": [],
    "error_message": "El formato del correo electrónico no es válido."
  }
]
```

---

## 🟠 Endpoints de Escritura

### 🟩 POST `/validation_rules`

Crea una nueva regla de validación asociada a un `LeadField`.

Existen **dos modalidades de creación**:

---

### 🧩 Opción A – Modo Asistente (Recomendado)

Se utiliza una plantilla existente (`template_code`).
El backend genera automáticamente la expresión lógica y el mensaje de error.

#### Request Body

```json
{
  "field_id": 35,
  "template_code": "MIN_LENGTH",
  "template_params": {
    "limit": 5
  }
}
```

#### Campos

| Campo             | Tipo     | Obligatorio | Descripción                                                          |
| ----------------- | -------- | ----------- | -------------------------------------------------------------------- |
| `field_id`        | `int`    | ✅           | ID del `LeadField` al cual se aplica la regla                        |
| `template_code`   | `string` | ✅           | Código de la plantilla (`MIN_VALUE`, `REGEX_MATCH`, etc.)            |
| `template_params` | `object` | ✅*          | Parámetros requeridos por la plantilla (si no requiere, enviar `{}`) |
| `name`            | `string` | ❌           | Nombre personalizado                                                 |
| `error_message`   | `string` | ❌           | Mensaje de error personalizado                                       |

---

### 🧠 Opción B – Modo Experto (Manual)

Se define manualmente la expresión lógica en Python.
La regla **no queda asociada a ninguna plantilla**.

#### Request Body

```json
{
  "field_id": 35,
  "name": "Validación Compleja Custom",
  "expression": "len(str(value)) > 5 and '@' in str(value)",
  "error_message": "El valor no cumple con el formato corporativo."
}
```

#### Variables disponibles en `expression`

| Variable / Función | Descripción                                                  |
| ------------------ | ------------------------------------------------------------ |
| `value`            | Valor del campo actual                                       |
| `fields`           | Diccionario con todos los campos del Lead (`fields.get(ID)`) |
| `today`, `now`     | Objetos `datetime`                                           |
| Funciones          | `len()`, `sum()`, `abs()`, `str()`                           |

📌 **Ejemplo usando múltiples campos**:

```python
value > fields.get(10)
```

---

### 🟧 PUT `/validation_rules/{id}`

Actualiza una regla de validación existente.

#### Comportamiento

* Si se envía `template_params`, se recalcula la expresión manteniendo la plantilla
* Si se envía `expression`, la regla pasa a **modo manual** y se elimina la referencia al template

#### Request Body (Ejemplo)

```json
{
  "name": "Nombre Actualizado",
  "error_message": "Nuevo mensaje de error",
  "template_params": {
    "limit": 8
  }
}
```

---

## 🔴 Endpoints de Estado y Borrado

### 🟥 DELETE `/validation_rules/{id}`

Elimina **físicamente** una regla de validación.

⚠️ **Advertencia**: esta acción es irreversible.

---

### 🟧 PUT `/validation_rules/disable/{id}`

Realiza un **borrado lógico (soft delete)**.
La regla deja de aplicarse, pero se conserva en el historial.

---

### 🟩 PUT `/validation_rules/active/{id}`

Restaura una regla previamente desactivada (`is_active = true`).

---
