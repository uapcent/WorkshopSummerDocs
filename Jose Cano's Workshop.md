---
tags:
  - Formacion
---
Diagrama UML. 
NoSQL donde, como, diferencias?
Se pueden usar diagramas UML para noSQL para entender la lógica de la aplicación. 

El objetivo es aprender sobre la programación reactiva. 
4 microservicios para un sistema de gestión de transporte público. 
- Gestión de vehículos
- Rutas
- Ubicación de vehículos
- Gestión de pasajeros. 
- Microservicio de notificaciones. 

## Design Views
### System context
Provide a conceptual component and connector diagram of the system. This should include:
- Peripherial components that are not in this design
- Clear identification of the scope of the design 

| **IN SCOPE**             | description                                                                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| Gestión de rutas         | Gestiona la información de las rutas                                                                                      |
| Gestion de vehiculos     | Gestiona la información de los vehículos                                                                                  |
| Monitoreo en tiempo real | Recibe y procesa los datos de ubicación en tiempo real de los vehículos                                                   |
| Gestión de pasajeros     | Gestiona la información de los pasajeros y sus registros de viaje.                                                        |
| Notificaciones           | Envía notificaciones basadas en eventos del sistema                                                                       |
| Cola de mensajes         | Facilita la comunicación entre los microservicios mediante el uso de una cola de mensajes (por ejemplo, RabbitMQ o Kafka) |
Diseñar las entidades, modelo, etcetera. Mirar Domain Driven Development. Hexagonal Architecture??
Ver las entidades con las que trabajar, describir el funcionamiento, hacer open questions. 



![[EsquemaSistemaTransporte.canvas|EsquemaSistemaTransporte]]