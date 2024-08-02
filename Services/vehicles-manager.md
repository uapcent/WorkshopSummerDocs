---
tags:
  - JCWorkshop
---
Servicio que almacena y gestiona la información de los vehículos i las [[routes-manager|rutas]] que tienen asignadas, permitiendo operaciones CRUD.

### Endpoints:
 - `POST /vehicles`: Registrar un nuevo vehículo.
 - `GET /vehicles/{id}`: Obtener detalles de un vehículo por ID.
 - `PUT /vehicles/{id}`: Actualizar información de un vehículo.
 - `DELETE /vehicles/{id}`: Eliminar un vehículo.

### Datos
Los datos de vehículo deben incluir ID, número de placa, capacidad, y estado actual (en servicio, en mantenimiento, etc.).

Aquí tienes un ejemplo de una representación en JSON de un vehículo utilizado en un sistema de transporte público. Este ejemplo incluye información básica del vehículo, como su ID, número de placa, capacidad, y estado actual.

```json
{
  "vehicleId": "V-456",
  "licensePlate": "ABC-1234",
  "capacity": 40,
  "currentStatus": "in_service",
  "type": "bus",
  "routeId": "123",
  "lastMaintenance": "2024-06-15",
  "currentLocation": {
    "latitude": 40.730610,
    "longitude": -73.935242
  },
  "driver": {
    "driverId": "D-789",
    "name": "John Doe",
    "contact": "+1234567890"
  }
}
```

 Explicación del JSON:
1. vehicleId: Identificador único del vehículo.
2. licensePlate: Número de placa del vehículo.
3. capacity: Capacidad de pasajeros que puede transportar el vehículo.
4. currentStatus: Estado actual del vehículo, que puede ser "in_service", "out_of_service", "maintenance", etc.
5. type: Tipo de vehículo, por ejemplo, "bus", "tram", "train".
6. routeId: Identificador de la [[routes-manager|ruta]] que actualmente está asignada al vehículo.
7. lastMaintenance: Fecha de la última vez que el vehículo recibió mantenimiento.
8. currentLocation: Ubicación actual del vehículo con coordenadas de latitud y longitud.
9. driver: Información del conductor asignado al vehículo, incluyendo:
   - driverId: Identificador único del conductor.
   - name: Nombre del conductor.
   - contact: Información de contacto del conductor.

#### Ejemplo JSON de un vehículo en mantenimiento
```json
{
  "vehicleId": "V-789",
  "licensePlate": "XYZ-5678",
  "capacity": 50,
  "currentStatus": "maintenance",
  "type": "tram",
  "lastMaintenance": "2024-07-01",
  "maintenanceDetails": {
    "scheduledBy": "Jane Smith",
    "scheduledDate": "2024-07-10",
    "details": "Routine check and brake replacement"
  }
}
```

 Explicación adicional del JSON:
1. maintenanceDetails: Información adicional sobre el mantenimiento programado:
   - scheduledBy: Nombre de la persona que programó el mantenimiento.
   - scheduledDate: Fecha programada para el mantenimiento.
   - details: Descripción de las tareas de mantenimiento que se realizarán.

Estos ejemplos pueden ser adaptados y extendidos según los requisitos específicos de tu sistema de gestión de transporte público, incluyendo más detalles como registros de mantenimiento anteriores, información adicional del conductor, y otros atributos relevantes.