# 🗂️ API Reference: Nomenclador (`/nomenclator_items`)

El recurso `nomenclator_items` administra los items de las entidades que pueden ser usadas en los LeadFieldValue. Por ejemplo Mendoza, San Juan, etc

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /nomenclator_items`
Obtiene el listado de items de nomencladores configurados en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo las entidades activas (visibles en formularios). Si es `false`, incluye también los deshabilitados. |
| `detailed` | `bool` | `false` | Si es `true`, devuelve el mayor detalle (hijos) de cada nomenclador, no usar si existen muchos items de nomencladores ya que puede ser lento. Si es `false`, se muestre el minimo detalle del nomenclador. |
| `nomenclator_id` | `int` | `null` | . Si se indica un id entonces devuelve los items que pertenecen a ese nomenclador |
| `parent_item_id` | `int` | `null` | Si se indica un id entonces devuelve los items que son hijos de ese item de nomenclador |

---

### 🟦 `GET /nomenclator_items/{id}`
Obtiene el detalle de un solo item de nomenclador por su ID.

**Parámetros (Path)**
* `id` (int): ID único del item de nomenclador.

---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /nomenclator_items`  
Crea un nuevo item de nomenclador.

**Body:**

```{
  "code": "MDZ",
  "value": "Mendoza",
  "nomenclator_id": 2,
  "parent_item_id": 1
}
```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `code` | `str` | Sí* | Código unico para el item |
| `value` | `int` | Si* | Valor que tiene el item |
| `nomenclator_id` | `int` | Si | Se indica el id del nomenclador al cual pertenecen |
| `parent_item_id` | `int` | No | Se indica el id del item de nomenclador que es el padre. Ejemplo: Mendoza pertenece a Argentina (se indica id de Argentina) |

---

### 🟧 `PUT /nomenclator_items/{id}`  
Actualiza la información de un item de nomenclador existente.

**Body:**

```json
{
  "code": "MDZ",
  "value": "Mendoza",
  "nomenclator_id": 2,
  "parent_item_id": 1
}

```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /nomenclator_items/{id}`  
Elimina físicamente el item de nomenclador.

---

### 🟧 `PUT /nomenclator_items/disable/{id}`  
Desactivación lógica (Soft Delete).

* El nomenclador item deja de aparecer en los formularios.
* Los datos históricos se conservan.

---

### 🟩 `PUT /nomenclator_items/active/{id}`  
Restaura un nomenclador item previamente desactivado.

* El nomenclador vuelve a ser visible y operativo.

```

```
