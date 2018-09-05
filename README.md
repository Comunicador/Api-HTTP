# Api-HTTP
Manual de conexión API HTTP




# Contenido

1. API HTTP
2. APPI HTTP
3. Autenticación
4. Envío individual
5. Envió a Grupos
6. Recepción De Mensajes Entrantes 
7. Códigos de Error




# APPI HTTP
El API HTTP permite a los usuarios hacer un manejo ágil de la plataforma de
envío de mensaje, dicho de otra forma es una versión simplificada del API REST, ya que
esta interfaz permite hacer envíos sin mayor complejidad que elaborar una llamada vía
HTTP.

API HTTP: HTTPS://APPS.INTERACTUAMOVIL.COM/HTTP

Ventajas: La principal ventaja de esta Api, es que permite la integración de sistemas
cerrados que actualmente ya soportan una interfaz SMS, y esto se realiza mediante el
uso de un URL predefinido. Al igual que en la API REST debe existir un proceso de
autenticación el cual se puede realizar por medio la autorización de direcciones IP fijas
o utilizando el API KEY. Además es importante mencionar que se permite el envío de
mensajes a contactos y grupos.

Nota: Debe tener en cuenta que con esta interfaz no se puede realizar la administración
de grupos y contactos y que el proceso de autenticación es mucho menos estricto. Si se
tiene la necesidad de administrar la creación de contactos, grupos y demás
funcionalidades, le sugerimos ponerse en contacto con su ejecutivo de cuenta para que
le haga llegar la documentación del API Rest o SDK.




# Autenticación
El primer paso consiste en la autenticación. Esta se puede realizar validando la
dirección IP de origen de la llamada. Para ello se necesita que la empresa genere y
envíe lo antes posible el listado de direcciones IP de los cuales deseen elaborar las
peticiones.

Otra forma de realizar la autenticación (en caso no sea posible o no se desee generar un
listado de direcciones IP) consiste en enviar en cada llamada el parámetro API_KEY, el
cual debe contener el API KEY proporcionado para su cuenta empresarial.

# Ejemplo enviando el API KEY
HTTPS://APPS.INTERACTUAMOVIL.COM/HMP/SEND_TO_CONTACT?MSISDN=SMSNUMBER&MESSAGE=SMSTEXT&API_KEY=API_KEY

# Ejemplo con IP autenticado
HTTPS://APPS.INTERACTUAMOVIL.COM/HMP/SEND_TO_CONTACT?MSISDN=SMSNUMBER&MESSAGE=SMSTEXT


# Envío individual
Una de las funcionalidades principales consiste en el envío de mensajes de forma
individual. Para hacer un envío de esta forma se debe hacer una llamada al siguiente
URL:

HTTPS://APPS.INTERACTUAMOVIL.COM/HMP/SEND_TO_CONTACT?MSISDN=SMSNUMBER&MESSAGE=SMSTEXT&API_KEY=API_KEY&ID=ID


Donde:

1. SMSNUMBER se refiere al número de teléfono destino del mensaje y debe incluir
el código internacional de país, en este caso 502 para Guatemala.

2. SMSTEXT contiene el texto del mensaje que se desea enviar.

3. API_KEY es la llave de autenticación suministrada (la cual puede obviarse si se
utiliza el método de autenticación por medio de validación de dirección IP)

4. ID el cual es un valor de identificación único de mensaje. Este valor sirve para
evitar envíos duplicados de mensajes al realizar reintentos. Cualquier mensaje
que lleve el mismo ID dentro de una ventana de 2 horas será rechazado por
duplicidad. Si no se envía este campo, la validación de duplicación se realizará
sobre el destinatario + mensaje

# Envio a Grupos
Otra de las funcionalidades principales del API, consiste en el envío de mensajes a
grupos. Para poder enviar mensajes a grupos (los cuales deben haber sido creados
previamente desde el API REST o desde la interfaz web) se debe invocar al siguiente
URL:

HTTPS://APPS.INTERACTUAMOVIL.COM/HMP/SEND_TO_GROUP?GROUPS=GROUP_NAME&MESSAGE=SMSTEXT&API_KEY=API_KEY&ID=ID

Donde:
1. GROUP_NAME contiene un listado de los grupos a los que se desea hacer el envío
del mensaje. Los grupos debe ir separados por coma. Por ejemplo: ventas,
mercadeo, gerencia.

2. SMSTEXT contiene el mensaje que se desea enviar.

3. API_KEY es la llave de autenticación suministrada (la cual puede obviarse si se
utiliza el método de autenticación por medio de validación de dirección IP)

4. ID el cual es un valor de identificación único de mensaje. Este valor sirve para
evitar envíos duplicados de mensajes al realizar reintentos. Cualquier mensaje
que lleve el mismo ID dentro de una ventana de 2 horas será rechazado por
duplicidad. Si no se envía este


# Recepción De Mensajes Entrantes

El Api provee la funcionalidad de poder recibir mensajes. Para poder recibir los
mensajes entrantes, se debe suministrar un URL al cual se desea que se envíen todos los
mensajes por medio del método PUSH.

El mensaje llegara en JSON (JavaScript Object Notation) y contendrá los valores de
msisdn remitente, fecha y el mensaje.


# Códigos de ERROR

Código HTTP:503 | Código:503   | Descripción: Error interno | Reintentar: Si

Código HTTP:401 | Código:401   | Descripción: No autorizado | Reintentar: No

Código HTTP:400 | Código:40001 | Descripción: Parámetro invalido o vacío | Reintentar: No

Código HTTP:400 | Código:40002 | Descripción: El msisdn no puede ser igual a la marcación | Reintentar: No

Código HTTP:400 | Código:40003 | Descripción: No hay coincidencias para los grupos enviados | Reintentar: No

Código HTTP:400 | Código:40301 | Descripción: Ha excedido el número de mensajes contratados | Reintentar: No

Código HTTP:403 | Código:40302 | Descripción: El msisdn está bloqueado en lista negra | Reintentar: No

Código HTTP:403 | Código:40303 | Descripción: No se encontró contacto asociado al msisdn | Reintentar: No

Código HTTP:403 | Código:40304 | Descripción: El mensaje ha sido bloqueado por políticas antiSPAM | Reintentar: No

Código HTTP:403 | Código:40305 | Descripción: El contacto ha cancelado el servicio | Reintentar: No

Código HTTP:403 | Código:40306 | Descripción: El envío excederá el número de mensajes contratados | Reintentar: No

Código HTTP:403 | Código:40307 | Descripción: El envío está fuera del horario permitido | Reintentar: No

Código HTTP:403 | Código:40308 | El mensaje ha sido bloqueado debido a que esta duplicado | Reintentar: No

Código HTTP:403 | Código:40309 | El mensaje ha sido bloqueado debido a que el ID de mensaje esta duplicado | Reintentar: No



