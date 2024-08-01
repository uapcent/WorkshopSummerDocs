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
  - name: Routes
    description: Everything about routes
paths:
  '/routes':
    post:
      tags:
        - Routes
      summary: Create a new route
      description: Receives the json with the information of a route and creates it on the service
      operationId: createNewRoute
      responses:
        '200':
          description: Ok
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Route'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
  '/routes/{routeId}':
    get:
      tags:
        - Routes
      summary: get route
      description: returns the information of a single route
      operationId: getRouteById
      parameters:
        - name: routeId
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
                type: array
                items:
                  $ref: '#/components/schemas/Route'
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
    put:
      tags:
        - Routes
      summary: Update the information of a route
      description: Receives the information of a route and updates it in the service
      operationId: updateRouteById
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            type: integer
            format: long
      responses:
        '200':
          description: Route successfully updated
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Route'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
    delete:
      tags:
        - Routes
      summary: Delete a route
      description: Deletes a route from the service
      operationId: deleteRouteById
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            type: integer
            format: long
      responses:
        '200':
          description: Route successfully deleted
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Route'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
components:
  schemas:
    Route:
      type: object
      properties:
        routeId:
          type: integer
          format: long
          description: UUID of each shopping cart
        routeName:
          type: string
          items:
            type: integer
          description: Name of the route - "Ruta Centro-Norte"
        stops:
          type: array
          items:
            type: object
            properties:
                  stopId:
                    type: integer
                  stopName:
                    type: string
                  coordinates: 
                    type: string
                  arrivalTimes:
                    type: array
                    items: 
                      type: string
          description: List of stops sorted by driving order.
        schedule:
          type: array
          items: 
            type: string
          description: List containing the schedule for weekdays and weekends
      required:
        - routeId
    Stop:
     type: object
     properties:
      stopId: 
       type: integer
    ErrorResponse:
      type: object
      properties:
        msg:
          type: string
        error_code:
          type: integer

    

```