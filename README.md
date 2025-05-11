- [x] Pickup y request no necesariamente son lo mismo (en normalización de columnas)

  - **Se ha quitado de la normalización pickup y request separados**

- [x] ¿Todos los base number son lo mismo?

  - **Se ha quitado de la normalización dispatching_base_num y originating_base_num separados**

- [x] Estaría bien mostrar lo de las columnas después de normalizar como un heatmap también

  - **Se muestran juntos para comparar el antes y después**

- [x] Añadir un criterio de normalización para mantener los trayectos con origen = destino.

  - **Se añade una nueva característica same_location_flag, para los siguientes casos válidos:**
    - Carreras muy cortas: el pasajero viaja solo unas pocas manzanas dentro de la misma zona (las zonas pueden cubrir varias calles).
    - Tráfico denso: se recorre poco pero se cobra tiempo de espera, especialmente si el taxi está detenido.
    - Cancelaciones tras el inicio: el pasajero cancela o baja casi inmediatamente, pero la carrera se registra.
    - Errores de geocodificación: en ocasiones, aunque el trayecto sí ocurrió, ambos puntos se agrupan en la misma zona por la forma en que se registran los GPS.
    - Casos logísticos: viajes para recoger o dejar objetos, donde el origen y destino coinciden pero se cobra por el tiempo.
  - **Se añade una nueva característica suspicious_location_flag, para los siguientes casos sospechosos de fraude/inválidos:**
    - Si además de origen = destino, la distancia es cero, o el tiempo es muy corto y el precio es muy alto → caso de posible error o fraude.

- [x] ¿Por qué los pasajeros nulos a 0?

  - **Se cambia la función para imputar valores nulos o negativos en passenger_count usando: 1. Mediana por trayecto (PULocationID + DOLocationID), si hay suficientes registros. 2. Mediana global como respaldo.**

- [x] En la limpieza de pasajeros se podría hacer todo en la misma pasada

  - **Se aprovecha la iteración de los datasets para hacer las limpiezas de varios criterios en un a pasada, es decir un solo bucle, que aplica las normalizaciones**

- [x] En las limpiezas que se basan en poner la media de los viajes con mismo origen/destino (me ha gustado mucho la idea), podríamos ser un poco menos extremos y en vez de cargarnos el registro poner la media o mediana global.

  - **Se utiliza el mismo criterio para todas las normalizaciones:**
    - passenger_count: mediana local o global
    - trip_distance: mediana local o global
    - trip_duration_min: media local o global
    - total_amount: media local o global
    - location_valid: marca si el origen y destino son válidos

- [x] En la visualización de los trayectos entre zonas más activas quitaría los números de la matriz y los dejaría a que se infieran con la escala de colores. Igual he visto que tenías seaborn por ahí, así que se podría añadir interactivo para que cuando ponga el ratón sobre la celda se muestre el número.
  - **Se ha actualizado la función con:**
    - Recorre ambos diccionarios de datasets (originales y limpios).
    - Genera un heatmap para cada uno.
    - Quita los números dentro de las celdas (annot=False) para que se infieran por escala de color.
    - Usa plotly.express.imshow para interactividad: permite ver el valor al pasar el ratón.
- [x] Ya que se han normalizado los nombres de columnas y etc, podrían integrarse los dataframes ya limpios en uno solo y hacer las visualizaciones filtrando en vez de llevarlos separados. Igual, si se usa seaborn eso podría dejarsele al usuario (que escoja el tipo de taxi/mes analizado, por ejemplo)
  - **Se descarta unificar porque es muy costoso**
  - `error: MemoryError: Unable to allocate 1.26 GiB for an array with shape (8, 21068851) and data type object`
- [ ] A nivel de diseño (y también para demostrar que "entendimos" lo de los tier de datalakes y eso) daría un poco la apariencia de hacerlo por capas. En plan: se reciben los datos crudos, en el paso a la primera capa se normalizan las columnas (bronce, que no se suelen tocar nada de los datos) y luego en el paso a la segunda capa se hace la limpieza (valores nulos, etc...) y ahí de nuevo pues a salvarlos.
      Pero bueno, eso si quieres lo puedo trabajar yo que es más una idea de diseño.
      Y lo otro sería añadir más explicaciones en plan texto al notebook, pero eso sí por fa déjamelo completo a mí, que lo voy a coger como ejercicio de entender el código
      **100% para Alejandro**
- [ ] El plasmar esto en el Documento
  - **40% Alejandro Borrador + 50% René Borrador + 10% Versión final**
