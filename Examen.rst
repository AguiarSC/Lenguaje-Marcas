ENUNCIADO
---------

::

  El Hotel Noa, precisa disponer de informacion para sus reservas de habitaciones, por lo que decidieron generar un documento 
  XML con la informacion de las mismas, asi como documentos de validacion. Aunque el tecnico informatico ha pensado en 
  generarlo dinamicamente a partir de la informacion almacenada en una base de datos, necesitan preparar un documento XML y 
  un DTD asociado que sirva como plantilla.
  
  Caracteristicas:
  
  - Un elemento raiz llamado reservas.
  
  - Todos los atributos del XML seran obligatorios.
  
  - Las reservas tienen un numero variable de reservas y clientes. Puede no haber.
  
  - Cada reserva tiene:
  
    - Atributos, todos obligatorios: codigo de cliente (cliente), formado por la letra C seguida del DNI (8 numeros y una 
      letra mayuscula), por ejemplo C53454123X; tipoHabitacion, que podra tener los valores: SA, AD, MP o PC, que indican 
      solo alojamiento, alojamiento y desayuno, media pension y pension completa; tipo de habitacion (habitacion), que 
      puede tener los valores, Doble o Individual.
  
    - Fecha de Inicio (fechaInicio), con atributos dia, mes y ano, obligatorios. Los tres deben ser atributos. El atributo mes 
      solo puede tomar los valores de los nombres de los meses del ano.
  
    - Fecha de fin (fechaFin), con atributos dia, mes y ano, obligatorios. Igual a la anterior.
  
    - Observaciones (observaciones), una parrafada, opcional para cada reserva y solo puede
      haber una.
  
  - Cada cliente tiene un atributo codigo (id) que debe estar relacionado con la reserva (cliente), y ademas consta de:
  
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

::

  Modifica el documento XML Schema que valide el documento XML generado en el ejercicio 1:
  - Define un tipo de dato, llamado "tipoFecha" para reutilizar y emplear en el elemento
  fechaInicio y fechaFin (0,8 puntos)
  - Define un tipo de dato simple, llamado "tipoIdCliente" para reutilizar en los atributos cliente e
  id y definir el patrón. (0,7 puntos)
  - Define ATRIBUTO "tipoHabitacion" restringir valores "AD", "MP", "PC" y "SA". (0,6 puntos)
  - Define ATRIBUTO "habitacion" restringir valores "Doble", "Individual". (0,6 puntos)
  - Define las referencias entre las claves. (0,8 puntos)


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

::

  Genera un nuevo documento XML a partir del creado en el ejercicio1, teniendo en cuenta que:
  - Existe un nuevo elemento, empleado, que aparece dentro de cliente. (0,25 puntos)
  - El empleado es un elemento que contiene sólo el texto con el código de empleado. El código de
  empleado es de la forma HC123456, esto es, dos letras mayúsculas seguidas de 6 números.
  (0,5 puntos)
  - Ahora, el cliente puede tener, o el elemento empleado o los elementos del ejercicio 1, pero
  no ambos a la vez. (1 punto)
  Modifica el documento XML Schema que valide el documento XML creado en esta opción:
  - Define un tipo de dato, llamado "tipoFecha" para reutilizar y emplear en el elemento
  fechaInicio y fechaFin (0,8 puntos)
  - Define un tipo de dato simple, llamado "tipoIdCliente" para reutilizar en los atributos cliente e
  id y definir el patrón. (0,7 puntos)
  - Define ATRIBUTO "tipoHabitacion" restringir valores "AD", "MP", "PC" y "SA". (0,6 puntos)
  - Define ATRIBUTO "habitacion" restringir valores "Doble", "Individual". (0,6 puntos)
  - Define las referencias entre las claves. (0,8 puntos)


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



.. raw:: html

    <embed>
        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <title></title>
    <meta http-equiv="content-type" content="text/html; charset=Cp1252">
    <style type="text/css">
      body { font-family: verdana, arial, helvetica, sans-serif; font-size: smaller; }
      table { padding: 0px;  margin: 0px; border: 1px solid #dddddd; border-collapse: collapse; }
      tr { font-size: smaller; }
      th, td { border: 1px solid #dddddd; padding: 2px; }
      /*table.info { background: #ffffff; }*/
      /*table.data { background: #ffffff; }*/
      /*tr.even { background: #ffffff; }*/
      /*tr.odd { background: #eeeeee; }*/
    </style>
  </head>
  <body>
    <table class="info">
<tr>
  <td class="label">Date:</td>
  <td class="value"><b>2024-05-31 11:52:22</b></td>
</tr>
<tr>
  <td class="label">Rows:</td>
  <td class="value"><b>12</b></td>
</tr>
<tr>
  <td class="label">Columns:</td>
  <td class="value"><b>8</b></td>
</tr>

    </table>
    <br>
    <table class="data">
      <tr>
        <th>empno</th>
        <th>ename</th>
        <th>job</th>
        <th>mgr</th>
        <th>hiredate</th>
        <th>sal</th>
        <th>comm</th>
        <th>deptno</th>
      </tr>
      <tr class="even">
        <td align="right">7369</td>
        <td>SMITH</td>
        <td>CLERK</td>
        <td align="right">7902</td>
        <td>1980-12-17</td>
        <td align="right">800.00</td>
        <td>(null)</td>
        <td align="right">20</td>
      </tr>
      <tr class="odd">
        <td align="right">7499</td>
        <td>ALLEN</td>
        <td>SALESMAN</td>
        <td align="right">7698</td>
        <td>1981-02-20</td>
        <td align="right">1600.00</td>
        <td align="right">300.00</td>
        <td align="right">30</td>
      </tr>
      <tr class="even">
        <td align="right">7566</td>
        <td>JONES</td>
        <td>MANAGER</td>
        <td align="right">7839</td>
        <td>1981-04-02</td>
        <td align="right">2975.00</td>
        <td>(null)</td>
        <td align="right">20</td>
      </tr>
      <tr class="odd">
        <td align="right">7698</td>
        <td>BLAKE</td>
        <td>MANAGER</td>
        <td align="right">7839</td>
        <td>1981-05-01</td>
        <td align="right">2850.00</td>
        <td>(null)</td>
        <td align="right">30</td>
      </tr>
      <tr class="even">
        <td align="right">7782</td>
        <td>CLARK</td>
        <td>MANAGER</td>
        <td align="right">7839</td>
        <td>1981-06-09</td>
        <td align="right">2450.00</td>
        <td>(null)</td>
        <td align="right">10</td>
      </tr>
      <tr class="odd">
        <td align="right">7788</td>
        <td>SCOTT</td>
        <td>ANALYST</td>
        <td align="right">7566</td>
        <td>1987-04-19</td>
        <td align="right">3000.00</td>
        <td>(null)</td>
        <td align="right">20</td>
      </tr>
      <tr class="even">
        <td align="right">7839</td>
        <td>KING</td>
        <td>PRESIDENT</td>
        <td>(null)</td>
        <td>1981-11-17</td>
        <td align="right">5000.00</td>
        <td>(null)</td>
        <td align="right">10</td>
      </tr>
      <tr class="odd">
        <td align="right">7844</td>
        <td>TURNER</td>
        <td>SALESMAN</td>
        <td align="right">7698</td>
        <td>1981-09-08</td>
        <td align="right">1500.00</td>
        <td align="right">0.00</td>
        <td align="right">30</td>
      </tr>
      <tr class="even">
        <td align="right">7876</td>
        <td>ADAMS</td>
        <td>CLERK</td>
        <td align="right">7788</td>
        <td>1987-05-23</td>
        <td align="right">1100.00</td>
        <td>(null)</td>
        <td align="right">20</td>
      </tr>
      <tr class="odd">
        <td align="right">7900</td>
        <td>JAMES</td>
        <td>CLERK</td>
        <td align="right">7698</td>
        <td>1981-12-03</td>
        <td align="right">950.00</td>
        <td>(null)</td>
        <td align="right">30</td>
      </tr>
      <tr class="even">
        <td align="right">7902</td>
        <td>FORD</td>
        <td>ANALYST</td>
        <td align="right">7566</td>
        <td>1981-12-03</td>
        <td align="right">3000.00</td>
        <td>(null)</td>
        <td align="right">20</td>
      </tr>
      <tr class="odd">
        <td align="right">7934</td>
        <td>MILLER</td>
        <td>CLERK</td>
        <td align="right">7782</td>
        <td>1982-01-23</td>
        <td align="right">1300.00</td>
        <td>(null)</td>
        <td align="right">10</td>
      </tr>
    </table>
    <p>[ Generated by: <a href="https://www.dbvis.com">DbVisualizer Free 24.1.3</a> ]</p>
  </body>
</html>

    </embed>
  
  </xs:schema>

.. 
