# 🎰 Base de Datos Casino Climax

Este repositorio contiene el diseño y estructura de una base de datos MongoDB para el **Casino Climax**. Su propósito es gestionar de forma eficiente los datos relacionados con clientes, juegos, empleados, niveles de membresía, horarios y productos disponibles en la tienda del casino.

---

## 🗂️ Colecciones principales

### 📁 1. `clientes`
Contiene la información personal de los clientes y su historial de juego. Cada cliente puede tener múltiples registros de actividad, incluyendo tipo de juego, fechas y resultados.

#### 📑Estructura basica:
```json
  {
    "id": "cliente_001",
    "nombre": "Lucía",
    "apellido": "Gómez",
    "documento": "12345678A",
    "edad": 28,
    "telefono": "+34 600123456",
    "nivel_id": "nivel_001",
    "correo": "lucia.gomez@email.com",
    "historial_juego": [
      {"juego_id": "jueg0_001", "apuesta": 50, "resultado": "ganó", "ganancia": 120},
      {"juego_id": "jueg0_002", "apuesta": 30, "resultado": "perdió", "ganancia": 0}
    ]
  }

```

---

### 🎲 2. `juegos`
Incluye los distintos juegos disponibles en el casino (por ejemplo, blackjack, póker, tragamonedas). Se almacena información como el tipo de juego, límites de apuesta y capacidad máxima de jugadores.

#### 📑Estructura basica:
```json
{
  "_id": "juego_001",
  "nombre": "poker mesa 1",
  "tipo": "cartas",
  "nivel": "VIP",
  "capacidad_maxima_personas": 5,
  "limites_apuestas_cop": [
    {
      "minima": 2000000,
      "maxima": 100000000
    }
  ],
  "estado_actual": "en mantenimeinto",
  "reponsable_id": "empleado_001"
}
```

---

### 🧍‍♂️ 3. `empleados`
Gestiona los datos del personal del casino, como crupieres, supervisores o personal administrativo. También se incluyen los turnos y asignaciones a mesas o máquinas específicas.

#### 📑Estructura basica:
```json
{
  "_id": "empleado_001",
  "nombre": "Jose",
  "apellido": "Borrero",
  "numero_telefonico": 3124357893,
  "cargo": "dealer",
  "id_juego_asignado": "juego_001",
  "horario": {
    "lunes": {
      "entrada": "14:00",
      "salida": "23:30"
    },
    "martes": {
      "entrada": "14:00",
      "salida": "23:30"
    },
    "miércoles": {
      "entrada": "14:00",
      "salida": "23:30"
    },
    "jueves": {
      "entrada": "14:00",
      "salida": "23:30"
    },
    "viernes": {
      "entrada": "14:00",
      "salida": "23:30"
    },
    "sabado": {
      "entrada": "14:00",
      "salida": "23:30"
    }
  }
}
```

---

### 🥤 4. `productos`
Registra los productos que se venden en la tienda del casino (bebidas, snacks, souvenirs, etc.), incluyendo nombre, categoría, precio y stock.

#### 📑Estructura basica:
```json
{
  "_id": "producto_001",
  "nombre": "coca-cola personal",
  "tipo": "bevida",
  "precio_cop": 2500,
  "stock": 22
}
```

---

### 🏅 5. `niveles`
Define los distintos niveles o membresías VIP del casino, sus beneficios y requisitos de acceso (como puntos acumulados u otras condiciones).

#### 📑Estructura basica:
```json
{
  "_id": "nivel_006",
  "nombre": "diamond",
  "costo": [
    {
      "mensual": 120000,
      "anual": 1200000
    }
  ],
    "id_juegos_disponibles": ["jueg0_007", "jueg0_006", "jueg0_005", "jueg0_004", "jueg0_003", "jueg0_001", "jueg0_002"]
}
```

---

## 🕐 6. `Horario del casino`

El casino opera en **jornada nocturna** de **lunes a sábado**, desde las **2:00 p.m. hasta las 11:30 p.m.**

#### 📑Estructura basica:
```json
{
    "_id": "horario_003",
    "dia": "miércoles",
    "hora_apertura": "14:00",
    "hora_cierre": "23:30"
}
```

---

## 📦 Organización del repositorio

- `Casino_climax.clientes.json` 
Contiene los datos de los clientes.

- `Casino_climax.juegos.json`  
Contiene los datos de los juegos.

- `Casino_climax.empleados.json`  
Contiene los datos de los empleados.

- `Casino_climax.productos.json` 
Contiene los datos de los productos.

- `Casino_climax.niveles.json` 
Contiene los datos de los niveles. 

Cada archivo `.json` contiene documentos de ejemplo para poblar la base de datos.

---

## 🧠 Notas importantes

- Se utilizan **referencias por ID** para relacionar clientes, juegos, empleados y niveles.
- Puedes usar **IDs personalizados** para facilitar consultas legibles y controladas.
- Para los **horarios** en el archivo de empleados se usaron incurstaciones.


---

### 🍃Consulta 1:

```js
db.clientes.find(
  {documento: {$regex: /[A-Z]$/}}
)
```
Muestra todos los clientes cuyo documento termine en una letra, ideal para ofertas especiales a extrajeros, o cumplimiento normativo.

### 🍃Consulta 2:

```js
db.juegos.find({
  nombre: { $regex: /\d+/ }
})
```
Muestra todos los juegos que contengan numeros en sus nombres para saber cuales juegos tiene mas de un puesto.

### 🍃Consulta 3:

```js
db.juegos.find({
  estado_actual: { $regex: /^(en|de)\s/ }
})
```
Muestra todos los juegos tengan estados con patrones especificos como *en* mantenimeinto o *de* baja.

### 🍃Consulta 4:

```js
db.empleados.find({
  nombre: { $regex: /[áéíóúñü]/i }
})
```
Muestra todos los empleados que tengan nombres con tildes ideal para identificar nombres de empleados con caracteres especiales y tenerlos en ceunta para filtrarlos mas facil.

### 🍃Consulta 5:

```js
db.empleados.find({
  cargo: { $regex: /dealer/i }
})
```
Muestra todos los empleados que tengan un cargo de dealer util para filtrar mas facil a los empleados y tenerlos en cuenta segun su cargo.

### 🍃Consulta 6:

```js
db.empleados.find({
  cargo: { $regex: /mantenimiento/i }
})
```
Muestra todos los empleados que tengan un cargo de mantenimeinto util para filtrar mas facil a los empleados y tenerlos en cuenta segun su cargo.

### 🍃Consulta 6:

```js
db.productos.find({
  nombre: { $regex: /-/ }
})
```
Muestra todos los productos que contengan guiones (-) en su nombre, ideal para identificar productos compuestos o con nombres especiales.

### 🍃Consulta 7:

```js
db.productos.find({
  "nombre": { $regex: /(personal)$/i },
  "tipo": "bevida"
})
```
Muestra todos los productos que tengan personal al final de su nombre para poder categorizarlos.

### 🍃Consulta 8:

```js
db.niveles.find({
  nombre: { $regex: /(gold|silver|platinum|diamond)/i }
})
```
Muestra todos los niveles con nombres de metales preciosos, perfecto para agrupar distintos tipos de membresia.

### 🍃Consulta 9:

```js
db.clientes.find({
  correo: { $not: { $regex: /^[^\s@]+@[^\s@]+\.[^\s@]+$/ } }
})
```
Muestra todos los clientes cuyos emails esten con un formato incorrecto, muy util para tener esto en cuenta y actualizar los datos de la mejor menara posible.

### 🍃Consulta 9:

```js
db.clientes.find({ 
    correo: { $regex: "\\.(ru|cn)$" } })

```
Muestra todos los clientes cuyos emails tengan dominios poco comunes para detectar posibles fraudes o spam.

### 🍃Consulta 10:

```js
db.clientes.find({ 
    documento: { $not: { $regex: "^\\d{8}[A-Z]$" } } })

```
Muestra todos los clientes cuyos documentos no cumplen las con los parametros de un documento valido, esto sirve para detectar fraudes o ingresos incorrectos en este campo.

### 🍃Consulta 11:

```js
db.clientes.find({ 
    correo: { $regex: "(_|\\.\\.)" } })

```
Muestra todos los clientes cuyos correos tienen guiones bajos (_), o multiples puntos para evitar cuentas con correos falsos o sospechosos.

### 🍃Consulta 11:

```js
db.clientes.find({ 
    "historial_juego.resultado": { $regex: "ganó" } })


```
Muestra todos los clientes que hayan ganado almenos una vez en su historial de apuestas, ideal para identificar las ganancias de los clientes y y cuando fueron.

### 🍃Consulta 12:

```js
db.juegos.find({ 
    tipo: { $regex: "ruleta", $options: "i" } })


```
Muestra todos los juegos que sean de tipo ruleta, esto es util para clasificar y filtrar juegos por tipo y consultarlos facilmente.

### 🍃Consulta 13:

```js
db.empleados.find({ 
    nombre: { $regex: "^J", $options: "i" } })


```
Muestra todos los empleados cuyo nombre comienza por "J", para facilitar busquedas rapidas.

### 🍃Consulta 14:

```js
db.empleados.find({ 
    numero_telefonico: { $regex: "^\\d{1,9}$" } })


```
Muestra todos los empleados cuyo numero telefonico tiene menos de 10 dijitos, sirve para identificar errores en el ingreso de datos.

### 🍃Consulta 15:

```js
db.niveles.find({ 
    _id: { $not: { $regex: "^nivel_\\d{3}$" } } })


```
Muestra todos los niveles cuyo id no sigue el formato establecido, sirve para poder asegurar que todos los niveles siguen el mismo formato de id.

### 🍃Consulta 16:

```js
db.niveles.find({ 
    _id: { $regex: "[13579]$" } })


```
Muestra todos los niveles cuyo id impar, sirve para segmentar los niveles por id y facilitar la busqueda.

### 🍃Consulta 17:

```js
db.niveles.find({ 
    nombre: { $regex: "\\s" } })


```
Muestra todos los niveles que contienen mas de una paabra en su nombre, ideal para filtrar de una manera muy cencilla.

### 🍃Consulta 18:

```js
db.niveles.find({ 
    "costo.0.mensual": { $not: { $mod: [1000, 0] } } })


```
Muestra todos los niveles cuyo costo mensual no sea multiplo de 1000, para asegurar que todos tengan valores redondos.

### 🍃Consulta 19:

```js
db.niveles.find({
  $expr: {
    $eq: [
      { $arrayElemAt: ["$costo.anual", 0] },
      { $multiply: [{ $arrayElemAt: ["$costo.mensual", 0] }, 10] }
    ]
  }
})


```
Muestra todos los niveles cuyo costo anual es 10 su costo mensual, para mantener todos los costos anueles en torno a la misma politica de precios.

### 🍃Consulta 20:

```js
db.niveles.find({ 
    costo: { $exists: false } })


```
Muestra todos los niveles cuyo costo esta nulo, para detectar documentos de niveles incompletos y dar pronta solucion al problema.

### 🍃Consulta 21:

```js
db.niveles.find({ 
    "id_juegos_disponibles.5": { $exists: true } })


```
Muestra todos los niveles que tengan disponibles mas de 5 juegos, esto con el fin de filtrarlos en torno a su generocidad con el cliente y ajustar los precios segun lo que se ofrece si es que se necesita.

### 🍃Consulta 22:

```js
db.niveles.find({ 
    "id_juegos_disponibles.5": { $exists: true } })


```
Muestra todos los niveles que tengan disponibles juegos con numeros impares, esto con el fin de facilitar su filtracion y busqueda efectiva.

### 🍃Consulta 23:

```js
db.niveles.find({ 
    id_juegos_disponibles: { $size: 0 } })


```
Muestra todos los niveles que no tengan juegos disponibles con el fin de encontrar y solucionar errores cometidos en la creacion de los documentos de esta coleccion.

### 🍃Consulta 24:

```js
db.niveles.find({ 
    id_juegos_disponibles: { $in: ["juego_001"] } })


```
Muestra todos los niveles que contengan un juego especifico por id, con el fin de que tan comun o popular es el juego.

### 🍃Consulta 25:

```js
db.niveles.find({ 
    id_juegos_disponibles: { $elemMatch: { $regex: "[A-Z]" } } })

```
Muestra todos los niveles que id de juegos con mayusculas (errores), con el fin de corregir errores de insercion de datos.


##### Gracias por tu leer :)

### Integrantes:
- Alejandro Naranjo Marin
- Daniel Felipe Trigos Sarmiento


























