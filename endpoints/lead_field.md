## 🟦 GET /lead_fields
Trae el listado de campos de leads activos.

## Params
only_active=[True|False] -> Si queremos traer todos los que existen se coloca en False. 

## 🟦 GET /lead_fields/templates
Trae el listado de templates de campos de leads creados. 

## 🟦 POST /lead_fields
Crea un campo de lead

### Request (Body)
```json
{
  "name": "Nombre del Campo",
  "field_type_code": "INT",
  "default_value": "",
  "is_primary": false,
}
```
En caso de querer crear un campo con una plantilla:
```json
{
  "field_template_code": "PASSWORD_STRONG"
}
```

## 🟦 PUT /lead_fields/{id}
Obtiene un solo campo

## 🟦 DELETE /lead_fields/{id}
Elimina un campo

## 🟦 PUT /lead_fields/disable/{id}
Borrado logico de un lead. Lo desactiva.

## 🟦 PUT /lead_fields/active/{id}
Restaura un lead, lo vuelve a activar.



