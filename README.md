- [x] Pickup y request no necesariamente son lo mismo (en normalización de columnas) **Se ha quitado de la normalización pickup y request separados**

- [x] ¿Todos los base number son lo mismo? **Se ha quitado de la normalización dispatching_base_num y originating_base_num separados**

- [x] Estaría bien mostrar lo de las columnas después de normalizar como un heatmap también **Se muestran juntos para comparar el antes y después**

- [x] ¿Por qué los pasajeros nulos a 0? **Se cambia la función para imputar valores nulos o negativos en passenger_count usando: 1. Mediana por trayecto (PULocationID + DOLocationID), si hay suficientes registros. 2. Mediana global como respaldo.**

- [ ] En la limpieza de pasajeros se podría hacer todo en la misma pasada
- [ ] En las limpiezas que se basan en poner la media de los viajes con mismo origen/destino (me ha gustado mucho la idea), podríamos ser un poco menos extremos y en vez de cargarnos el registro poner la media o mediana global
- [ ] En la visualización de los trayectos entre zonas más activas quitaría los números de la matriz y los dejaría a que se infieran con la escala de colores. Igual he visto que tenías seaborn por ahí, así que se podría añadir interactivo para que cuando ponga el ratón sobre la celda se muestre el número
- [ ] Ya que se han normalizado los nombres de columnas y etc, podrían integrarse los dataframes ya limpios en uno solo y hacer las visualizaciones filtrando en vez de llevarlos separados. Igual, si se usa seaborn eso podría dejarsele al usuario (que escoja el tipo de taxi/mes analizado, por ejemplo)
- [ ] A nivel de diseño (y también para demostrar que "entendimos" lo de los tier de datalakes y eso) daría un poco la apariencia de hacerlo por capas. En plan: se reciben los datos crudos, en el paso a la primera capa se normalizan las columnas (bronce, que no se suelen tocar nada de los datos) y luego en el paso a la segunda capa se hace la limpieza (valores nulos, etc...) y ahí de nuevo pues a salvarlos
- [ ] Pero bueno, eso si quieres lo puedo trabajar yo que es más una idea de diseño
- [ ] Y lo otro sería añadir más explicaciones en plan texto al notebook, pero eso sí por fa déjamelo completo a mí, que lo voy a coger como ejercicio de entender el código
