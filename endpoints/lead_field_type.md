# 🗂️ API Reference: Tipo de Campo de Lead (`/lead_field_types`)

El recurso `lead_field_types` administra los tipos de datos de los campos de leads. Permite definir qué tipos de datos se guardan (ej: String, Int, Float, Date, etc). 

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /lead_field_types`
Obtiene el listado de tipos de datos configurados en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo los tipos de datos activos (visibles en formularios). Si es `false`, incluye también los deshabilitados. |

Respuesta:

```json
[
    {
        "id": 1,
        "created_at": "2025-12-14T13:23:10.034156-03:00",
        "updated_at": "2025-12-14T13:23:10.034156-03:00",
        "active": true,
        "code": "STRING",
        "description": "Texto"
    },
    {
        "id": 2,
        "created_at": "2025-12-14T13:23:10.034156-03:00",
        "updated_at": "2025-12-14T13:23:10.034156-03:00",
        "active": true,
        "code": "INT",
        "description": "Número entero"
    },
    {
        "id": 3,
        "created_at": "2025-12-14T13:23:10.034156-03:00",
        "updated_at": "2025-12-14T13:23:10.034156-03:00",
        "active": true,
        "code": "NUMBER",
        "description": "Número decimal"
    },
    {
        "id": 4,
        "created_at": "2025-12-14T13:23:10.034156-03:00",
        "updated_at": "2025-12-14T13:23:10.034156-03:00",
        "active": true,
        "code": "DATE",
        "description": "Fecha"
    },
    {
        "id": 5,
        "created_at": "2025-12-14T13:23:10.034156-03:00",
        "updated_at": "2025-12-14T13:23:10.034156-03:00",
        "active": true,
        "code": "BOOL",
        "description": "Valor verdadero/falso"
    }
]

```

---

### 🟦 `GET /lead_field_types/{id}`
Obtiene el detalle de un solo tipo de dato por su ID.

**Parámetros (Path)**
* `id` (int): ID único del tipo de dato.

Respuesta: 
```json
{
    "id": 1,
    "created_at": "2025-12-14T13:23:10.034156-03:00",
    "updated_at": "2025-12-14T13:23:10.034156-03:00",
    "active": true,
    "code": "STRING",
    "description": "Texto"
}
```
---
