## Modelo relacional

## Sebastian Ramirez Ramos.
## Wainer Jesus Angulo Panameño.
## Sandra Nahomy Castro Olaya
## Erika Alexandra Estupiñan Valenzuela

persona_contacto (
    id                  INTEGER          PK,
    primer_nombre       VARCHAR(60)      NOT NULL,
    segundo_nombre      VARCHAR(60),
    primer_apellido     VARCHAR(60)      NOT NULL,
    segundo_apellido    VARCHAR(60),
    genero              VARCHAR(30)      NOT NULL,
    tipo_documento      VARCHAR(30)      NOT NULL,
    numero_documento    VARCHAR(30)      NOT NULL UNIQUE,
    edad                SMALLINT         NOT NULL,
    numero_telefono     VARCHAR(20)      NOT NULL
)

ubicacion (
    id                  INTEGER          PK,
    barrio              ENUM(),
    corregimiento       ENUM(),
    vereda              ENUM(),
    comunidad           ENUM(),
    referencia_ubicacion VARCHAR(255)
)

hogar (
    id                  INTEGER          PK,
    persona_contacto    INTEGER          FK -> hogar.id,
    id_ubicacion        INTEGER          FK -> ubicacion.id,
    numero_integrantes  SMALLINT         NOT NULL
)

necesidad (
    id                  INTEGER          PK,
    categoria           VARCHAR(100)     NOT NULL
)

condicion_prioridad (
    id                  INTEGER          PK,
    embarazadas         BOOLEAN          NOT NULL,
    niños               BOOLEAN          NOT NULL,
    discapacitados      BOOLEAN          NOT NULL,
    adultos_mayores     BOOLEAN          NOT NULL
)

reporte (
    id                      INTEGER          PK,
    id_hogar                INTEGER          FK -> hogar.id,
    id_necesidad            INTEGER          FK -> necesidad.id,
    id_condicion_prioridad  INTEGER          FK -> condicion_prioridad.id,
    cantidad                INTEGER          NOT NULL,
    observacion             TEXT,
    fecha                   DATETIME         NOT NULL,
    nivel_urgencia          ENUM()           NOT NULL,
    estado                  ENUM()           NOT NULL
)

ayudas_disponibles (
    id                  INTEGER          PK,
    id_inventario       INTEGER          FK -> inventario.id,
    cantidad            INTEGER          NOT NULL
)

seleccion_ayuda (
    id                      INTEGER          PK,
    id_punto_atencion       INTEGER          FK -> punto_atencion.id,
    id_inventario           INTEGER          FK -> inventario.id,
    cantidad                INTEGER          NOT NULL
)

tipo_ayuda (
    id                  INTEGER          PK,
    categoria           VARCHAR(100)     NOT NULL,
    nombre_articulo     VARCHAR(120)     NOT NULL
)

donante (
    id                  INTEGER          PK,
    tipo_donante        VARCHAR(40)      NOT NULL,
    nombre              VARCHAR(120)     NOT NULL
)

donacion (
    id                  INTEGER          PK,
    id_donante          INTEGER          FK -> donante.id,
    fecha               DATE             NOT NULL
)

detalle_donacion (
    id                  INTEGER          PK,
    id_donacion         INTEGER          FK -> donacion.id,
    id_tipo_ayuda       INTEGER          FK -> tipo_ayuda.id,
    id_inventario       INTEGER          FK -> inventrio.id,
    cantidad            INTEGER          NOT NULL,
    unidad_medida       VARCHAR(30)      NOT NULL
)

inventario (
    id                      INTEGER          PK,
    cantidad                INTEGER          NOT NULL,
    disponible              BOOLEAN          NOT NULL
)

punto_atencion (
    id                      INTEGER          PK,
    id_seleccion_ayuda      INTEGER          FK -> seleccion_ayuda.id,
    ubicacion               VARCHAR(255)     NOT NULL,
    id_inventario           INTEGER          FK -> inventario.id,
    fecha                   DATE             NOT NULL
)

entrega (
    id                  INTEGER          PK,
    id_punto_atencion   INTEGER          FK -> punto_atencion.id,
    id_jornada_entrega  INTEGER          FK -> jornada_entrega.id
)

jornada_entrega (
    id                  INTEGER          PK,
    nombre              VARCHAR(100)     NOT NULL,
    fecha               DATETIME         NOT NULL,
    lugar               VARCHAR(200)     NOT NULL,
    descripcion         TEXT,
    estado              ENUM()           
)
