```markdown
# 📚 API Reference: Reglas de Validación (`/validation_rules`)

El recurso `validation_rules` permite gestionar la lógica de validación dinámica aplicada a los campos de los Leads (`LeadField`). Estas reglas pueden ser expresiones personalizadas (Modo Experto) o basarse en plantillas predefinidas (Modo Asistente).

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /validation_rules`
Obtiene el listado general de todas las reglas de validación existentes.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo las reglas activas. Si es `false`, incluye también las eliminadas lógicamente. |

---

### 🟦 `GET /validation_rules/{id}`
Obtiene el detalle de una única regla de validación específica.

**Parámetros (Path)**
* `id` (int): ID único de la regla de validación.

---

### 🟦 `GET /validation_rules/templates`
Devuelve el catálogo de plantillas (`STANDARD_RULES`) disponibles en el sistema. Es fundamental para construir formularios dinámicos en el Frontend.

**Respuesta de Ejemplo:**
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

##🟠 Endpoints de Escritura###🟩 `POST /validation_rules`Crea una nueva regla de validación asociada a un campo. Existen dos modalidades de creación:

####**Opción A: Modo Asistente (Recomendado)**Se utiliza un `template_code` obtenido del endpoint `/templates`. El backend genera automáticamente la expresión lógica y el mensaje de error.

**Body:**

```json
{
    "field_id": 35,
    "template_code": "MIN_LENGTH",
    "template_params": {
        "limit": 5
    }
}

```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `field_id` | `int` | Sí | ID del `LeadField` al cual se aplicará la regla. |
| `template_code` | `str` | Sí | Código de la plantilla (ej: `MIN_VALUE`, `REGEX_MATCH`). |
| `template_params` | `dict` | Sí* | Diccionario con los valores requeridos por la plantilla. (*Si la plantilla no pide params, enviar `{}`). |
| `name` | `str` | No | Nombre personalizado. Si se omite, se usa el de la plantilla. |
| `error_message` | `str` | No | Mensaje de error personalizado. Si se omite, se genera uno automático. |

####**Opción B: Modo Experto (Manual)**Se define la expresión lógica manualmente en Python. Esto desvincula la regla de cualquier plantilla.

**Body:**

```json
{
    "field_id": 35,
    "name": "Validación Compleja Custom",
    "expression": "len(str(value)) > 5 and '@' in str(value)",
    "error_message": "El valor no cumple con el formato corporativo."
}

```

**Variables disponibles en `expression`:**

* `value`: El valor del campo actual que se está validando.
* `fields`: Diccionario de todos los campos del Lead. Se accede vía `fields.get(ID)`. Ej: `value > fields.get(10)`.
* `today`, `now`: Objetos datetime para comparaciones de fecha.
* Funciones: `len()`, `sum()`, `abs()`, `str()`.

---

###🟧 `PUT /validation_rules/{id}`Actualiza una regla existente.

* Si envías `template_params`, se recalcula la expresión manteniendo la plantilla original.
* Si envías `expression`, la regla se convierte en "Manual" y se elimina la referencia al template.

**Body:**

```json
{
    "name": "Nombre Actualizado",
    "error_message": "Nuevo mensaje de error",
    "template_params": { "limit": 8 }
}

```

---

##🔴 Endpoints de Estado y Borrado###🟥 `DELETE /validation_rules/{id}`Elimina físicamente una regla de la base de datos.

> ⚠️ **Advertencia:** Esta acción es irreversible.

---

###🟧 `PUT /validation_rules/disable/{id}`Desactivación lógica (Soft Delete). La regla deja de validarse al procesar Leads, pero se mantiene en el historial.

---

###🟩 `PUT /validation_rules/active/{id}`Restaura una regla previamente desactivada, volviendo a poner `is_active = true`.

```

```
