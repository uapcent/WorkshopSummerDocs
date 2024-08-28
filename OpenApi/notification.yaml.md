
```yaml
openapi: 3.0.0
info:
  title: Notification service
  description: Configures and sends notifications
  license:
    name: Apache 2.0
    url: 'http://www.apache.org/licenses/LICENSE-2.0.html'
  version: 1.0.1
tags:
  - name: Notification service
    description: Configures and sends notifications
paths:
  '/notifications':
    post:
      tags:
        - Notifications
      summary: Configure new rules of notification
      description: Receives a new rule for sending notifications
      operationId: getAllLocations
      responses:
        '200':
          description: Ok
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/NotificationRule'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
components:
  schemas:
    NotificationRule:
      type: object
      properties:
        notificationType:
          type: integer
          format: long
          description: Reason for the notification
        severity:
          type: string
          description: Severity of the notification
          enum:
          - low
          - medium
          - high
        recipients:
          type: array
          description: List of people that will receive an email
          items:
            type: object
            properties:
              recipientId:
                type: string
                description: Unique identifier for the event
              recipientType:
                type: string
                description: Type of the event
                enum:
                  - passenger
                  - manager
                  - supervisor
              contact:
                type: string
                description: Email and/or phone number
        actions:
          type: array
          items:
            type: object
            properties:
              actionId:
                type: string
                description: Unique identifier for the event
              typeAction:
                type: string
                description: Type of the event
                enum:
                  - send_email
                  - ignore
              status:
                type: string
                description: Identifier of the stop where the event occurred
                enum:
                 - completed
                 - in_progress
                 - to_do
      required:
        - notificationType
        - severity
        - actions
    ErrorResponse:
      type: object
      properties:
        msg:
          type: string
        error_code:
          type: integer
```