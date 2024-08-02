
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
    get:
      tags:
        - Location
      summary: Get a summary of all the vehicles current location
      description: Complete
      operationId: getAllLocations
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