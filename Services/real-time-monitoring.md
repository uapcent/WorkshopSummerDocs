---
tags:
  - JCWorkshop
---
### Descripción
Este servicio recibirá y gestionará datos de ubicación en tiempo real de los [[vehicles-manager|vehículos]].

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

```yaml
openapi: 3.0.0
info:
  title: Route management microservice
  description: Service to handle routes of vehicles
  license:
    name: Apache 2.0
    url: 'http://www.apache.org/licenses/LICENSE-2.0.html'
  version: 1.0.1
tags:
  - name: Real Time Monitoring
    description: Everything about routes
paths:
  '/location':
    post:
      tags:
        - Location
      summary: Post the current what?
      description: Complete
      operationId: TODO
      responses:
        '200':
          description: Ok
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Metric'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
  '/location/{vehicleId}':
    get:
      tags:
        - Location
      summary: get the current location of a vehicle
      description: returns the information of a single vehicle
      operationId: getLocationByVehicleId
      parameters:
        - name: vehicleId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Ok
          content:
            application/json:
              schema:
                type: object
                items:
                  $ref: '#/components/schemas/Metric'
        '404':
          description: not found error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
components:
  schemas:
    Metric:
      type: object
      properties:
        vehicleId:
          type: integer
          format: long
          description: UUID of the monitored vehicle
        timestamp:
          type: string
          description: Time the metric was recorded
        location:
          type: string
          description: latitude & longitude
        speed:
          type: number
          description: Speed of the vehicle when the metric was recorded
        direction:
          type: string
          description: Time the metric was recorded
          enum: 
            - North
            - NorthEast
            - East
            - SouthEast
            - South
            - SouthWest
            - West
            - NorthWest
        routeId: 
          type: string
          description: The assigned route the vehicle was following
        passengerCount:
          type: integer
          description: Number of passengers currently on the train
        status:
          type: string
          description: Current status of the vehicle
          enum:
            - parked
            - on_route
        events:
          type: array
          items:
            type: object
            properties:
              eventId:
                type: string
                description: Unique identifier for the event
              type:
                type: string
                description: Type of the event
                enum:
                  - stop_arrival
                  - stop_departure
              stopId:
                type: string
                description: Identifier of the stop where the event occurred
              timestamp:
                type: string
                description: Time the event was recorded
                format: date-time
          description: List of stops sorted by driving order.
        schedule:
          type: array
          items: 
            type: string
          description: List containing the schedule for weekdays and weekends
      required:
        - routeId
    ErrorResponse:
      type: object
      properties:
        msg:
          type: string
        error_code:
          type: integer

```