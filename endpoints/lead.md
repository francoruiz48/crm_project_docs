# 🗂️ API Reference: Lead (`/leads`)

El recurso `leads` administra los leads que puede crear el usuario. Llamamos "lead" a persona interesada en las ventas, en el sistema, es lo que el usuario quiera registrar.

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /leads`
Obtiene el listado de leads configurados en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo las entidades activas. Si es `false`, incluye también los deshabilitados. |
| `detailed` | `bool` | `false` | Si es `true`, devuelve el mayor detalle de los leads, no usar si existen muchos leads ya que puede ser lento. Si es `false`, se muestre el minimo detalle del lead. |
| `campaign_id` | `int` | `null` | . Si se indica un id entonces filtra los leads que son de esa campaña |

---

### 🟦 `GET /leads/{id}`
Obtiene el detalle de un solo lead por su ID.

**Parámetros (Path)**
* `id` (int): ID único del lead.

---

### 🟦 `POST /leads/search`
Realizar busqueda de leads por medio de filtros. Se envia un arreglo de filtros. 

**Body:**

```json
{
  "filters": [
    {
      "field_id": 4,
      "operator": "gte",
      "value": "2000-01-01"
    },
    {
      "field_id": 1,
      "operator": "like",
      "value": "r"
    }
  ]
}
```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `field_id` | `int` | Si* | Indica el field al cual se le aplica el filtro|
| `operator` | `str` | Si | Operador para realizar la busqueda |
| `value` | `str` | Si | Indica el valor con el cual se realiza la operación |

Los operadores disponbiles son:

| Operador | Descripción |
| --- | --- |
| `eq` | Igual (=) |
| `neq` | No igual (!=) |
| `gt` | Mayor que (>) |
| `lt` | Menor que (<) |
| `gte` | Mayor o igual (>=) |
| `let` | Menor o igual (<=) |
| `like` | Contiene (texto) |
| `ilike` | Contiene (texto, ignora mayusculas) |
| `in` | Lista de opciones |
| `between` | Entres dos valores (rangos) |

---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /leads`  
Crea un nuevo lead.

**Body:**

```json
{
    "campaign_id": 1,
    "values": [
        { "field_id": 1, "value": "Juan" },
        { "field_id": 2, "value": "Ruiz" },
        { "field_id": 3, "nomenclator_item_id": 2},
        { "field_id": 5, "value": "GAD-234"}
    ]
}


```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `campaign_id` | `int` | Si* | Campaña a la cual pertenece, solo puede pertencer a una |
| `field_id` | `int` | Si | Se indica el id del campo. |
| `value` | `str` | Si | Se indica el valor del campo. |
| `nomenclator_item_id` | `int` | No | Se indica el valor del id del nomenclador_item |

---
En los casos donde se utilicen los nomencladores como lead_field se utiliza "nomenclator_item_id", en vez de "value"

### 🟧 `PUT /leads/{id}`  
Actualiza la configuración básica de un lead existente.

**Body:**

```json
{
    "campaign_id": 1,
    "values": [
      { "field_id": 2, "value": "dadad"}
    ]
}


```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /leads/{id}`  
Elimina físicamente el lead y sus leadFieldValue asociados al lead.

---

### 🟧 `PUT /leads/disable/{id}`  
Desactivación lógica (Soft Delete).

* El lead deja de aparecer en las listas.
* Los datos históricos se conservan.

---

### 🟩 `PUT /leads/active/{id}`  
Restaura un lead previamente desactivado.

* El lead vuelve a ser visible y operativo.

```

```
