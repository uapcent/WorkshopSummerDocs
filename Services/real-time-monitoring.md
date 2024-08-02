---
tags:
  - JCWorkshop
---
### Descripción
Este servicio recibirá y gestionará datos de ubicación en tiempo real de los [[vehicles-manager|vehículos]].

OpenApi document: [[monitoring.yaml]]
Original documentation: [[Ejercicio sistema de transporte.pdf#page=5]]

### Endpoints
-  `POST /location`: Recibir actualizaciones de ubicación de los vehículos.
- `GET /location/{vehicleId}`: Obtener la ubicación actual de un vehículo.

### Datos
Los datos de ubicación deben incluir ID del vehículo, latitud, longitud, y timestamp

#todo Duda, tenemos que procesar los datos, almacenarlos, o ambos?

Aquí tienes un ejemplo de una representación en JSON de los datos de monitoreo en tiempo real para un sistema de transporte público. Este ejemplo incluye la información básica sobre la ubicación y estado de un vehículo en tiempo real.

```json
{
  "vehicleId": "V-456",
  "timestamp": "2024-07-04T14:48:00Z",
  "location": {
    "latitude": 40.730610,
    "longitude": -73.935242
  },
  "speed": 45.0,
  "direction": "north",
  "routeId": "123",
  "passengerCount": 30,
  "status": "on_route",
  "events": [
    {
      "eventId": "E-001",
      "type": "stop_arrival",
      "stopId": "2",
      "timestamp": "2024-07-04T14:47:00Z"
    },
    {
      "eventId": "E-002",
      "type": "stop_departure",
      "stopId": "2",
      "timestamp": "2024-07-04T14:48:00Z"
    }
  ]
}
```

 Explicación del JSON:
1. vehicleId: Identificador único del [[vehicles-manager|vehículo]].
2. timestamp: Marca de tiempo en que se registró la información.
3. location: Ubicación actual del vehículo con coordenadas de latitud y longitud.
4. speed: Velocidad actual del vehículo en km/h.
5. direction: Dirección del movimiento del vehículo (norte, sur, este, oeste).
6. routeId: Identificador de la ruta que actualmente está siguiendo el vehículo.
7. passengerCount: Número actual de pasajeros a bordo del vehículo.
8. status: Estado actual del vehículo, por ejemplo, "on_route", "stopped", "off_route".
9. events: Lista de eventos recientes relacionados con el vehículo, cada uno con:
   - eventId: Identificador único del evento.
   - type: Tipo de evento, como "stop_arrival" (llegada a una parada), "stop_departure" (salida de una parada).
   - stopId: Identificador de la parada relacionada con el evento.
   - timestamp: Marca de tiempo en que ocurrió el evento.

---

