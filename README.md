# Pasos

App personal para iPhone que muestra los pasos y la distancia caminada de cada día, tomados de la app Salud, con resúmenes por semana, mes y año.

## Qué muestra

- **El día**: pasos y distancia (caminando + corriendo). Las flechas, o deslizar a los lados, cambian de día; tocar la fecha vuelve a hoy.
- **Ver resumen**: Semana, Mes o Año, con total de pasos y kilómetros, promedio diario, mejor día, gráfico de barras (toca una barra para ver el detalle) y la lista de cada día o mes.
- Mientras no haya datos tuyos, muestra datos de ejemplo marcados como tales.

## Cómo se mantiene al día

iOS no deja que una página web lea Salud. Por eso el ícono de la app en la pantalla de inicio es un **atajo**:

1. Tocas el ícono **Pasos**.
2. El atajo lee de Salud los pasos y la distancia de cada día del último año. Tarda uno o dos segundos.
3. Abre la app en Safari con esos datos, así que siempre ves la cifra de ese momento.

El botón ↻ dentro de la app vuelve a ejecutar el atajo. La app no se actualiza sola mientras está abierta: para ver lo último, ábrela de nuevo desde el ícono o toca ↻.

Los datos viajan en la dirección después del signo `#`, una parte que el navegador no envía a ningún servidor, y quedan guardados solo en Safari, en tu teléfono. Cada vez que abres la app llega el último año completo; los días más antiguos se conservan en el teléfono.

## Crear el atajo «Pasos»

Se hace una sola vez. Los nombres pueden variar un poco según la versión de iOS.

1. Abre **Atajos**, entra a la pestaña **Atajos** y toca **+**. Arriba, toca el nombre y escribe `Pasos`, tal cual: la app busca el atajo con ese nombre.
2. Toca **Agregar acción**, busca «muestras de salud» y elige **Buscar muestras de salud**:
   - Tipo: **Pasos**.
   - Filtro de fecha: **Fecha de inicio · está en los últimos · 370 días**. Si la acción trae otro filtro de fecha, cámbialo por este.
   - **Agrupar por: Día**.
   - Si aparece **Límite** activado, desactívalo.
3. Agrega otra **Buscar muestras de salud**. Tipo: busca «distancia» y elige la de **caminar y correr** (Distancia caminando + corriendo). Mismo filtro de 370 días y **Agrupar por: Día**.
4. Agrega una acción **Texto** y arma estas seis líneas, cada una en su propio renglón:

   ```
   P
   (búsqueda 1) → Fecha de inicio
   (búsqueda 1) → Valor
   D
   (búsqueda 2) → Fecha de inicio
   (búsqueda 2) → Valor
   ```

   Para cada variable: deja el cursor en su renglón, toca **Seleccionar variable** sobre el teclado y toca la acción de búsqueda que corresponde (la primera para P, la segunda para D). Luego toca la variable que quedó en el texto y elige la propiedad **Fecha de inicio** o **Valor**. En las dos de fecha, en **Formato de fecha** elige **ISO 8601**. Si después de elegir **Valor** la variable sigue diciendo «Muestras de Salud», déjala así: la app toma el número igual.

5. Agrega **Codificar URL** (busca «codificar»). Toma el Texto anterior.
6. Agrega otra acción **Texto** y escribe `https://pablocarvallo.github.io/pasos/#r=` y, pegada al final y sin espacio, la variable que entrega **Codificar URL** (Texto codificado de URL). Usa **Texto** y no la acción **URL**: esta última separa la dirección y la variable en dos direcciones distintas.
7. Agrega **Abrir URL**. Toma el texto anterior.
8. Toca **Listo**.

La dirección del paso 6 también aparece en la app, en el botón de arriba a la izquierda (**Atajo y datos**), con un botón para copiarla.

### Ponerlo en la pantalla de inicio

1. Guarda en Fotos la imagen `icon-512.png` de este repositorio.
2. En Atajos, mantén presionado el atajo **Pasos** y toca **Compartir → Añadir a pantalla de inicio**.
3. Toca el ícono, elige **Seleccionar foto** y usa la imagen guardada. Deja el nombre **Pasos** y toca **Añadir**.

La primera vez, iOS pide permiso para leer Salud (permite **Pasos** y **Distancia caminando + corriendo**) y para abrir la página: elige **Permitir siempre**.

## Notas

- **No uses «Añadir a pantalla de inicio» desde Safari.** Esa versión guarda sus datos aparte y no recibe lo que manda el atajo. El ícono debe ser el del atajo.
- Safari abre una pestaña nueva cada vez. Si se acumulan, en los ajustes de Safari ve a **Cerrar pestañas** y elige **Después de un día**.
- Si el atajo envía algo que la app no entiende, la app lo avisa y muestra el texto recibido en **Atajo y datos**, con un botón para copiarlo.
- Desde **Atajo y datos** también se puede pegar un reporte a mano o borrar los datos guardados en el teléfono.

## Publicar

En GitHub, ve a **Settings → Pages** y publica la rama `main` desde la raíz (`/`). La app queda en `https://pablocarvallo.github.io/pasos/`.

## Archivos

- `index.html`: la app completa (HTML, estilos y código).
- `icon-180.png`, `icon-512.png`: ícono.
