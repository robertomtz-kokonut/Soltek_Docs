---
title: Soltek API

language_tabs:
  - java: Request Body
  - javascript: Success Response
  - csharp: Error Response

toc_footers:
  - <a href='http://kokonutstudio.com/'>Kokonut Studio</a>

search: true
---

# Soltek API

## URL

Ambiente        | Value
----------------|----------------------------------------
DEV Kokonut | https://newsoltek.kokonutstudio.com
QA Kokonut  | https://soltek-api-qa.kokonutstudio.com
QA Cliente  | https://soltek-api.kokonutstudio.com
Producción  | https://api.soltek.com.mx


## Estatus de usuarios
Se muestra listado de los estatus disponibles para un usuario.

ID | Estatus 
---|----------------------
1  | Activo
2  | Suspendido
3  | Deshabilitado
4  | Necesita activación


## Tipo de usuarios 
Se muestra listado de los tipos de usuarios.

id  | Rol
----|--------------------
 1  | Super Admin
 2  | Admin Cliente
 3  | Admin Independiente
 4  | Supervisor Soltek
 5  | Instalador Soltek
 6  | Supervisor
 7  | Instalador
 8  | Chofer
 9  | Moderador
 10 | Moderador Soltek


## Estatus de vehículos
Se muestra listado de los estatus disponibles para un vehículo.

ID | Estatus 
---|----------------------
1  | Activo
2  | Deshabilitado


# User
## Registro de usuarios

> Registro de usuarios

````java
{
    "email": "test@doc.com",
    "firebase_id": "ccalp5aypvU...",
    "last_name": "Doc",
    "name": "Test",
    "password": "123Qwe1",
    "password_confirmation": "123Qwe1"
}
```
```javascript
{
    "success": 1,
    "message": "",
    "data": {
        "token_type": "Bearer",
        "expires_in": 31535998,
        "access_token": "eyJ0eX...",
        "refresh_token": "def50...",
        "user_type": "3"
    }
}
```
```csharp
{
    "success": 0,
    "message": "Correo electronico ya registrado",
    "data": null
}
{
    "success": 0,
    "message": "Hacen falta datos para completar el registro",
    "data": null
}
```

Este endpoint registra un usuario de tipo 3 (Admin Independiente) a través de un correo electrónico y contraseña.

HTTP Request  | Name Endpoint | Endpoint
--------------|---------------|-----------------------
POST          | create user   | {{url}}/api/register

### Headers
No requerido.

### Body
Key                   | Descripción                 | Type   | Mandatory
----------------------|-----------------------------|--------|-------------
name                  | Nombre del usuario          | String | Obligatorio
last_name             | Apellido del usuario        | String | Opcional
email                 | Correo del usuario          | String | Obligatorio
password              | Contraseña del usuario      | String | Obligatorio
password_confirmation | Confirmación de Contraseña  | String | Obligatorio
firebase_id           | Token de Firebase Messaging | String | Opcional



## Inicio de sesión
> Inicio de sesión

````java
{
    "username": "test@doc.com",
    "password": "123Qwe1",
    "firebase_id": "ccalp5aypvU..."
}
```
```javascript
{
    "success": 1,
    "message": "",
    "data": {
        "token_type": "Bearer",
        "expires_in": 31536000,
        "access_token": "eyJ0eX...",
        "refresh_token": "def5...",
        "user_type": "3"
    }
}
```
```csharp
{
    "error": "invalid_credentials",
    "message": "The user credentials were incorrect."
}
```

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|--------------------
POST          |login          | {{url}}/api/login 

### Header
No aplica.

### Body
Key                   | Descripción                 | Type   | Mandatory
----------------------|-----------------------------|--------|-------------
username              | Correo del usuario          | String | Obligatorio
password              | Contraseña del usuario      | String | Obligatorio
firebase_id           | Token de Firebase Messaging | String | Opcional



## Cerrar sesión
>Cerrar sesión: 

```java
{
    "firebase_id": "ccalp5aypvU..."
}
```
```javascript
{
    "success": 1,
    "message": "Sesión cerrada correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}

```

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|-----------
POST          | logout        | {{url}}/api/logout

### Headers
Key          | Value 
-------------|-----
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key         | Value  | Mandatory
------------|--------|------------
firebase_id | String | Obligatorio




## Mostrar perfil
>Mostrar perfil:

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": null,
    "data": [
        {
            "id": "eyJpdiI6Imw4NDY0...",
            "name": "Test",
            "last_name": "Doc",
            "email": "test@doc.com",
            "image": null,
            "company_id": "eyJpdiI6IjF4bElyVHU3cT...",
            "company_name": "test@doc.com",
            "user_type": "3",
            "user_type_description": "Admin Ind",
            "is_principal": null,
            "created_at": {
                "date": "2019-12-10 15:20:08.000000",
                "timezone_type": 3,
                "timezone": "America/Mexico_City"
            }
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request  | Name Endpoint | Endpoint
--------------|---------------|---------------------
GET           | show profile  | {{url}}/api/profile

### Headers
Key          | Value 
-------------|-----------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.



## Editar perfil
>Editar perfil:

```java
{
    "name": "Test",
    "last_name": "Doc Edited",
    "password": "123Qwe1",
    "password_confirmation": "123Qwe1"
}
```
```javascript
{
    "success": 1,
    "message": "Actualización del usuario correcta",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Hacen falta datos para completar el registro",
    "data": null
}
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request  | Name Endpoint  |  Endpoint
--------------|----------------|----------------------
POST          | update profile | {{url}}/api/update

### Headers
Key          | Value 
-------------|----------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
name                  | String | 0
last_name             | String | 0
email                 | String | 0
password              | String | 0
password_confirmation | String | 0



## Recuperar contraseña
>Response:

```java
{
    "email": "test@doc.com"
}
```
```javascript
{
    "success": 1,
    "message": "Correo de recuperación enviado exitosamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "El correo electronico no se encuentra registrado",
    "data": null
}

{
    "success": 0,
    "message": "El correo de recuperación no pudo ser enviado",
    "data": null
}
```

HTTP Request  | Name Endpoint    |  Endpoint
--------------|------------------|--------------------------------
POST          | restore password | {{url}}/api/restore_password 

### Headers
Key          | Value 
-------------|--------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key      | Value  | Mandatory
---------|--------|------------
email    | String | 1





# Drivers

## Crear Chofer
>Crear Chofer:

```java
// Ej. Admin independiente
{
    "full_name": "Chofer Prueba Uno",
    "driver_number": "001001"
}
// Ej. Admin cliente
{
    "full_name": "Chofer Prueba Uno",
    "driver_number": "001001",
    "base_id": "eyJpdiI..."
}
// Ej. Super Admin, Admin Soltek
{
    "full_name": "Chofer Prueba Uno",
    "driver_number": "001001",
    "base_id": "eyJpdiI...",
    "company_id": "edsSAiI..."
}
```
```javascript
{
    "success": 1,
    "message": "Chofer creado con éxito",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Hacen falta datos para crear el chofer",
    "data": null
}
{
    "success": 0,
    "message": "No se pudo crear el chofer",
    "data": null
}
```

### Description
Crea a un usuario tipo "Chofer" y lo asocia a una compañía en específico.

### Request 
HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|-------------------------
POST          | Create driver | {{url}}/api/create_driver

### Headers
Key          | Value 
-------------|---------------------------
Autorization | Bearer eyJ0eXAiOiJK...

### Body
Key           | Value  | Mandatory   | Description
--------------|--------|-------------|------------------------------------------------------------
full_name     | String | Obligatorio | Nombre completo del chofer.
driver_number | String | Obligatorio | Número de chofer.
base_id       | String | Opcional    | ID encriptado de la base donde se asociará al chofer.
company_id    | String | Opcional    | ID encriptado de la compañía donde se asociará al chofer.





## Eliminar chofer
>Eliminar chofer:

```java
{
    "status": 3,
    "user_id": "eyJpdiI6ImNU..."
}
```
```javascript
{
    "success": 1,
    "message": "Usuario manejado correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "El usuario no existe",
    "data": null
}
{
    "success": 0,
    "message": "Hacen falta datos para completar el registro", // TODO: Fix this error message.
    "data": null
}
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint |  Endpoint
-------------|---------------|---------------------------------
POST         | manage user   | {{url}}/api/staff/manage_user

### Headers
Key          | Value 
-------------|---------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key     | Value  | Description                                                         | Mandatory
--------|--------|---------------------------------------------------------------------|------------
user_id | String | ID en forma encriptada del usuario.                                 | 1
status  | Int    | 1 para activar usuario, 2 para suspender y 3 para eliminar usuario. | 1



## Mostrar choferes
>Mostar choferes:

```java
// No aplica.
```
```javascript
{
    "success": 1,
    "message": null,
    "data": [
        {
            "user_id": "eyJpdiI6Il...",
            "name": "Test Chofer",
            "last_name": null,
            "driver_number": "002",
            "status": "1",
            "company": "DOCUMENTATION",
            "base": "Base_001",
            "incidents": 179,
            "score": 100,
            "status_description": "Active"
        },
        {
            "user_id": "eyJpdiI6IjRTR...",
            "name": "Test Chofer",
            "last_name": null,
            "driver_number": "003",
            "status": "1",
            "company": "DOCUMENTATION",
            "base": "Base_001",
            "incidents": 179,
            "score": 100,
            "status_description": "Active"
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

<aside class="notice">
    Este servicio puede ser llamado con un parámetro extra en el URL para poder obtener los choferes de una compañía en específico. Esto es para que los 
    trabajadores Soltek puedan acceder a esta información.
</aside>

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|---------------------------------
GET           | show drivers  | {{url}}/api/staff/show-drivers
GET           | show drivers  | {{url}}/api/staff/show-drivers/{companyId}

### Headers
Key  | Value 
-----|-----
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido



## Actualizar chofer
>Actualizar chofer:

```java
{
    "user_id": "eyJpdiI6I...",
    "name": "Test Chofer",
    "driver_id": "004",
    "base_id": "eyJpd...",
}
```
```javascript
{
    "success": 1,
    "message": "Actualización del usuario correcta",
    "data":null
}
```
```csharp
{
    "message": "Unauthenticated."
}
{
    "success": 0,
    "message": "Error al actualizar el usuario",
    "data": null
}
{
    "success": 0,
    "message": "Hacen falta datos para completar el registro",
    "data": null
}
```

### Description
Actualiza la información de un usuario tipo "Chofer".

### Request 
HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|-------------------------
POST          | Create driver | {{url}}/api/staff/update/driver

### Headers
Key          | Value 
-------------|---------------------------
Autorization | Bearer eyJ0eXAiOiJK...

### Body
Key       | Value  | Mandatory   | Description
----------|--------|-------------|-----------------------------------------------------------
user_id   | String | Obligatorio | ID encriptado del chofer
name      | String | Opcional    | Nombre completo del chofer.
driver_id | String | Opcional    | Número de chofer.
base_id   | String | Opcional    | ID encriptado de la base donde se asociará al chofer.





# Bases
## Mostrar bases

```java
// No aplica.
```
```javascript
// Sin bases asociadas
{
    "success": 1,
    "message": null,
    "data": []
}
// Compañía con bases asociadas
{
    "success": 1,
    "message": null,
    "data": [
        {
            "company_id": "eyJpdiI6Im...",
            "company_name": "ARK Studio",
            "base_id": "eyJpdiI6IlRWV...",
            "base_name": "ark_001",
            "base": "ark_001",
            "vehicles": [...], // En aplicaciones, ignorar este atributo
            "users": [...] // En aplicaciones, ignorar este atributo
        },
        {
            "company_id": "eyJpdi...",
            "company_name": "ARK Studio",
            "base_id": "eyJpdiI6IjVjU...",
            "base_name": "ark_002",
            "base": "ark_002",
            "vehicles": [...], // En aplicaciones, ignorar este atributo
            "users": [...] // En aplicaciones, ignorar este atributo
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

<aside class="notice">
    Este servicio puede ser llamado con un parámetro extra en el URL para poder obtener las bases de una compañía en específico. Esto es para que los 
    trabajadores Soltek puedan acceder a esta información.
</aside>

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|---------------------------------
GET           | show base     | {{url}}/api/staff/get-base/
GET           | show base     | {{url}}/api/staff/get-base/{companyId}

### Headers
Key          | Value 
-------------|---------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No aplica





# Vehicles
## Mostrar marcas y modelos
>Mostrar marcas y modelos:

```java
// No aplica.
```
```javascript
// Sin bases asociadas
{
    "success": 1,
    "message": null,
    "data": [
        {
            "brand": "KENWORTH",
            "brand_id": 1,
            "models": [
                {
                    "id": 1,
                    "description": "W990"
                },
                {
                    "id": 2,
                    "description": "T680"
                }
            ]
        },
        {
            "brand": "FREIGHTLINER",
            "brand_id": 2,
            "models": [
                {
                    "id": 14,
                    "description": "COLUMBIA"
                }
            ]
        }
    ]
}
```
```csharp
{
    "message": "Unauthenticated."
}
```

Muestra los modelos correspondientes a cada marca. Este servicio se utiliza para seleccionar marca y modelo en el proceso para dar alta vehículos

HTTP Request  | Name Endpoint     | Endpoint
--------------|-------------------|-----------
GET           | show cat vehicles | {{url}}/api/staff/catalog-vehicles

### Headers
Key          | Value 
-------------|-----------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido



## Crear vehículo
>Crear vehículo: 

```java 
{
    "base_id": "eyJpdiI6IkM3U0...",
    "fk_vehicle_model": 1,
    "tanks": 3,
    "vehicle_economic": "100",
    "vehicle_id": "100100"
}
```
```javascript
{
    "success": 1,
    "message": "Vehículo creado correctamente",
    "data": null
}
```
```csharp
{
    "success": 1,
    "message": "No se pudo crear el vehiculo",
    "data": null
}
```

HTTP Request  | Name Endpoint  |  Endpoint
--------------|----------------|---------------------------
POST          | create vehicle | {{url}}/api/staff/vehicle

### Headers
Key          | Value 
-------------|--------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key              | Description       | Mandatory
-----------------|-------------------|------------
vehicle_id       | Numero de serie   | 1
tanks            | Numero de tanques | 1
vehicle_economic | Numero económico  | 0
fk_vehicle_model | Modelo ID         | 1
base_id          | Base ID           | 0
company_id       | Compañía asociada | 0

Si no es enviado el parámetro company_id, entonces el vehículo es asociado a la compañía del usuario que realizó la petición



## Eliminar vehículo
>Eliminar vehículo:

```java
{
    "vehicle_id": "eyJpdiI6Ik9x...",
    "status": 3
}
```
```javascript
{
    "success": 1,
    "message": "Vehículo manejado correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Hubo un error al manejar vehículo",
    "data": null
}
```

HTTP Request | Name Endpoint  | Endpoint
-------------|----------------|----------------------------------
POST         | manage_vehicle | {{url}}/api/staff/manage_vehicle

### Headers
Key          | Value 
-------------|---------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key        | Description                                                            | Mandatory
-----------|------------------------------------------------------------------------|------------
vehicle_id | ID encriptado del vehículo a eliminar                                  | 1
status     | 1 si se requiere activar, 2 si se requiere suspender y 3 para eliminar | 1



## Mostrar vehículos
>Mostrar vehículos:

```java
// No aplica.
```
```javascript
{
    "success": 1,
    "message": "Consulta de vehículo exitosa",
    "data": {
        "154": [
            {
                "id_vehicle": "eyJpdiI6ImZaekVUejRHeF...",
                "company_id": "eyJpdiI6Ik92T2ZZNGZX...",
                "company_name": "ARK Studio",
                "serial_number": "001001",
                "economic_number": "001",
                "base": {
                    "base_id": "eyJpdiI6...",
                    "base_description": "ARK_001"
                },
                "model_vehicle_description": "W990",
                "model_vehicle_id": "1",
                "vehicle_brand_description": "KENWORTH",
                "vehicle_brand_id": "1",
                "tanks": "2",
                "vehicle_status_id": "1",
                "installed_kits": [
                    {
                        "id": "1",
                        "name": "Antisifon Tanksafe Standard"
                    },
                    {
                        "id": "2",
                        "name": "Antisifon Tanksafe Impregnable"
                    }
                ],
                "supervised": 1,
                "created_at": "19-12-09 02:12:59",
                "updated_at": "19-12-09 02:12:59",
                "incidents": 3,
                "vehicle_status_description": "Active"
            },
            {
                "id_vehicle": "eyJpdiI6IlYwb0d2Uk...",
                "company_id": "eyJpdiI6InFXR0dWcG...",
                "company_name": "ARK Studio",
                "serial_number": "002002",
                "economic_number": "002",
                "base": {
                    "base_id": "eyJpdiI6...",
                    "base_description": "ARK_002"
                },
                "model_vehicle_description": "COLUMBIA",
                "model_vehicle_id": "14",
                "vehicle_brand_description": "FREIGHTLINER",
                "vehicle_brand_id": "2",
                "tanks": "1",
                "vehicle_status_id": "1",
                "installed_kits": [],
                "supervised": 0,
                "created_at": "19-12-09 04:12:28",
                "updated_at": "19-12-09 04:12:28",
                "incidents": 0,
                "vehicle_status_description": "Active"
            }
        ]
    }
}
```
```csharp
{
    "message": "Unauthenticated."
}
```

HTTP Request | Name Endpoint | Endpoint
-------------|---------------|-------------------------------------------------------------
POST         | show vehicles | {{url}}/api/staff/vehicle/all/all/all
POST         | show vehicles | {{url}}/api/staff/vehicle/{companyId}/{vehicleId}/{userId}

### Headers
Key          | Value 
-------------|---------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### URL
Si se desea consultar la información global de la compañía utilizar al final: api/staff/vehicle/all/all/all.
Si se desea consultar información de compañías, vehículos o usuario en especifico, utilizar al final de URL: api/staff/vehicle/{company_id}/{vehicle_id}/{user_id}



## Actualizar vehiculo
>Actualizar vehiculo: 

```java
{
  "base_id": "eyJpd...",
  "fk_vehicle_model": 1,
  "tanks": 2,
  "vehicle_economic": "001",
  "vehicle_id": "001001"
}
```
```javascript
{
    "success": 1,
    "message": "Los datos se actualizaron correctamente",
    "data": null
}
```
```csharp
{
    "success": 1,
    "message": "Hubo un error al actualizar vehiculo",
    "data": null
}
```

HTTP Request | Name Endpoint  |  Endpoint
-------------|----------------|----------------------------------------
PUT          | update vehicle | {{url}}/api/staff/vehicle/{vehicleId}

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### URL
Es necesario pasar vehicle_id (ID de vehiculo, NO numero de serie) al final de la URL del endpoint

### Body
Key              | Description              | Mandatory
-----------------|--------------------------|-----------
vehicle_id       | Numero de serie          | Opcional
tanks            | Numero de tanques        | Opcional
vehicle_economic | Numero economico         | Opcional
fk_vehicle_model | Modelo id                | Opcional
base_id          | ID encriptado de la base | Opcional






# Company
## Mostrar compañías
>Mostrar compañías: 

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": null,
    "data": [
        {
            "name": "Test",
            "active": 1,
            "id_company": "eyJpdiI6IjNrWEl5W..."
        },
        {
            "name": "Roberto Kokonut",
            "active": 1,
            "id_company": "eyJpdiI6IlJuZkhvZ..."
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint  |  Endpoint
-------------|----------------|----------------------------------------
GET          | show companies | {{url}}/api/staff/show-companies/2

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No aplica





# Notifications

## Mostrar notificaciones
>Mostrar notificaciones: 

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": "Envio de notificación correcto",
    "data": {
        "total": 82,
        "actual_page": 9,
        "per_page": 10,
        "items": [
            {
                "push_id": "559",
                "title": "Alta de vehículo",
                "image": null,
                "was_read": "1",
                "created_at": "2019-12-09 14:45:59",
                "users": {
                    "installer_name": null,
                    "supervisor_name": null,
                    "driver_name": null
                },
                "installation_point_details": null,
                "vehicle": {
                    "serial_number": "001001",
                    "economic_number": "001",
                    "tanks": "2",
                    "model": "W990",
                    "brand": "KENWORTH",
                    "base_name": null
                },
                "notification_type": "NEW_VEHICLE",
                "priority": "0",
                "message": "Se ha dado de alta un nuevo vehículo"
            },
            {
                "push_id": "558",
                "title": "Daño detectado",
                "image": null,
                "was_read": "1",
                "created_at": "2019-12-09 12:24:38",
                "users": {
                    "installer_name": null,
                    "supervisor_name": null,
                    "driver_name": null
                },
                "installation_point_details": {
                    "installation_group_name": "Tanque piloto",
                    "installation_point_name": "Respiradero"
                },
                "vehicle": null,
                "notification_type": "DAMAGE_DETECTED",
                "priority": "0",
                "message": "Se ha detectado un daño en Respiradero en el vehiculo 001 marca KENWORTH modelo W990 que cuenta con 2 tanque(s) fecha de supervisión 2019-12-09 12:24:38"
            }
        ]
    }
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint  |  Endpoint
-------------|----------------|-----------------------------
GET          | get push       | {{url}}/api/get-push?page={PAGE}

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No aplica

### Type
Key                        | Value 
---------------------------|------------------------------
GENERIC                    | Notificación genérica enviada desde CMS.
DAMAGE_DETECTED            | Notificación detonada cuando un punto es supervisado con algún daño.
SUPERVISION_WITHOUT_DRIVER | Notificación detonada cuando una supervisión es creada sin Chofer asociado.
NEW_VEHICLE                | Notificación detonada cuando un vehículo es creado.
PENDING_SYNCHRONIZATION    | Notificación detonada cuando un usuario no ha realizado movimientos en 7 días.
NOT_SUPERVISED             | Notificación detonada semanalmente para listar los vehículos que no han sido supervisados en los últimos 7 días.

Obtiene las notificaciones asociadas al usuario. El servicio está configurado para que se implemente la función de Paginación.

### Ejemplos de cada tipo
### GENERIC
{
    "push_id": "1830",
    "title": "Título de mi notificación",
    "message": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris dui tortor",
    "notification_type": "GENERIC",
    "image": "https://myimage.com",
    "was_read": "0", 
    "priority": "0",
    "created_at": "2019-11-21 17:56:57",
    "users": null,
    "installation_point_details": null,
    "vehicle": null
}
### DAMAGED_DETECTED
{
    "push_id": "1830",
    "title": "Daño detectado",
    "message": "Se ha detectado un daño en Respiradero en el vehiculo 1 marca KENWORTH modelo W990 que cuenta con 2 tanque(s) fecha de supervisión 2019-11-21 17:56:57",
    "notification_type": "DAMAGE_DETECTED",
    "image": null,
    "was_read": "0",
    "priority": "0",
    "created_at": "2019-11-21 17:56:57",
    "users": {
        "supervisor_name": "Supervisor Test Kokonut",
        "driver_name": null,
        "installer_name": null
    },
    "installation_point_details": {
        "installation_group_name": "Tanque piloto",
        "installation_point_name": "Antisifon"
    },
    "vehicle": {
        "serial_number": "001",
        "economic_number": "001001",
        "tanks": 3,
        "model": "SERIE 300",
        "brand": "HINO",
        "base_name": "CDMX"
    }
}
### SUPERVISION_WITHOUT_DRIVER
{
    "push_id": "1830",
    "title": "Atención de supervisión",
    "message": “Se supervisó un vehículo con un chofer que no está dado de alta“,
    "notification_type": "SUPERVISION_WITHOUT_DRIVER",
    "image": null,
    "was_read": "0",
    "priority": "0",
    "created_at": "2019-11-21 17:56:57",
    "users": {
        "supervisor_name": “Supervisor Test Kokonut“,
        "driver_name": “Driver Test Kokonut”,
        "installer_name": null
    },
    "installation_point_details": null,
    "vehicle": {
        "serial_number": "001",
        "economic_number": "001001",
        "tanks": 3,
        "model": "SERIE 300",
        "brand": "HINO",
        "base_name": "CDMX"
    }
}
### NEW_VEHICLE
{
    "push_id": "1830",
    "title": "Vehículo registrado",
    "message": "Se ha dado de alta un nuevo vehículo",
    "notification_type": "NEW_VEHICLE",
    "image": null,
    "was_read": "0",
    "priority": "0",
    "created_at": "2019-11-21 17:56:57",
    "users": {
        "supervisor_name": null,
        "driver_name": null,
        "installer_name": "Installer Test Kokonut"
    },
    "installation_point_details": null,
    "vehicle": {
        "serial_number": "001",
        "economic_number": "001001",
        "tanks": 3,
        "model": "SERIE 300",
        "brand": "HINO",
        "base_name": "CDMX"
    }
}
### PENDING_SYNCHRONIZATION
{
    "push_id": "1830",
    "title": "Sincronización pendiente",
    "message": "No olvides sincronizar y/o cargar tus datos de supervisión.",
    "notification_type": "PENDING_SYNCHRONIZATION",
    "image": null,
    "was_read": "0",
    "priority": “1”,
    "created_at": "2019-11-21 17:56:57",
    "users": null,
    "installation_point_details": null,
    "vehicle": null
}
### NOT_SUPERVISED
{
    "push_id": "1830",
    "title": "Vehículos por supervisar",
    "message": "Los vehículos enlistados todavía no han sido supervisados.",
    "notification_type": "NOT_SUPERVISED",
    "image": null,
    "was_read": "0", 
    "priority": "0",
    "created_at": "2019-11-21 17:56:57",
    "users": null,
    "installation_point_details": null,
    "vehicle": null
}



## Actualizar estatus de lectura de una notificación
>Actualizar estatus de lectura de una notificación: 

```java
{
    "push_id": 123
}
```
```javascript
{
    "success": 1,
    "message": "Actualización correcta",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

### Descripción
Cambia el estatus de la notificación a "leído".

### Request
HTTP Request | Name Endpoint             |  Endpoint
-------------|---------------------------|------------------------------------------------
POST         | Update notifiacion status | {{url}}/api/staff/update-notification-status

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key     | Value | Mandatory   | Description
--------|-------|-------------|-------------------------------------------------------
push_id | Int   | Obligatorio | ID de la notificación que se desea marcar como leída.



## Obtener vehículos por supervisar
>Obtener vehículos por supervisar: 

```java
{
    "notification_id": 123
}
```
```javascript
{
    "success": 1,
    "message": null,
    "data": [
        {
            "id_vehicle": "eyJ0eX...",
            "serial_number": "100100",
            "economic_number": "100",
            "base_name": "MTY",
            "vehicle_model": "W990",
            "vehicle_brand": "KENWORTH",
            "tanks": 4
        },
        {
            "id_vehicle": "eSJsaeX...",
            "serial_number": "200200",
            "economic_number": "200",
            "base_name": "CDMX",
            "vehicle_model": "W990",
            "vehicle_brand": "KENWORTH",
            "tanks": 1
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

### Descripción
Obtiene el listado de vehículos que no han sido supervisados a través de una notifiación.
Este servicio solo puede ser utilizado con la notificación del tipo NOT_SUPERVISED.

### Request
HTTP Request | Name Endpoint           |  Endpoint
-------------|-------------------------|-------------------------------------
POST         | Not supervised vehicles | {{url}}/api/get-without-supervision

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key             | Value | Mandatory   | Description
----------------|-------|-------------|---------------------------------------------------------------------------
notification_id | Int   | Obligatorio | ID de la notificación de la que se desea obtener los vehículos asociados.





# Security Kit Install and Update
## Mostrar Kits disponibles
>Mostrar Kits disponibles: 

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": null,
    "data": [
        {
            "name": "Antisifon Tanksafe Standard",
            "id": "1"
        },
        {
            "name": "Antisifon Tanksafe Impregnable",
            "id": "2"
        },
        {
            "name": "Candado Respiradero BreatherSafe",
            "id": "3"
        },
        {
            "name": "Kit Protección Mangueras",
            "id": "4"
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|-----------------------------
GET          | show cat security kits | {{url}}/api/install/cat-security-kit-list

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No aplica



## Inicializar Instalación
>Inicializar Instalación: 

```java
{
    "security_kit_list": "[\"1\",\"2\"]",
    "vehicle_id": "eyJpdiI6IlB..."
}
```
```javascript
{
    "success": 1,
    "message": "Instalación completada",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|-----------------------------
POST         | create install         | {{url}}/api/install/create-install

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key               | Descripción                                                                       | Type    | Mandatory
------------------|-----------------------------------------------------------------------------------|---------|----------------
security_kit_list | Valor JSON de un arreglo que contiene los ID´s de los Kits que se desean instalar | String | Obligatorio
vehicle_id        | ID Tokenizado del vehículo para realizar la instalación                           | String | Obligatorio



## Mostrar Instalación
>Mostrar Instalación: 

```java
// No aplica.
```
```javascript
{
    "success": 1,
    "message": null,
    "data": {
        "vehicle_id": "eyJpdiI6IlVD...",
        "installed_kit": [
            {
                "id": "3",
                "name": "Candado Respiradero BreatherSafe"
            },
            {
                "id": "4",
                "name": "Kit Protección Mangueras"
            }
        ],
        "installation_groups": {
            "Tanque piloto": [
                {
                    "id": "4908",
                    "description": "Respiradero",
                    "foliate_stamp": null,
                    "image": "www...",
                    "checked": 1,
                    "failed": 1,
                    "security_kit_id": "3",
                    "other": null,
                    "created_at": "2020-02-18 12:59:00",
                    "fail_description": null,
                    "order": 2,
                    "was_failed": 1,
                    "is_obligatory": 1
                },
                {
                    "id": "4912",
                    "description": "Manguera inyeccion",
                    "foliate_stamp": null,
                    "image": "www...",
                    "checked": 0,
                    "failed": null,
                    "security_kit_id": "4",
                    "other": null,
                    "created_at": "2020-02-18 12:59:00",
                    "fail_description": null,
                    "order": 3,
                    "was_failed": 0,
                    "is_obligatory": 0
                },
                {
                    "id": "4913",
                    "description": "Manguera retorno",
                    "foliate_stamp": null,
                    "image": "www...",
                    "checked": 0,
                    "failed": null,
                    "security_kit_id": "4",
                    "other": null,
                    "created_at": "2020-02-18 12:59:00",
                    "fail_description": null,
                    "order": 4,
                    "was_failed": 0,
                    "is_obligatory": 1
                }
            ]
        }
    }
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|-----------------------------
GET          | show installation      | {{url}}/api/install/show-installation/{{vehicleId}}

### Headers
Key          | Value  
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.



## Remover punto
>Remover punto: 

```java
{
    "installation_point_id": 4457
}
```
```javascript
{
    "success": 1,
    "message": "Se ha eliminado el punto de instalación correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|-----------------------------
POST         | remove point           | {{url}}/api/install/remove-installation-point

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Descripción                                              | Type | Mandatory
----------------------|----------------------------------------------------------|------|--------------
installation_point_id | ID asociado al punto de instalación que se desea remover | Int  | Obligatorio



## Instalar Otro punto
>Instalar Otro punto: 

```java
{
    "vehicle_id": "eyJpdiI6Im5r...",
    "foliate_stamp": "[\"0001\",\"0003\",\"0004\"]",
    "name": "Llanta",
    "image": $FILE
}
```
```javascript
{
    "success": 1,
    "message": "Instalación completada",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|----------------------------------------------
POST         | create install others  | {{url}}/api/install/create-install-others

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key           | Descripción                                             | Type   | Mandatory
--------------|---------------------------------------------------------|--------|-------------
vehicle_id    | ID Tokenizado del vehículo para realizar la instalación | String | Obligatorio
foliate_stamp | Número de folio de la pieza                             | String | Opcional
name          | Nombre de la pieza                                      | String | Obligatorio
image         | Imagen de la pieza                                      | File   | Obligatorio





# Supervision
## Crear supervisión
>Crear supervisión: 

```java
// Con un chofer dado de alta anteriormente
{
    "driver_id": "eyJpdiI...",
    "it_goes_in": 1,
    "supervisor_id": "eyJpdiI6...",
    "vehicle_id": "eyJpdiI6I..."
}
// Con un chofer no registrado anteriormente
{
    "driver_name": "Nombre Del Chofer",
    "it_goes_in": 0,
    "supervisor_id": "eyJpdiI6...",
    "vehicle_id": "eyJpdiI6Il..."
}
```
```javascript
{
    "success": 1,
    "message": "Supervisión completada correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|---------------------------------------
POST         | create supervision     | {{url}}/api/install/create-supervision

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key           | Descripción                                                                            | Type   | Mandatory
--------------|----------------------------------------------------------------------------------------|--------|-------------
driver_id     | ID Tokenizado del chofer asignado a la supervisión                                     | String | Obligatorio
it_goes_in    | Indica si un vehículo va de entrada o de salida. 1 si va de entrada, 0 si va da salida | Int    | Obligatorio
supervisor_id | ID Tokenizado del supervisor que inicializó la supervisión                             | String | Obligatorio
vehicle_id    | ID Tokenizado del vehículo a supervisar                                                | String | Obligatorio



## Actualizar punto de supervisión
>Actualizar punto de supervisión: 

```java
{
    "its_ok": 1,
    "supervisor_id": "eyJpdiI6...",
    "supervision_id": 210,
    "vehicle_installation_point": 2572
}
{
    "its_ok": 0,
    "fail_description": "La manguera del Kit X está rota", // NULL
    "supervisor_id": "eyJpdiI6...",
    "supervision_id": 210,
    "vehicle_installation_point": 2572,
    "image_": $FILE
}
```
```javascript
{
    "success": 1,
    "message": "Supervisión completada correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|---------------------------------------
POST         | update supervision     | {{url}}/api/install/update-supervision

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                        | Descripción                                                                                   | Type   | Mandatory
---------------------------|-----------------------------------------------------------------------------------------------|--------|-------------
its_ok                     | Indica el status actual del punto. 1 si va el punto está sin falló, 0 si se encontró un fallo | Int    | Obligatorio
vehicle_installation_point | ID del punto a supervisar.                                                                    | Int    | Obligatorio
supervisor_id              | ID Tokenizado del supervisor que inicializó la supervisión                                    | String | Obligatorio
supervision_id             | ID de la supervisón                                                                           | Int    | Obligatorio
image_                     | Imagen a actualizar                                                                           | File   | Opcional



## Obtener supervisión
>Obtener supervisión: 

```java
// No requerido
```
```javascript
{
    "success": 1,
    "message": null,
    "data": {
        "id": 210,
        "vehicle_id": "eyJpdiI6...",
        "driver_id": "eyJpdiI...",
        "supervisor_id": "eyJpdi...",
        "it_goes_in": "0",
        "created_at": "2019-09-25 16:24:25"
    }
}
```
```csharp
{
    "success": 0,
    "message": "Unauthenticated",
    "data": []
}
```

HTTP Request | Name Endpoint          |  Endpoint
-------------|------------------------|---------------------------------------
GET          | get supervision        | {{url}}/api/install/get-supervision/{{vehicleId}

### Headers
Key          | Value 
-------------|------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido