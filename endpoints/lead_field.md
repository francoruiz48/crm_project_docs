## 🟦 GET /lead_fields

### Descripción
Trae el listado de campos de leads activos.
---

## Params
only_active=[True|False] -> Si queremos traer todos los que existen se coloca en False. 


## 🟦 POST /lead_fields

### Descripción
Crea un campo de lead
---

### Request (Body)
```json
{
  "name": "Nombre del Campo",
  "field_type_code": "INT",
  "default_value": ""
}
```

