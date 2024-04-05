----
- Tags: #tecnologías
-----
# Modulo **datetime**

La biblioteca **datetime** en Python es una de las principales herramientas para trabajar con fechas y horas. 

- Los **tipos de datos principales**: *datetime* incluye varios tipos de datos, como *date* (Para fechas), *time* (Para horas), *datetime* (Para fechas y horas combinadas) y *timedelta* (Para representar diferencias de tiempo).
- **Manipulación de fechas y horas**: Permite realizar operaciones como suamr o restar días, semanas, o meses a una fecha, comparar fechas, o extraer componenetes como el día, mes, o año de una fecha específica.
- **Zonas Horarias**: A través del módulo **pytz** que se integra con datetime, se pueden manejar fechas y horas en diferentes zonas horarias, lo que es crucial para aplicaciones que requieren precisión a nivel global.
- **Formateo y análisis**: Datetime permite convertir fechas y horas a srtings y viceversa, utilizando códigos de formato específicos. Esto es útil para mostrar fechas y horas en formatos legibles o para parsear strings que representan fechas/horas.
- **Facilidad de Uso**: A pesar de su potencia y flexibilidad, datetime es relativamente fácil de usar, lo que la hace accesible incluso para programadores principiantes.
- **Amplia aplicación**: Desde registros de eventos hasta cálculos de períodos de tiempo, datetime es indispensable en una variedad de aplicaciones, como sistemas de reservas, análisis de datos temporales, y más.

```python
import datetime 

# Get actual time 
now = datetime.datetime.now()
year = now.year
month = now.month
day = now.day
hour = now.hour
minutes = now.minute
seconds = now.second

# Create a date
my_date = datetime.date(2023, 12, 12)

# Create a time 
my_time = datetime.time(14, 59, 4)

# Create a datetime
my_datetime = datetime.datetime(2023, 6, 12, 14, 59, 4)


```