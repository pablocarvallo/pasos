# Pasos

App personal para iPhone que muestra los pasos y la distancia caminada de cada día, tomados de la app Salud, con resúmenes por semana, mes y año.

## Qué muestra

- **El día**: pasos y distancia (caminando + corriendo). Las flechas, o deslizar a los lados, cambian de día; tocar la fecha vuelve a hoy.
- **Ver resumen**: Semana, Mes o Año, con total de pasos y kilómetros, promedio diario, mejor día, gráfico de barras (toca una barra para ver el detalle) y la lista de cada día o mes.
- Mientras no haya un buzón conectado, muestra datos de ejemplo marcados como tales.

## Cómo llegan los datos de Salud

iOS no deja que una app web lea Salud. Por eso los datos pasan por un buzón:

1. El atajo **Pasos** lee de Salud los pasos y la distancia de cada día del último año.
2. Deja ese reporte en un repositorio **privado** de GitHub (`pasos-datos`), como un *issue*.
3. La app lee el reporte más reciente cada vez que la abres o vuelves a ella.

Para traer la cifra de este momento, toca ↻ (arriba a la derecha): la app abre Atajos, el atajo corre en uno o dos segundos y, al volver a la app, aparecen los datos nuevos. Cada reporte trae el último año completo, así que no se pierde nada aunque pases días sin actualizar.

La app revisa cada reporte antes de usarlo. Si el atajo manda varias muestras por día (búsquedas sin **Agrupar por: Día**) o fechas y valores que no calzan, no cambia tus datos y avisa qué corregir.

## 1. Crear el buzón en GitHub

1. Crea un repositorio nuevo, **privado**, llamado `pasos-datos`.
2. Ve a **Settings → Developer settings → Personal access tokens → Fine-grained tokens** y toca **Generate new token**.
3. Ponle un nombre (por ejemplo `Pasos`) y elige la expiración. Cuando venza, habrá que crear otro y volver a conectarlo.
4. En **Repository access** elige **Only select repositories** y marca `pasos-datos`.
5. En **Permissions → Repository permissions**, da a **Issues** el acceso **Read and write**.
6. Toca **Generate token** y copia el token. GitHub lo muestra una sola vez.

## 2. Instalar y conectar la app

1. Abre `https://pablocarvallo.github.io/pasos/` en **Safari**.
2. Toca **Compartir → Añadir a pantalla de inicio**.
3. Abre la app desde la pantalla de inicio y toca el botón de arriba a la izquierda (**Buzón y atajo**).
4. Deja el repositorio `pablocarvallo/pasos-datos`, pega el token y toca **Probar y conectar**. La pantalla muestra los datos para el atajo, con botones para copiarlos.

## 3. Crear el atajo «Pasos»

Se hace una sola vez. Los nombres pueden variar un poco según la versión de iOS.

1. Abre **Atajos**, entra a la pestaña **Atajos** y toca **+**. Arriba, toca el nombre y escribe `Pasos`, tal cual: la app busca el atajo con ese nombre.
2. Agrega **Buscar muestras de salud**:
   - Tipo: **Pasos**.
   - Filtro: **Fecha de inicio · está en los últimos · 370 días**.
   - **Agrupar por: Día**. Es indispensable: sin esto Salud entrega cada registro suelto y no el total del día.
   - **Límite** desactivado.
3. Agrega otra **Buscar muestras de salud**. Tipo: busca «distancia» y elige la de **caminar y correr**. Mismo filtro de 370 días y **Agrupar por: Día**.
4. Agrega una acción **Texto** con seis renglones:

   ```
   P
   (búsqueda de pasos) → Fecha de inicio
   (búsqueda de pasos) → Valor
   D
   (búsqueda de distancia) → Fecha de inicio
   (búsqueda de distancia) → Valor
   ```

   Para cada variable: deja el cursor en su renglón, toca **Seleccionar variable** y toca la burbuja de la búsqueda que corresponde. Luego toca la variable y elige **Fecha de inicio** o **Valor**. En las fechas, en **Formato de fecha** elige **ISO 8601**. Si después de elegir **Valor** la variable sigue diciendo «Muestras de Salud», déjala así: la app toma el número igual.

5. Agrega **Obtener contenido de URL**:
   - URL: `https://api.github.com/repos/pablocarvallo/pasos-datos/issues`
   - Toca **Mostrar más**. **Método: POST**.
   - **Encabezados**: agrega uno con la clave `Authorization` y el valor `Bearer ` seguido del token. La app lo tiene listo para copiar.
   - **Cuerpo de la solicitud: JSON**, con dos campos de tipo **Texto**: `title` con el valor `Pasos`, y `body` con la variable **Texto** del paso 4.
6. Toca **Listo**.

La primera vez, iOS pide permiso para leer Salud (permite **Pasos** y la distancia) y para conectarse a `api.github.com`: elige **Permitir siempre**.

Como el atajo envía un año de datos de Salud, iOS pide un permiso extra: en **Configuración → Apps → Atajos → Avanzado**, activa **Permitir compartir grandes cantidades de datos**.

## Notas

- Si tienes la versión anterior del atajo, borra las acciones **Codificar URL**, el segundo **Texto** y **Abrir URL**: ya no se usan.
- En **Buzón y atajo** se puede recuperar todo el historial del buzón, pegar un reporte a mano, desconectar el buzón o borrar los datos guardados en el teléfono.
- El token da acceso solo a los issues del repositorio privado y queda guardado en Atajos y en la app, en el teléfono.
- Dentro de Claude la página no puede llamar a GitHub; la lectura del buzón funciona en la app instalada desde `pablocarvallo.github.io/pasos`.

## Archivos

- `index.html`: la app completa (HTML, estilos y código).
- `manifest.webmanifest`, `icon-180.png`, `icon-512.png`: instalación en la pantalla de inicio e ícono.
