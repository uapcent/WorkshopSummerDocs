https://editor.swagger.io/

```json
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
                  $ref: '#/components/schemas/Cart'
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
                  $ref: '#/components/schemas/Cart'
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
                $ref: '#/components/schemas/Cart'
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
                $ref: '#/components/schemas/Cart'
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
  '/submitCart/{cartId}':
    put:
      tags:
        - Carts
      summary: Submits a cart
      description: a cart is submitted for purchase
      operationId: submitCart
      parameters:
        - name: cartId
          in: path
          required: true
          schema:
            type: integer
            format: long
      requestBody:
        description: show data required to create a show
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Cart'
      responses:
        '200':
          description: Cart is updated
        '404':
          description: Not found error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                msg: Not found ID
                error_code: 404
        '500':
          description: error response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
  /carts/updateStock:
    put:
      tags:
        - Carts
      summary: Update stock in multiple carts
      description: Update stock of products in multiple carts
      operationId: updateProductsFromCarts
      requestBody:
        description: Data required to update stock in multiple carts
        required: true
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Product'
      responses:
        '200':
          description: Products updated in multiple carts
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Cart'
  '/carts/{cartId}/addProduct/{productId}':
    put:
      tags:
        - Carts
      summary: Add a product to a cart
      description: Create a new product in a cart
      operationId: addProductToCart
      parameters:
        - name: cartId
          in: path
          required: true
          schema:
            type: integer
            format: int64
          description: ID of the cart
        - name: productId
          in: path
          required: true
          schema:
            type: integer
            format: int64
          description: ID of the product
        - name: quantity
          in: query
          required: true
          schema:
            type: integer
          description: Quantity of the product to add
      responses:
        '200':
          description: New product is added to the cart
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Cart'
        '400':
          description: Bad Request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
  '/carts/{idCart}':
    delete:
      tags:
        - Carts
      summary: deletes a cart
      description: deletes a specific cart
      operationId: deleteCarts
      parameters:
        - name: idCart
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
                  $ref: '#/components/schemas/Cart'
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
  '/carts/{cartId}/product/{productId}':
    delete:
      tags:
        - Carts
      summary: deletes a product
      description: deletes a specific product
      operationId: deleteProduct
      parameters:
        - name: cartId
          in: path
          required: true
          schema:
            type: integer
            format: long
        - name: productId
          in: path
          required: true
          schema:
            type: integer
            format: long
      responses:
        '200':
          description: Ok
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Cart'
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
    Cart:
      type: object
      properties:
        id:
          type: integer
          format: long
          description: UUID of each shopping cart
        invalidProducts:
          type: array
          items:
            type: integer
          description: List of invalid product IDs
        products:
          type: object
          additionalProperties:
            type: integer
          description: Map of product IDs to quantities
        userId:
          type: integer
          format: long
          description: ID of the user associated with the cart
        status:
          type: string
          description: Status of the shopping cart
          enum:
            - DRAFT
            - SUBMITTED
        finalPrice:
          type: number
          format: decimal
          minimum: 0
          description: Final price of the cart
        finalWeight:
          type: number
          format: decimal
          minimum: 0
          description: Final weight of the cart
      required:
        - id
        - userId
        - status
        - finalPrice
        - finalWeight
    Product:
      type: object
      properties:
        id:
          type: integer
          format: long
          description: ID of the product
        price:
          type: number
          format: decimal
          minimum: 0
          description: Price of the product
        weight:
          type: number
          format: decimal
          minimum: 0
          description: Weight of the product
        storageQuantity:
          type: integer
          description: Quantity available in storage
      required:
        - id
        - price
        - weight
        - storageQuantity
    ErrorResponse:
      type: object
      properties:
        msg:
          type: string
        error_code:
          type: integer

```