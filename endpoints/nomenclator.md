# 🗂️ API Reference: Nomenclador (`/nomenclators`)

El recurso `nomenclators` administra las entidades que pueden ser usadas en los LeadField. Por ejemplo Ciudades, Paises

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /nomenclators`
Obtiene el listado de nomencladores configurados en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo las entidades activas (visibles en formularios). Si es `false`, incluye también los deshabilitados. |
| `detailed` | `bool` | `false` | Si es `true`, devuelve el mayor detalle (hijos) de cada nomenclador, no usar si existen muchos nomencladores ya que puede ser lento. Si es `false`, se muestre el minimo detalle del nomenclador. |
| `campaign_id` | `int` | `null` | . Si se indica un id entonces filtra los nomencladores que son de esa campaña |
| `global_nomenclator` | `bool` | `null` | Si se indica en True entonces trae todos los nomencladores que no tienen asociado una campaña, si se coloco en campaign_id un valor se concatena con estos valores. 

---

### 🟦 `GET /nomenclators/{id}`
Obtiene el detalle de un solo nomenclador por su ID.

**Parámetros (Path)**
* `id` (int): ID único del nomenclador.

---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /nomenclators`  
Crea un nuevo nomenclador.

**Body:**

```json
{
  "name": "Universidades",
  "campaign_id": 1,
  "parent_nomenclator_id": null
}

```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `name` | `str` | Sí* | Nombre visible del nomenclador (Label). |
| `campaign_id` | `int` | No* | Campaña a la cual pertenece, si no se indica campaña es un nomenclador global (se usa en todas las campañas) |
| `parent_nomenclator_id` | `int` | No | Se indica el id del nomenclador padre. |

---

### 🟧 `PUT /nomenclators/{id}`  
Actualiza la configuración básica de un nomenclador existente.

**Body:**

```json
{
  "name": "Facultades",
  "campaign_id": null,
  "parent_nomenclator_id": null
}

```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /nomenclators/{id}`  
Elimina físicamente el campo y tambien `nomenclator_items` asociados

Si creamos al menos un campo y le asociamos este nomenclator entonces al ejecutar el endpoint funcionara como un soft delete, es decir cambiara el atributo `active` a false.


---

### 🟩 `PUT /nomenclators/active/{id}`  
Restaura un nomenclador previamente desactivado.

* El nomenclador vuelve a ser visible y operativo.

