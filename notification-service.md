Microservicio de Notificaciones:

### Descripción
Este servicio enviará notificaciones basadas en ciertos eventos o umbrales alcanzados en el sistema.

Endpoints:
-  `POST /notifications`: Configurar nuevas reglas de notificación.

#todo eventos capturados por el sistema. Por ejemplo? Que habría que monitorizar?
Como se detecta una avería, o un retraso?
### Funciones 
Enviar notificaciones por email o a una cola de mensajes cuando se detecten eventos como retrasos significativos o interrupciones en el servicio.

Se ejecutará periódicamente, escaneará los valores de ciertos servicios y responderá según la configuración: 
Servicios que monitoriza:
- ª

#### Ejemplo JSON de una notificación de retraso

```json
{
  "notificationId": "N-002",
  "timestamp": "2024-07-04T15:10:00Z",
  "type": "delay",
  "title": "Retraso en la Ruta 123",
  "message": "El vehículo en la Ruta 123 está experimentando un retraso de 10 minutos debido a tráfico pesado. Agradecemos su paciencia.",
  "severity": "medium",
  "routeId": "123",
  "vehicleId": "V-456",
  "recipients": [
    {
      "recipientId": "U-124",
      "recipientType": "passenger",
      "contact": {
        "email": "passenger124@example.com",
        "phone": "+123456780"
      }
    }
  ],
  "actions": [
    {
      "actionId": "A-003",
      "type": "send_email",
      "status": "completed"
    }
  ]
}
```

 Explicación adicional del JSON:
- type: En este caso, el tipo de notificación es "delay" (retraso).
- message: El mensaje indica un retraso específico y la razón del mismo.
- recipients: Solo hay un destinatario en este ejemplo.
- actions: Una sola acción de envío de email ha sido completada.

Estos ejemplos pueden ser adaptados y extendidos según los requisitos específicos de tu sistema de gestión de transporte público, incluyendo más detalles sobre eventos específicos, formatos de contacto adicionales, y tipos de acciones realizadas.