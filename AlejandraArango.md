# Tarea 4 - Almacenamiento y Consultas de Datos en Big Data con MongoDB

## Aplicando consultas en MongoDB para la gestión eficiente de datos en un entorno Ecommerce
El manejo de grandes volúmenes de información es uno de los pilares fundamentales en el ámbito del Big Data. Para ello, las bases de datos NoSQL como MongoDB ofrecen herramientas flexibles y potentes que permiten realizar operaciones de inserción, actualización, eliminación y consulta de datos de manera eficiente.
En este trabajo se presentan ejemplos prácticos aplicados a una base de datos de comercio electrónico (Ecommerce), donde se ilustran consultas básicas, filtros con operadores y procesos de agregación para obtener estadísticas relevantes. El objetivo es comprender cómo estas operaciones facilitan la organización y el análisis de la información, optimizando la gestión de datos en entornos reales.

### Descripción
Este trabajo muestra ejemplos de consultas en MongoDB aplicadas a una base de datos de Ecommerce, incluyendo operaciones básicas, filtros y agregaciones para analizar y gestionar datos de manera eficiente.

1.Consultas básicas (inserción, selección, actualización y eliminación de documentos).

- Insertar un producto
```bash
db.products.insertOne({
  name: "Audífonos Bluetooth",
  category_id: ObjectId("6732ab12e1"),
  price: 120000,
  stock: 50,
  description: "Audífonos inalámbricos con gran autonomía.",
  specifications: { color: "negro", bateria: "24h", bluetooth: true },
  created_at: new Date()
});
```
<p float="left">
  <img src="Capturas/Agregar producto.png" width="500" />
</p>

- Actualizar nombre de un producto
```bash
db.products.updateOne(
  { name: "Audífonos Bluetooth" }, 
  { $set: { name: "Audífonos Inalámbricos" } } 
);
```
<p float="left">
  <img src="Capturas/Actualizar producto.png" width="500" />
</p>


- Eliminar reseña con un id especifico
```bash
db.reviews.deleteOne({ _id: 60 });
```
<p float="left">
  <img src="Capturas/Borrar reseña.png" width="500" />
</p>


---

2.Consultas con filtros y operadores. 

- Productos que el nombre inicie con A
```bash
db.products.find(
  { name: { $regex: /^A/i } },
  { name: 1, description: 1, _id: 0 }
);
```
<p float="left">
  <img src="Capturas/Productos que empiezan por A.png" width="500" />
</p>


- Reseñas con una puntuacion mayor a 5
```bash
db.reviews.find({ rating: { $gte: 5 } });
```
<p float="left">
  <img src="Capturas/Puntuacion 5.png" width="500" />
</p>


- Ordenes que esten en estado Entregado 
```bash
db.orders.find(
  { status: "Entregado"  },
  { order_date: 1, total: 1, status:1, _id: 0 }
);
```
<p float="left">
  <img src="Capturas/Estatus Entregado.png" width="500" />
</p>


---

3.Consultas de agregación para calcular estadísticas (contar, sumar, promediar, etc.).


- Contar cuántos ordenes tiene un usuario 
```bash
db.orders.aggregate([
  { $group: { _id: "$user_id", orders_count: { $sum: 1 } } }
]);
```
<p float="left">
  <img src="Capturas/Orden de compra 1.png" width="500" />
</p>


- Promedio de precio de productos
```bash
db.products.aggregate([
  { $group: { _id: null, avg_price: { $avg: "$price" } } }
]);
```
<p float="left">
  <img src="Capturas/Promedio Precio.png" width="500" />
</p>


- Total de productos
```bash
db.products.aggregate([
  { $count: "total_products" }
]);
```
<p float="left">
  <img src="Capturas/Total productos.png" width="500" />
</p>
