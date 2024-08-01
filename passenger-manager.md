---
tags:
  - JCWorkshop
---
Microservicio de gestión de pasajeros y de los viajes que han realizado.

### Descripción: 
Este servicio gestionará la información sobre los pasajeros y sus registros de viaje.

Endpoints:
 - `POST /passengers`: Registrar un nuevo pasajero.
 - `GET /passengers/{id}`: Obtener detalles de un pasajero por ID.
 - `POST /passengers/{id}/trips`: Registrar un nuevo viaje para un pasajero.
 - `GET /passengers/{id}/trips`: Obtener el historial de viajes de un pasajero.

### Datos: 
Los datos de pasajero deben incluir ID, nombre, y método de pago preferido.


Imaginamos que el usuario tiene una aplicación de viajes. A partir de ella, podrá:
- Registrar-se: Crear una nueva cuenta en el sistema
- Ver su perfil: Obtener detalles 
- Usar la aplicación como billete: Registrar viaje 
- Ver historial de viajes 

#### Ejemplo de Gestión de Pasajeros en JSON

```json
{
  "passengerId": "P-001",
  "name": "Juan Pérez",
  "email": "juan.perez@example.com",
  "phone": "+1234567890",
  "preferredPaymentMethod": "card",
  "registeredAt": "2024-01-15T09:00:00Z",
  "trips": [
    {
      "tripId": "T-1001",
      "routeId": "123",
      "vehicleId": "V-456",
      "startTime": "2024-07-04T08:00:00Z",
      "endTime": "2024-07-04T08:45:00Z",
      "startStop": "Estación Central",
      "endStop": "Plaza Norte",
      "fare": 2.50
    },
    {
      "tripId": "T-1002",
      "routeId": "123",
      "vehicleId": "V-456",
      "startTime": "2024-07-04T09:00:00Z",
      "endTime": "2024-07-04T09:45:00Z",
      "startStop": "Plaza Norte",
      "endStop": "Terminal Norte",
      "fare": 2.50
    }
  ]
}
```

Explicación del JSON:
1. **passengerId**: Identificador único del pasajero.
2. **name**: Nombre del pasajero.
3. **email**: Correo electrónico del pasajero.
4. **phone**: Número de teléfono del pasajero.
5. **preferredPaymentMethod**: Método de pago preferido del pasajero, por ejemplo, "card" (tarjeta) o "cash" (efectivo).
6. **registeredAt**: Fecha y hora en que el pasajero se registró en el sistema.
7. **trips**: Lista de viajes realizados por el pasajero, cada uno con:
	- **tripId**: Identificador único del viaje.
	- **routeId**: Identificador de la ruta que siguió el viaje.
	- **vehicleId**: Identificador del vehículo utilizado.
	- **startTime**: Hora de inicio del viaje.
	- **endTime**: Hora de finalización del viaje.
	- **startStop**: Nombre de la parada de inicio.
	- **endStop**: Nombre de la parada final.
	- **fare**: Tarifa pagada por el viaje.


#### Ejemplo de Registro de un Nuevo Pasajero

```json
{
  "passengerId": "P-002",
  "name": "Ana Gómez",
  "email": "ana.gomez@example.com",
  "phone": "+1987654321",
  "preferredPaymentMethod": "cash",
  "registeredAt": "2024-07-01T10:30:00Z"
}
```

Explicación del JSON:
- Este ejemplo muestra cómo se registraría un nuevo pasajero en el sistema, con toda la información básica pero sin viajes registrados aún.

#### Ejemplo de Registro de un Nuevo Viaje

```json
{
  "tripId": "T-1003",
  "routeId": "124",
  "vehicleId": "V-457",
  "passengerId": "P-002",
  "startTime": "2024-07-04T10:00:00Z",
  "endTime": "2024-07-04T10:30:00Z",
  "startStop": "Estación Norte",
  "endStop": "Centro Comercial",
  "fare": 3.00
}
```

Explicación del JSON:
- **tripId**: Identificador único del viaje.
- **routeId**: Identificador de la ruta seguida.
- **vehicleId**: Identificador del vehículo utilizado.
- **passengerId**: Identificador del pasajero que realizó el viaje.
- **startTime**: Hora de inicio del viaje.
- **endTime**: Hora de finalización del viaje.
- **startStop**: Nombre de la parada de inicio.
- **endStop**: Nombre de la parada final.
- **fare**: Tarifa pagada por el viaje.

Estos ejemplos pueden ser adaptados y extendidos según los requisitos específicos de tu sistema de gestión de transporte público, incluyendo más detalles sobre métodos de pago, información adicional de contacto, y otros atributos relevantes.