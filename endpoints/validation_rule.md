## 🟦 GET /validation_rules
Trae el listado de reglas de validaciones creadas. 

Params
only_active=[True|False] -> Si queremos traer todos los que existen se coloca en False. 

## 🟦 GET /validation_rules/templates
Trae el listado de templates de reglas de validaciones creados. 

## 🟦 POST /validation_rules
Crea una validación

### Request (Body)
```json
{
    "name": "Es Email Válido",
    "expression": "'@' in str(value) and '.' in str(value)",
    "error_message": "El formato del correo electrónico no es válido.",
    "field_id": 35
}
```
name: nombre de la validación.
expressión: expresión que va a evaluar el sistema de validaciones. Si usas fields['id'] donde id es el id del LeadField podes usar multiples campos en la expresión.
error_message: es el mensaje de error cuando hace efecto la regla de validación.
field_id: es el id del LeadField al cual pertenece la regla de validación.

En caso de querer crear un campo con una plantilla:
```json
{
    "template_code": "MIN_LENGTH",
    "template_params": {"limit": 5},
    "field_id": 35
}
```
field_id: es el ID del LeadField que queremos asociar a la regla.
template_code: valor de "code" de los templates de validation rules.
template_params: los nombres de los parametros varian según la regla, y algunos no requieren un parametro.

## 🟦 PUT /validation_rules/{id}
Obtiene una sola regla de validación

## 🟦 DELETE /validation_rules/{id}
Elimina una regla de validación

## 🟦 PUT /validation_rules/disable/{id}
Borrado logico de una regla. Lo desactiva.

## 🟦 PUT /validation_rules/active/{id}
Restaura una regla, la vuelve a activar.


