ENUNCIADO
---------

El Hotel Noa, precisa disponer de informacion para sus reservas de habitaciones, por lo que decidieron generar un documento XML con la informacion de las mismas, asi como documentos de validacion. Aunque el tecnico informatico ha pensado en generarlo dinamicamente a partir de la informacion almacenada en una base de datos, necesitan preparar un documento XML y un DTD asociado que sirva como plantilla.

Caracteristicas:

- Un elemento raiz llamado reservas.

- Todos los atributos del XML seran obligatorios.

- Las reservas tienen un numero variable de reservas y clientes. Puede no haber.

- Cada reserva tiene:

  - Atributos, todos obligatorios: codigo de cliente (cliente), formado por la letra C seguida del DNI (8 numeros y una letra mayuscula), por ejemplo C53454123X; tipoHabitacion, que podra tener los valores: SA, AD, MP o PC, que indican solo alojamiento, alojamiento y desayuno, media pension y pension completa; tipo de habitacion (habitacion), que puede tener los valores, Doble o Individual.

  - Fecha de Inicio (fechaInicio), con atributos dia, mes y ano, obligatorios. Los tres deben ser atributos. El atributo mes solo puede tomar los valores de los nombres de los meses del ano.

  - Fecha de fin (fechaFin), con atributos dia, mes y ano, obligatorios. Igual a la anterior.

  - Observaciones (observaciones), una parrafada, opcional para cada reserva y solo puede
    haber una.

- Cada cliente tiene un atributo codigo de cliente (id) que debe estar relacionado con la reserva (cliente), y ademas consta de:

  - Nombre (nombre). Obligatorio.

  - Apellidos (apellidos). Obligatorio.

  - Telefono movil (movil). Obligatorio, puede haber varios.

  - Correo (email). Opcional, puede haber varios.

- Emplea entidades donde lo consideres oportuno, nombres de los meses, por ejemplo.

a) Modifica el documento XML, reservas.xml, para que se ajuste a las caracteristicas anteriores.(0,25 puntos)
b) Realiza un documento DTD, reservas.dtd, que valide el XML creado. (2,5 puntos)


.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8" standalone="no"?>
  <reservas>
  	<reserva tipoHabitacion="AD" habitacion="Doble">
  		<cliente>C53454123X</cliente>
  		<fechaInicio año="2022" mes="Marzo" dia="18"></fechaInicio>
  		<fechaFin año="2022" mes="Marzo" dia="20"></fechaFin>
  		<observaciones>LLegan tarde, sobre las 23:30</observaciones>
  	</reserva>
  	<reserva tipoHabitacion="MP" habitacion="Individual">
  		<cliente>C53454123X</cliente>
  		<fechaInicio año="2021" mes="Mayo" d¡ia="16"></fechaInicio>
  		<fechaFin año="2021" mes="Mayo" dia="17"></fechaFin>
  		<observaciones>Salida a las 17:45</observaciones>
  	</reserva>
  	<reserva tipoHabitacion="PC" habitacion="Doble">
  		<cliente>C44545123A</cliente>
  		<fechaInicio año="2022" mes="Abril" dia="14" />
  		<fechaFin año="2022" mes="Abril" dia="18" />
  	</reserva>
  	<cliente id="C53454123X">
  		<nombre>Clara</nombre>
  		<apellidos>Lago Grau</apellidos>
  		<móvil>655656777</móvil>
  		<correo>clarita@email.com</correo>
  	</cliente>
  	<cliente id="C44545123A">
  		<nombre>Fernando</nombre>
  		<apellidos>Simón Soria</apellidos>
  		<móvil>785567811</móvil>
  	</cliente>
  </reservas>

..


PRIMER EJERCICIO. APARTADO A
----------------------------

.. code-block:: xml

  <!-- CORRECCIÓN:
  * Declaración DOCTYPE
  * Cliente como atributo en lugar de elemento hijo
  * Corrección del error tipográfico en d¡ia a dia
  * Tilde en <móvil> eliminada
  -->

  <!DOCTYPE reservas SYSTEM "reservas.dtd">

  <!-- ORIGINAL -->
  <reserva tipoHabitacion="AD" habitacion="Doble">
    <cliente>C53454123X</cliente>

  <!-- CORREGIDO -->
  <reserva cliente="C53454123X" tipoHabitacion="AD" habitacion="Doble">

  <!-- ORIGINAL -->
  <reserva tipoHabitacion="MP" habitacion="Individual">
    <cliente>C53454123X</cliente>
    <fechaInicio año="2021" mes="Mayo" d¡ia="16"></fechaInicio>

  <!-- CORREGIDO -->
  <reserva cliente="C53454123X" tipoHabitacion="MP" habitacion="Individual">
    <fechaInicio año="2021" mes="Mayo" dia="16"></fechaInicio>

  <!-- ORIGINAL -->
  <cliente id="C53454123X">
    <nombre>Clara</nombre>
    ...
    <móvil>655656777</móvil>
  </cliente>

  <!-- CORREGIDO -->
  <cliente id="C53454123X">
    <nombre>Clara</nombre>
    ...
    <movil>655656777</movil>
  </cliente>

..


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


PRIMER EJERCICIO. APARTADO B
----------------------------

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
        mes (Enero | Febrero | Marzo | Abril | Mayo | Junio | Julio | Agosto | Septiembre | Octubre | Noviembre | Diciembre) #REQUIRED
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


SEGUNDO EJERCICIO. APARTADO A
-----------------------------

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8" standalone="no"?>
  <reservas xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  	xsi:noNamespaceSchemaLocation="reservas2a.xsd">
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


.. code-block:: xsd

  <?xml version="1.0" encoding="UTF-8"?>
  <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  
  	<!-- TIPO DE DATO complejo para guardar fechas:  tipoFecha -->
  	<!-- Define un tipo de dato, llamado "tipoFecha" para reutilizar 
  	y emplear en el elemento fechaInicio y fechaFin -->
  	<xs:complexType name="tipoFecha">
  		<xs:attribute name="año" type="xs:gYear" use="required"/>
  		<xs:attribute name="mes" use="required">
  			<xs:simpleType>
  				<xs:restriction base="xs:string">
  					<xs:enumeration value="Enero"/>
  					<xs:enumeration value="Febrero"/>
  					<xs:enumeration value="Marzo"/>
  					<xs:enumeration value="Abril"/>
  					<xs:enumeration value="Mayo"/>
  					<xs:enumeration value="Junio"/>
  					<xs:enumeration value="Julio"/>
  					<xs:enumeration value="Agosto"/>
  					<xs:enumeration value="Septiembre"/>
  					<xs:enumeration value="Octubre"/>
  					<xs:enumeration value="Noviembre"/>
  					<xs:enumeration value="Diciembre"/>
  				</xs:restriction>
  			</xs:simpleType>
  		</xs:attribute>
  		<xs:attribute name="dia" type="xs:unsignedByte" use="required"/>
  	</xs:complexType>
  	
  	<!-- TIPO DE DATO simple para identificador cliente:  tipoIdCliente -->
  	<!-- Define un tipo de dato simple, llamado "tipoIdCliente" para reutilizar 
  	en los atributos cliente e id y definir el patrón.-->
  	<xs:simpleType name="tipoIdCliente">
  		<xs:restriction base="xs:string">
  			<xs:pattern value="[C]\d{8}[A-Z]"/>
  		</xs:restriction>
  	</xs:simpleType>
  	
  	<!-- Define ATRIBUTO "tipoHabitación" 
  	restringir valores "AD", "MP", "PC" y "SA"  -->
  	<xs:attribute name="tipoHabitacion">
  		<xs:simpleType>
  			<xs:restriction base="xs:string">
  				<xs:enumeration value="AD"/>
  				<xs:enumeration value="MP"/>
  				<xs:enumeration value="PC"/>
  				<xs:enumeration value="SA"/>
  			</xs:restriction>
  		</xs:simpleType>
  	</xs:attribute>
  	
  	<!-- Define ATRIBUTO "habitación" 
  	restringir valores "Doble", "Individual"  -->
  	<xs:attribute name="habitacion">
  		<xs:simpleType>
  			<xs:restriction base="xs:string">
  				<xs:enumeration value="Doble"/>
  				<xs:enumeration value="Individual"/>
  			</xs:restriction>
  		</xs:simpleType>
  	</xs:attribute>
  		
  	<!-- ELEMENTOS PRINCIPAIS -->
  	
  	<!-- reservas -->
  	<xs:element name="reservas">
  		<xs:complexType>
  			<xs:sequence>
  				<xs:element ref="reserva" minOccurs="0" maxOccurs="unbounded"/>
  				<xs:element ref="cliente" minOccurs="0" maxOccurs="unbounded"/>
  			</xs:sequence>
  		</xs:complexType>
  		<!--  Define las REFERENCIAS ENTRE las claves del CLIENTE y RESERVA -->
  		<xs:key name="clienteKey">
  			<xs:selector xpath="cliente"/>
  			<xs:field xpath="@id"/>
  		</xs:key>
  		<!-- keyref especifica que el valor del atributo cliente del elemento reserva 
  		corresponde al atributo id del elemento cliente -->
  		<xs:keyref name="reserva" refer="clienteKey">
  			<xs:selector xpath="reserva"/>
  			<xs:field xpath="@cliente"/>
  		</xs:keyref>
  	</xs:element>
  		
  	<!-- reserva -->
  	<xs:element name="reserva">
  		<xs:complexType>
  			<xs:sequence>
  				<xs:element name="fechaInicio" type="tipoFecha"/>
  				<xs:element name="fechaFin" type="tipoFecha"/>
  				<xs:element name="observaciones" type="xs:string" minOccurs="0"/>
  			</xs:sequence>
  			<xs:attribute name="cliente" type="tipoIdCliente" use="required"/>
  			<xs:attribute ref="tipoHabitacion" use="required"/>
  			<xs:attribute ref="habitacion" use="required"/>
  		</xs:complexType>
  	</xs:element>
  		
  	<!-- cliente -->
  	<xs:element name="cliente">
  		<xs:complexType>
  			<xs:sequence>
  				<xs:element name="nombre" type="xs:string"/>
  				<xs:element name="apellidos" type="xs:string"/>
  				<xs:element name="movil" type="xs:int" minOccurs="0" maxOccurs="unbounded"/>
  				<xs:element name="correo" type="xs:string" minOccurs="0"/>
  			</xs:sequence>
  			<xs:attribute name="id" type="tipoIdCliente" use="required"/>
  		</xs:complexType>
  	</xs:element>
  	
  </xs:schema>

..


SEGUNDO EJERCICIO. APARTADO B
-----------------------------

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8" standalone="no"?>
  <reservas xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  	xsi:noNamespaceSchemaLocation="reservas2b.xsd">
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
  	<cliente id="C37545123A">
  		<empleado>NB567890</empleado>
  	</cliente>
  </reservas>

..


.. code-block:: xsd

  <?xml version="1.0" encoding="UTF-8"?>
  <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  
  	<!-- TIPO DE DATO complejo para guardar fechas:  tipoFecha -->
  	<!-- Define un tipo de dato, llamado "tipoFecha" para reutilizar 
  	y emplear en el elemento fechaInicio y fechaFin -->
  	<xs:complexType name="tipoFecha">
  		<xs:attribute name="año" type="xs:gYear" use="required" />
  		<xs:attribute name="mes" use="required">
  			<xs:simpleType>
  				<xs:restriction base="xs:string">
  					<xs:enumeration value="Enero" />
  					<xs:enumeration value="Febrero" />
  					<xs:enumeration value="Marzo" />
  					<xs:enumeration value="Abril" />
  					<xs:enumeration value="Mayo" />
  					<xs:enumeration value="Junio" />
  					<xs:enumeration value="Julio" />
  					<xs:enumeration value="Agosto" />
  					<xs:enumeration value="Septiembre" />
  					<xs:enumeration value="Octubre" />
  					<xs:enumeration value="Noviembre" />
  					<xs:enumeration value="Diciembre" />
  				</xs:restriction>
  			</xs:simpleType>
  		</xs:attribute>
  		<xs:attribute name="dia" type="xs:unsignedByte" use="required" />
  	</xs:complexType>
  
  	<!-- TIPO DE DATO simple para identificador cliente:  tipoIdCliente -->
  	<!-- Define un tipo de dato simple, llamado "tipoIdCliente" para reutilizar 
  	en los atributos cliente e id y definir el patrón.-->
  	<xs:simpleType name="tipoIdCliente">
  		<xs:restriction base="xs:string">
  			<xs:pattern value="[C]\d{8}[A-Z]" />
  		</xs:restriction>
  	</xs:simpleType>
  
  	<!-- TIPO DE DATO simple para identificador empleado:  tipoEmpleado-->
  	<!-- Define un tipo de dato simple, llamado "tipoIdCliente" para reutilizar 
  	en los atributos cliente e id y definir el patrón.-->
  	<xs:simpleType name="tipoEmpleado">
  		<xs:restriction base="xs:string">
  			<xs:pattern value="[A-Z]{2}\d{6}" />
  		</xs:restriction>
  	</xs:simpleType>
  
  	<!-- Define ATRIBUTO "tipoHabitación" restringir valores 
  	"AD", "MP", "PC" y "SA"  -->
  	<xs:attribute name="tipoHabitacion">
  		<xs:simpleType>
  			<xs:restriction base="xs:string">
  				<xs:enumeration value="AD" />
  				<xs:enumeration value="MP" />
  				<xs:enumeration value="PC" />
  				<xs:enumeration value="SA" />
  			</xs:restriction>
  		</xs:simpleType>
  	</xs:attribute>
  
  	<!-- Define ATRIBUTO "habitación" restringir valores 
  	"Doble", "Individual"  -->
  	<xs:attribute name="habitacion">
  		<xs:simpleType>
  			<xs:restriction base="xs:string">
  				<xs:enumeration value="Doble" />
  				<xs:enumeration value="Individual" />
  			</xs:restriction>
  		</xs:simpleType>
  	</xs:attribute>
  
  	<!-- ELEMENTOS PRINCIPAIS -->
  
  	<!-- reservas -->
  	<xs:element name="reservas">
  		<xs:complexType>
  			<xs:sequence>
  				<xs:element ref="reserva" minOccurs="0" maxOccurs="unbounded" />
  				<xs:element ref="cliente" minOccurs="0" maxOccurs="unbounded" />
  			</xs:sequence>
  		</xs:complexType>
  		<!--  Define las REFERENCIAS ENTRE las claves del CLIENTE y RESERVA -->
  		<xs:key name="clienteKey">
  			<xs:selector xpath="cliente" />
  			<xs:field xpath="@id" />
  		</xs:key>
  		<!-- keyref especifica que el valor del atributo cliente del elemento reserva 
  			corresponde al atributo id del elemento cliente -->
  		<xs:keyref name="reserva" refer="clienteKey">
  			<xs:selector xpath="reserva" />
  			<xs:field xpath="@cliente" />
  		</xs:keyref>
  	</xs:element>
  
  	<!-- reserva -->
  	<xs:element name="reserva">
  		<xs:complexType>
  			<xs:sequence>
  				<xs:element name="fechaInicio" type="tipoFecha" />
  				<xs:element name="fechaFin" type="tipoFecha" />
  				<xs:element name="observaciones" type="xs:string" minOccurs="0" />
  			</xs:sequence>
  			<xs:attribute name="cliente" type="tipoIdCliente" use="required" />
  			<xs:attribute ref="tipoHabitacion" use="required" />
  			<xs:attribute ref="habitacion" use="required" />
  		</xs:complexType>
  	</xs:element>
  
  	<!-- cliente -->
  	<xs:element name="cliente">
  		<xs:complexType>
  			<xs:choice>
  				<xs:sequence>
  					<xs:element name="nombre" type="xs:string" />
  					<xs:element name="apellidos" type="xs:string" />
  					<xs:element name="movil" type="xs:int" minOccurs="0" maxOccurs="unbounded" />
  					<xs:element name="correo" type="xs:string" minOccurs="0" />
  				</xs:sequence>
  				<xs:element name="empleado" type="tipoEmpleado" />
  			</xs:choice>
  			<xs:attribute name="id" type="tipoIdCliente" use="required" />
  		</xs:complexType>
  	</xs:element>
  
  </xs:schema>

.. 
