# Control de Gastos (Backend)

Control de Gastos es un backend construido con **Spring Boot** y **MongoDB**, diseñado para gestionar un presupuesto y múltiples gastos realizados por el usuario. Este proyecto proporciona una API RESTful que permite crear, leer, actualizar y eliminar gastos, así como realizar estas mismas acciones para un único presupuesto.

## Tecnologías Utilizadas

- **Spring Boot**: Framework para construir aplicaciones Java. Particularmente en este proyecto se utiliza la versión `3.4.0`.
  - **Jakarta Validation**: Validación de datos de entrada.
  - **Eventos de ciclo de vida**: Se crea una clase que extiende de la clase `AbstractMongoEventListener`, la cual permite manejar acciones antes o después de realizar alguna de las operaciones CRUD sobre los objetos de la clase `Expense`.
- **Java**: Lenguaje de programación principal. Para este proyecto en específico se utilizó el `JDK 17`.
- **Maven**: Para la gestión de dependencias y construcción del proyecto.
- **MongoDB**: Base de datos NoSQL para almacenar las actividades.
- **Postman**: Para simular ser un cliente que hace peticiones al servidor y probar los endpoints.
- **JUnit**: Framework de pruebas unitarias utilizado para verificar el correcto funcionamiento de los métodos.
- **Mockito**: Framework de mocking usado para simular dependencias y facilitar las pruebas unitarias en aislamiento.
- **Swagger / OpenAPI**: Herramienta para documentar y probar los endpoints de la API de forma interactiva.
- **Docker**: permite ejecutar esta aplicación en un entorno aislado, sin necesidad de configurar manualmente dependencias o versiones. 

## Características

### EndPoint's

Rutas organizadas para interactuar con los gastos y el presupuesto del usuario. Operaciones soportadas:
- **Budget**:
  - Obtener el presupuesto.
  - Guardar el presupuesto.
  - Eliminar el presupuesto.
- **Expenses**
  - Listar todos los gastos.
  - Obtener un gasto específico por su ID.
  - Crear nuevos gastos. Para ello se debe ingresar el nombre, monto, categoría y fecha del gasto.
  - Actualizar gastos existentes.
  - Eliminar gastos individuales.
  - Eliminar todos los gastos.
 
### Gestor de base de datos

- Integración con MongoDB para la manipulación de datos.
- La base de datos NoSQL cuenta con dos colecciones: una gestiona la información del presupuesto y la otra gestiona la información de los gastos.

### Validaciones

Se emplean las siguientes validaciones:
- No se permite que los atributos **nombre** y **categoría** de los gastos se reciban vacíos o con puros espacios en blanco.
- No se permite que el atributo **monto** del gasto se reciba con un valor menor o igual a cero.
- No se permite que el atributo **monto** del presupuesto se reciba con un valor menor a 500 (valor arbitrariamente seleccionado).
- No se permite que el atributo **fecha de creación** del presupuesto se reciba con una fecha posterior al día de hoy.

### Patrones de diseño

- Se emplea el patrón de diseño arquitectónico conocido como **MVC**, para separar en diferentes capas el código del proyecto.
- El proyecto emplea **DTOs** para separar los datos expuestos en las solicitudes y respuestas del modelo de dominio, mejorando la organización y el control de la información intercambiada.

### Eventos del ciclo de vida para los objetos de las clases entity

- Cada vez que se actualiza la información de algún gasto, se actualizará automáticamente el campo `updateAt` de ese mismo registro.

### Docker

Este proyecto utiliza Docker para crear un entorno de ejecución aislado y reproducible, asegurando que la aplicación funcione igual en cualquier sistema. 

Archivos relevantes:

- `Dockerfile`: define la imagen base y cómo se construye el entorno del proyecto.
- `docker-compose.yml`: orquesta los servicios (API y base de datos) para facilitar la ejecución local.
- `.env`: contiene variables de entorno usadas por Docker (no se incluye en el repositorio por seguridad).

## Estructura del Proyecto

### Código fuente de la aplicación

- `controllers/`: Carpeta donde se almacenan las clases que manejan las solicitudes HTTP y definen los endpoints de la API.
- `services/`: Carpeta donde se almacenan las clases que contienen el código relacionado con la lógica de negocio.
- `repositories/`: Carpeta donde se almacenan las interfaces que extienden de una interfaz que permite el manejo de datos.
- `entities/`: Carpeta donde se almacenan las clases que se mapean con sus respectivas colecciones en la base de datos.
- `events/`: Carpeta donde se almacenan las clases que manejan acciones antes o después de realizar alguna de las operaciones CRUD.

### Código de pruebas

- `controllers/`: Contiene las clases de prueba que validan el comportamiento de los métodos en los controladores del código fuente.
- `services/`: Incluye las clases de prueba dedicadas a verificar el correcto funcionamiento de los métodos dentro de los servicios de la aplicación.
- `data/`: Almacena clases con datos simulados (mock data) utilizados durante la ejecución de las pruebas.
- `integrations/`: Contiene las clases de prueba que validan el comportamiento completo de los controladores (tests de integración).
- `resources/`: Almacena los datos en formato JSON utilizados como insumos para las pruebas de integración.

## Demo

Puedes ver una demo del proyecto en el siguiente enlace: [Control de Gastos](https://serene-frangollo-9ddb20.netlify.app/).

**Nota:** La demo del proyecto es únicamente demostrativa. Esta no está enlazada con el backend.

## Futuras mejoras

- Despliegue de la aplicacion en AWS
- Despligue automatico usando jenkins

---

# Expense Tracker (Backend)

Expense Tracker is a backend built with **Spring Boot** and **MongoDB**, designed to manage a budget and multiple expenses made by the user. This project provides a RESTful API that allows creating, reading, updating, and deleting expenses, as well as performing the same actions for a single budget.

## Technologies Used

- **Spring Boot**: Framework for building Java applications. This project uses version `3.4.0`.
  - **Jakarta Validation**: For validating input data.
  - **Lifecycle Events**: A class extending `AbstractMongoEventListener` is created, allowing actions to be executed before or after CRUD operations on `Expense` objects.
- **Java**: Main programming language. This project uses `JDK 17`.
- **Maven**: For dependency management and building the project.
- **MongoDB**: NoSQL database used to store activities.
- **Postman**: Used to simulate a client making requests to the server and to test API endpoints.
- **JUnit**: Unit testing framework used to verify the correct functionality of methods.
- **Mockito**: Mocking framework used to simulate dependencies and facilitate isolated unit testing.
- **Swagger / OpenAPI**: Tool to document and interactively test API endpoints.
- **Docker**: Allows the application to run in an isolated environment without manually configuring dependencies or versions.

## Features

### Endpoints

Organized routes to interact with the user's expenses and budget. Supported operations:
- **Budget**:
  - Get the budget.
  - Save the budget.
  - Delete the budget.
- **Expenses**
  - List all expenses.
  - Get a specific expense by its ID.
  - Create new expenses by providing the name, amount, category, and date.
  - Update existing expenses.
  - Delete individual expenses.
  - Delete all expenses.

### Database Manager

- Integration with MongoDB for data manipulation.
- The NoSQL database contains two collections: one manages budget information, the other manages expense information.

### Validations

The following validations are used:
- The **name** and **category** fields of expenses cannot be empty or contain only whitespace.
- The **amount** field of an expense cannot be less than or equal to zero.
- The **budget amount** cannot be less than 500 (arbitrary value).
- The **creation date** of the budget cannot be a future date.

### Design Patterns

- The **MVC** architectural design pattern is used to separate the project’s code into different layers.
- The project uses **DTOs** to separate the data exposed in requests and responses from the domain model, improving organization and control of the exchanged information.

### Lifecycle Events for Entity Classes

- Every time an expense is updated, the `updatedAt` field of that document is automatically updated.

### Docker

This project uses Docker to create an isolated and reproducible runtime environment, ensuring that the application behaves the same on any system.

Relevant files:

- `Dockerfile`: Defines the base image and how to build the project environment.
- `docker-compose.yml`: Orchestrates the services (API and database) to simplify local execution.
- `.env`: Contains environment variables used by Docker (not included in the repository for security reasons).

## Project Structure

### Application Source Code

- `controllers/`: Contains classes that handle HTTP requests and define API endpoints.
- `services/`: Contains classes that implement business logic.
- `repositories/`: Contains interfaces extending data management functionality.
- `entities/`: Contains classes mapped to their respective database collections.
- `events/`: Contains classes handling actions before or after CRUD operations.

### Test Code

- `controllers/`: Contains test classes that validate the behavior of controller methods.
- `services/`: Contains test classes that verify correct functionality within service methods.
- `data/`: Stores mock data classes used during tests.
- `integrations/`: Contains integration tests validating full controller behavior.
- `resources/`: Stores JSON data used as input for integration tests.

## Demo

You can view a demo of the project at the following link: [Expense Tracker](https://serene-frangollo-9ddb20.netlify.app/).

**Note:** This demo is only for demonstration purposes. It is not connected to the backend.

## Future Improvements

- Deploy the application on AWS  
- Automated deployment using Jenkins