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
  correo: { $not: { $regex: /^[^\s@]+@[^\s@]+\.[^\s@]+$/ } }
})
```
Muestra todos los clientes cuyos emails esten con un formato incorrecto, muy util para tener esto en cuenta y actualizar los datos de la mejor menara posible.

















