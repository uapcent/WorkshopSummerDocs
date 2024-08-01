---
tags:
  - JCWorkshop
---
Servicio usado para gestionar las rutas de [[vehicles-manager|vehículos]]. 
#### Ejemplo de Ruta en JSON

Aquí tienes un ejemplo de una representación en JSON de una ruta de transporte público. Este ejemplo incluye la información básica de una ruta, como el ID, nombre de la ruta, lista de paradas, y horarios:

```json
{
  "routeId": "123",
  "routeName": "Ruta Centro-Norte",
  "stops": [
    {
      "stopId": "1",
      "stopName": "Estación Central",
      "coordinates": {
        "latitude": 40.712776,
        "longitude": -74.005974
      },
      "arrivalTimes": [
        "08:00",
        "08:30",
        "09:00"
      ]
    },
    {
      "stopId": "2",
      "stopName": "Plaza Norte",
      "coordinates": {
        "latitude": 40.730610,
        "longitude": -73.935242
      },
      "arrivalTimes": [
        "08:15",
        "08:45",
        "09:15"
      ]
    },
    {
      "stopId": "3",
      "stopName": "Terminal Norte",
      "coordinates": {
        "latitude": 40.748817,
        "longitude": -73.985428
      },
      "arrivalTimes": [
        "08:30",
        "09:00",
        "09:30"
      ]
    }
  ],
  "schedule": {
    "weekdays": {
      "startTime": "06:00",
      "endTime": "22:00",
      "frequencyMinutes": 15
    },
    "weekends": {
      "startTime": "07:00",
      "endTime": "20:00",
      "frequencyMinutes": 20
    }
  }
}
```

Explicación del JSON:
1. **routeId**: Identificador único de la ruta.
2. **routeName**: Nombre descriptivo de la ruta.
3. **stops**: Lista de paradas en la ruta, cada una con:
   - stopId: Identificador único de la parada.
   - stopName: Nombre de la parada.
   - coordinates: Coordenadas geográficas de la parada (latitud y longitud).
   - arrivalTimes: Horarios de llegada del vehículo a la parada.
4. **schedule**: Horarios de operación de la ruta, diferenciados entre días de semana y fines de semana:
   - weekdays: Horarios y frecuencia de operación durante los días de semana.
   - weekends: Horarios y frecuencia de operación durante los fines de semana.

Este ejemplo puede ser adaptado según los requisitos específicos de tu sistema de gestión de transporte público, incluyendo más detalles como tipos de vehículos, información adicional de las paradas, y otros atributos relevantes.