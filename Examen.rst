ENUNCIADO
---------

El Hotel Noa, precisa disponer de informacion para sus reservas de habitaciones, por lo que
decidieron generar un documento XML con la informacion de las mismas, asi como documentos de
validacion. Aunque el tecnico informatico ha pensado en generarlo dinamicamente a partir de la
informacion almacenada en una base de datos, necesitan preparar un documento XML y un DTD
asociado que sirva como plantilla.

Caracteristicas:
- Un elemento raiz llamado reservas.

- Todos los atributos del XML seran obligatorios.

- Las reservas tienen un numero variable de reservas y clientes. Puede no haber.

- Cada reserva tiene:
  o Atributos, todos obligatorios: codigo de cliente (cliente), formado por la letra C
    seguida del DNI (8 numeros y una letra mayuscula), por ejemplo C53454123X;
    tipoHabitacion, que podra tener los valores: SA, AD, MP o PC, que indican ``solo
    alojamiento``, ``alojamiento y desayuno``, ``media pension`` y ``pension completa``; tipo de
    habitacion (habitacion), que puede tener los valores, Doble o Individual.
  o Fecha de Inicio (fechaInicio), con atributos dia, mes y ano, obligatorios. Los tres
    deben ser atributos. El atributo mes solo puede tomar los valores de los nombres de los
    meses del ano.
  o Fecha de fin (fechaFin), con atributos dia, mes y ano, obligatorios. Igual a la anterior.
  o Observaciones (observaciones), una parrafada, opcional para cada reserva y solo puede
    haber una.

- Cada cliente tiene un atributo codigo de cliente (id) que debe estar relacionado con la reserva
  (cliente), y ademas consta de:
  o Nombre (nombre). Obligatorio.
  o Apellidos (apellidos). Obligatorio.
  o Telefono movil (movil). Obligatorio, puede haber varios.
  o Correo (email). Opcional, puede haber varios.
- Emplea entidades donde lo consideres oportuno, nombres de los meses, por ejemplo.

a) Modifica el documento XML, reservas.xml, para que se ajuste a las caracteristicas anteriores.(0,25 puntos)
b) Realiza un documento DTD, reservas.dtd, que valide el XML creado. (2,5 puntos)


reservas.dtd
------------

.. code-block:: dtd

    <?xml version="1.0" encoding="UTF-8"?>
    <!ELEMENT reservas (reserva*, cliente*)>

    <!ELEMENT reserva (fechaInicio, fechaFin, observaciones?)>
    <!ATTLIST reserva
        cliente IDREF #REQUIRED
        tipoHabitacion (SA | AD | MP |PC) #REQUIRED
        habitacion (Individual | Doble) #REQUIRED>

    <!ELEMENT fechaInicio EMPTY>
    <!ELEMENT fechaFin EMPTY>

    <!-- Podemos definir una entidad para las fechas 
    <!ENTITY % fecha 
        "año CDATA #REQUIRED
            mes (Enero | Febrero | Marzo | Abril | Mayo | Junio | Julio | 
            Agosto | Septiembre | Octubre | Noviembre | Diciembre) #REQUIRED
            dia CDATA #REQUIRED">
    <!ATTLIST fechaInicio %fecha; >	
    <!ATTLIST fechaFin %fecha; >

    O podríamos haber definido una entidad para los meses
    <!ENTITY % meses "(Enero|Febrero|Marzo|Abril|Mayo|Junio|Julio|Agosto|Septiembre|Octubre|Noviembre|Diciembre)">
    <!ATTLIST fechaInicio 
            año CDATA #REQUIRED 
            mes %meses; #REQUIRED 
            dia CDATA #REQUIRED>
    <!ATTLIST fechaFin 
            año CDATA #REQUIRED 
            mes %meses; #REQUIRED 
            dia CDATA #REQUIRED>
    -->

    <!ELEMENT observaciones (#PCDATA )>
        
    <!ELEMENT cliente (nombre, apellidos, movil+, correo*)>
    <!ATTLIST cliente
        id ID #REQUIRED>
        
    <!ELEMENT nombre (#PCDATA)>
    <!ELEMENT apellidos (#PCDATA)>
    <!ELEMENT movil (#PCDATA)>
    <!ELEMENT correo (#PCDATA)>

..

reservas.xml
------------

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <!DOCTYPE reservas SYSTEM "reservas.dtd"> 
    <reservas>
        <reserva cliente="C53454123X" tipoHabitacion="AD" habitacion="Doble">
            <fechaInicio año="2022" mes="Marzo" dia="18"></fechaInicio>
            <fechaFin año="2022" mes="Marzo" dia="20"></fechaFin>
            <observaciones>LLegan tarde, sobre las 23:30</observaciones>
        </reserva>
        <reserva cliente="C53454123X" tipoHabitacion="MP" habitacion="Individual">
            <fechaInicio año="2021" mes="Mayo" dia="16"></fechaInicio>
            <fechaFin año="2021" mes="Mayo" dia="17"></fechaFin>
            <observaciones>Salida a las 17:45</observaciones>
        </reserva>
        <reserva cliente="C44545123A" tipoHabitacion="PC" habitacion="Doble">
            <fechaInicio año="2022" mes="Abril" dia="14" />
            <fechaFin año="2022" mes="Abril" dia="18" />
        </reserva>
        <cliente id="C53454123X">
            <nombre>Clara</nombre>
            <apellidos>Lago Grau</apellidos>
            <movil>655656777</movil>
            <correo>clarita@email.com</correo>
        </cliente>
        <cliente id="C44545123A">
            <nombre>Fernando</nombre>
            <apellidos>Simón Soria</apellidos>
            <movil>785567811</movil>
        </cliente>
    </reservas>

..
