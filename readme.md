## Índice

0. [Ficha del proyecto](#0-ficha-del-proyecto)
1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 0. Ficha del proyecto

### **0.1. Tu nombre completo:**
Cristina Cachero Castro
### **0.2. Nombre del proyecto:**
API REST para gestión de asociaciones de vecinos
### **0.3. Descripción breve del proyecto:**

### **0.4. URL del proyecto:**


> Puede ser pública o privada, en cuyo caso deberás compartir los accesos de manera segura. Puedes enviarlos a [alvaro@lidr.co](mailto:alvaro@lidr.co) usando algún servicio como [onetimesecret](https://onetimesecret.com/).

### 0.5. URL o archivo comprimido del repositorio
https://github.com/ccacheroc/AI4Devs-finalproject
> Puedes tenerlo alojado en público o en privado, en cuyo caso deberás compartir los accesos de manera segura. Puedes enviarlos a [alvaro@lidr.co](mailto:alvaro@lidr.co) usando algún servicio como [onetimesecret](https://onetimesecret.com/). También puedes compartir por correo un archivo zip con el contenido


---

## 1. Descripción general del producto

> Describe en detalle los siguientes aspectos del producto:

### **1.1. Objetivo:**

La aplicación tiene como propósito central facilitar la gestión integral de una asociación de vecinos, proporcionando un sistema unificado donde residentes, socios y administradores puedan comunicarse, organizar actividades comunitarias, resolver incidencias y acceder a información relevante de forma rápida y segura. 

El producto aporta valor a tres niveles:

1. **Administración eficiente para la Junta Directiva**  
   Centraliza tareas clave como la gestión de incidencias, el envío de notificaciones, la comunicación con socios, la organización de eventos, el control financiero y la distribución de documentación interna.

2. **Participación y transparencia para los socios**  
   Permite a los miembros registrar incidencias, consultar documentos, votar en encuestas, acceder al estado financiero de la asociación y participar activamente en eventos y decisiones comunitarias.

3. **Acceso público responsable para simpatizantes y visitantes**  
   Ofrece información básica del barrio, noticias, eventos públicos y opciones para registrarse y convertirse en socios, fomentando una comunidad más conectada.

En conjunto, la app resuelve problemas habituales en asociaciones vecinales: falta de comunicación, trámites dispersos, dificultad para gestionar incidencias, baja participación y escasa transparencia en decisiones y finanzas. Este producto unifica todas esas necesidades en una plataforma accesible, clara y adaptada a roles.


### **1.2. Características y funcionalidades principales:**

1. **Gestión de usuarios y roles**
   - Roles definidos: administrador, socio, simpatizante y visitante.  
   - Permisos diferenciados según cada rol.  
   - Posibilidad de crear grupos personalizados de usuarios para comunicaciones específicas.

2. **Notificaciones push**
   - Envío de avisos con prioridad y destinatarios específicos.  
   - Pop-ups en móvil y registro histórico de notificaciones.  
   - Campos clave: título, descripción, prioridad, fechas, estado, destinatarios.

3. **Gestión de incidencias**
   - Creación, edición y eliminación de incidencias por parte de socios.  
   - Tipificación de incidencias con guía de tramitación automática.  
   - Campo `tramita_socio` para decidir quién gestiona la incidencia.  
   - Administradores gestionan todas las incidencias y comentarios.  
   - Soporte para fotos, ubicación y comentarios encadenados.

4. **Acceso y gestión de documentación**
   - Subida, edición y eliminación de documentos por administradores.  
   - Visualización por parte de socios.  
   - Campos: tipo, fecha, autor, descripción y archivo adjunto.

5. **Finanzas y presupuestos**
   - Gestión de ingresos, gastos, balances y previsiones anuales.  
   - Consulta de estado financiero global por parte de socios.  
   - Registro detallado de ingresos reales y gastos reales.

6. **Pagos y cuotas**
   - Pasarela integrada para pagos de socios y no socios.  
   - Recordatorios programables enviados como notificaciones.  
   - Información para que simpatizantes puedan convertirse en socios.

7. **Eventos comunitarios**
   - Creación y gestión de eventos públicos y privados.  
   - Registro de intención de asistencia y confirmación el día del evento.  
   - Campos: fecha, lugar, tipo, participantes, organizador.  
   - Gestión separada de eventos y registros de asistencia.

8. **Encuestas y votaciones**
   - Creación y administración por parte de administradores.  
   - Participación abierta solo a socios.  
   - Herramienta clave para la toma de decisiones comunitarias.

9. **Noticias del barrio**
   - Publicación de noticias con foto, categoría, fecha y enlace.  
   - Acceso universal para todos los perfiles.  

10. **Directorio de contactos**
   - Información de la junta directiva, servicios públicos y emergencias.  
   - Accesible a todos los perfiles.  
   - Teléfonos y correos interactivos (tap-to-call / tap-to-email).

Estas funcionalidades se articulan para cubrir las necesidades centrales de una comunidad vecinal moderna: comunicación, participación, transparencia, gestión operativa y eficiencia administrativa.


### **1.3. Diseño y experiencia de usuario:**

> Proporciona imágenes y/o videotutorial mostrando la experiencia del usuario desde que aterriza en la aplicación, pasando por todas las funcionalidades principales.

### **1.4. Instrucciones de instalación:**
> Documenta de manera precisa las instrucciones para instalar y poner en marcha el proyecto en local (librerías, backend, frontend, servidor, base de datos, migraciones y semillas de datos, etc.)

---

## 2. Arquitectura del Sistema

### **2.1. Diagrama de arquitectura:**
> Usa el formato que consideres más adecuado para representar los componentes principales de la aplicación y las tecnologías utilizadas. Explica si sigue algún patrón predefinido, justifica por qué se ha elegido esta arquitectura, y destaca los beneficios principales que aportan al proyecto y justifican su uso, así como sacrificios o déficits que implica.


### **2.2. Descripción de componentes principales:**

> Describe los componentes más importantes, incluyendo la tecnología utilizada

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros**

> Representa la estructura del proyecto y explica brevemente el propósito de las carpetas principales, así como si obedece a algún patrón o arquitectura específica.

### **2.4. Infraestructura y despliegue**

> Detalla la infraestructura del proyecto, incluyendo un diagrama en el formato que creas conveniente, y explica el proceso de despliegue que se sigue

### **2.5. Seguridad**

> Enumera y describe las prácticas de seguridad principales que se han implementado en el proyecto, añadiendo ejemplos si procede

### **2.6. Tests**

> Describe brevemente algunos de los tests realizados

---

## 3. Modelo de Datos

### **3.1. Diagrama del modelo de datos:**

> Recomendamos usar mermaid para el modelo de datos, y utilizar todos los parámetros que permite la sintaxis para dar el máximo detalle, por ejemplo las claves primarias y foráneas.


### **3.2. Descripción de entidades principales:**

> Recuerda incluir el máximo detalle de cada entidad, como el nombre y tipo de cada atributo, descripción breve si procede, claves primarias y foráneas, relaciones y tipo de relación, restricciones (unique, not null…), etc.

---

## 4. Especificación de la API

> Si tu backend se comunica a través de API, describe los endpoints principales (máximo 3) en formato OpenAPI. Opcionalmente puedes añadir un ejemplo de petición y de respuesta para mayor claridad

---

## 5. Historias de Usuario

> Documenta 3 de las historias de usuario principales utilizadas durante el desarrollo, teniendo en cuenta las buenas prácticas de producto al respecto.

**Historia de Usuario 1**

**Historia de Usuario 2**

**Historia de Usuario 3**

---

## 6. Tickets de Trabajo

> Documenta 3 de los tickets de trabajo principales del desarrollo, uno de backend, uno de frontend, y uno de bases de datos. Da todo el detalle requerido para desarrollar la tarea de inicio a fin teniendo en cuenta las buenas prácticas al respecto. 

**Ticket 1**

**Ticket 2**

**Ticket 3**

---

## 7. Pull Requests

> Documenta 3 de las Pull Requests realizadas durante la ejecución del proyecto

**Pull Request 1**

**Pull Request 2**

**Pull Request 3**

