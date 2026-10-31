## Sebastian Ramirez Ramos.
## Wainer Jesus Angulo Panameño.
## Sandra Nahomy Castro Olaya
## Erika Alexandra Estupiñan Valenzuela

## 1. Introducción

Durante el desarrollo del taller **Operación Marea Alta**, el equipo
trabajó en una propuesta de base de datos para organizar la información
relacionada con los hogares afectados por la emergencia, sus
necesidades, las donaciones recibidas y la entrega de ayudas
humanitarias.

Para construir el modelo se realizaron discusiones grupales y se tomaron
decisiones sobre la forma de organizar la información. Estas decisiones
se reflejan tanto en el diagrama entidad-relación como en las reglas que
el equipo propuso para ordenar la atención de los hogares.

En este documento se explican  las principales decisiones del equipo,
teniendo en cuenta el enunciado y el diagrama elaborado.

## Decisiones tomadas en el diseño del diagrama

## 1. Diseño del diagrama

### Separar las condiciones de prioridad y las necesidades del hogar
Esta desición, se toma teniendo en cuenta que un hogar puede tener varias
condiciones de prioridad y varias necesidades, de esta manera se garantiza
que el diseño permita a cada hogar la seleccion de muchas necesidades y condiciones
de prioridad.


### Crear una tabla para la persona de contacto
En el diagrama se creó la tabla persona_contacto, separada de la tabla
hogar. Allí se guardan los datos personales y de contacto de quien
representa al hogar, como nombres, apellidos, tipo y número de documento
y teléfono.

Se tomó esta decisión porque la persona de contacto y el hogar
representan información diferente. El hogar reúne los datos sobre la
familia y su situación, mientras que la persona de contacto permite
identificar con quien puede comunicarse con el equipo encargado de la
operación.

Separar estas tablas facilita organizar la información y
modificar los datos de contacto sin tener que alterar los demás datos
del hogar. 

### Separar la ubicación del hogar
También se creó la tabla ubicacion, relacionada con hogar mediante
id_ubicacion. Esta tabla contempla campos como barrio, corregimiento,
vereda, comunidad y referencia de ubicación.

La decisión se tomó porque Buenaventura tiene sectores urbanos y
rurales, y no todos los hogares pueden identificarse mediante una
dirección convencional. Por ejemplo, en una zona rural puede ser más
útil registrar la vereda o una referencia que permita encontrar el
lugar.

Al separar la ubicación, se evita mezclar estos datos con la información
general del hogar y se facilita consultar los hogares según el sector
donde se encuentran.

### Registrar la selección de las ayudas
Esta tabla se conecta con el inventario y el reporte, para garantizar que la ayudas sean
escogidas de acuerdo con la necesidad de hogar. El inventario cuenta con el atributo
"disponible", que en caso de que su valor sea true, significaría que si se puede llevar seleccionar
y se puede llevar a cabo al entrega.


### 2. Prioridad según las condiciones del hogar
Se decidió dar mayor prioridad a los hogares que presenten alguna de
estas condiciones:

-   Mujeres gestantes.
-   Niños.
-   Personas con discapacidad o movilidad reducida.
-   Personas mayores.

El orden propuesto por el equipo es:

1.  Mujeres gestantes.
2.  Niños.
3.  Personas con discapacidad.
4.  Personas mayores.

La idea es reconocer que algunas condiciones pueden hacer que un hogar
necesite atención especial. Sin embargo, este orden debe entenderse como
un criterio inicial del equipo y no como una regla que aplique de la
misma manera a todas las situaciones.



### Prioridad según el tipo de necesidad
También se propuso ordenar las necesidades de acuerdo con su categoría:

1.  Refugio temporal.
2.  Agua potable.
3.  Alimentación.
4.  Medicamentos.
5.  Elementos de aseo.

Este orden busca dar una orientación general sobre cuáles necesidades
deberían atenderse primero. Aunque la categoría no debe confundirse
con la urgencia de un caso particular, porque na solicitud de medicamentos
podría ser urgente dependiendo de la situación del hogar.

Por eso, se considera importante conservar el tipo de necesidad y su
nivel de urgencia como datos diferentes.

### Sistema de puntuación
Para combinar los criterios anteriores, el equipo propuso asignar puntos
a las condiciones del hogar y a los tipos de necesidad. Las categorías
consideradas más prioritarias recibirían una puntuación mayor y las de
menor prioridad una puntuación inferior, este sistema permitiría ordenar los casos de una manera más clara.
