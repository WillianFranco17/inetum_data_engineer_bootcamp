# Respuestas a las preguntas

## 1. En la parte 1, al guardar nuestro DataFrame transformado en la capa Silver, utilizamos .mode("overwrite"). Si un ingeniero comete un error y cambia esto a .mode("append") y ejecuta la celda tres veces seguidas, ¿qué ocurriría físicamente con los datos en el Lakehouse y cómo afectaría esto a las métricas del negocio?

### Si el ingeniero ejecuta .mode("append") varias veces los registros se duplicaran lo cual afectaria de forma negativa las metricas de negocio, ya que las metricas se inflarian quedando incorrectas o inconsistentes, lo que llevaria a tomar malas decisiones y problemas dentro de la operacion.

---

## 2. Durante la parte 2 simulamos la llegada de novedades logísticas (ej. un pedido que cambió de "EN TRÁNSITO" a "ENTREGADO"). ¿Por qué fue estrictamente necesario usar una operación MERGE (Upsert) sobre nuestra tabla Delta en lugar de usar un simple .mode("append") o .mode("overwrite")?

### En este escenario el uso de la operacion MERGE(Upsert) es esencial ya que esta permite actualizar los registros existentes sin crear duplicados, tambien permite insertar nuevos registros solo cuando es necesario y mantiene la consistencia de los daots lo cual evita la eliminacion innecesaria o que se dupliquen los registros; en el caso de usar .mode("append") se crearian duplicados innesarios o .mode("overwrite") eliminaria datos importantes y se perderia el historial. 

---

## 3. En la parte 3 preparamos la tabla Gold para ser consumida directamente por Power BI aplicando V-Order y Z-Order. Explica brevemente cuál es la diferencia principal entre estas dos técnicas y por qué son fundamentales para el modo Direct Lake.

### Las dos tecnicas reducen el tiempo de busqueda y mejoran la eficiencia del procesamiento al realizar consultas en Power BI cuando se usa el modo Direct Lake lo que genera respuestas mas rapidas y mejorando la experiencia del usuario final.

### - V-order: Optimiza las consultas basadas en un columna clave.
### - Z-order: Optimiza las consultas complejas con multiples columnas.
