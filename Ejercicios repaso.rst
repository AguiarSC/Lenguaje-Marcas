Ejercicio 1
-----------

Definir una DTD que valide el documento XML que se muestra a continuacion.
Construir un documento XML con DTD interna y otro con DTD externa. Comprobar la buena formacion y la validez del documento en ambos casos.
Se deben tener en cuenta las siguientes caracteristicas:

• El numero de factura (n_fac), numero de cliente (n_cli) y numero de pedido (n_ped) son valores unicos, por cada factura, cliente y pedido distintos, y son obligatorios.

• Los numeros de telefono (telefono) y fax (fax) de la empresa no tienen porque aparecer en la factura, pero siempre que lo hagan deberan tener los mismos valores (telefono 917776688, fax 917776699).

• La forma de pago puede tomar los valores “efectivo”, “tarjeta” y “plazos”.

• La moneda tiene que aparecer siempre, y siempre toma al valor “euro”.

• El iva tiene que aparecer siempre, y su valor no puede contener caracteres especiales.


.. code-block:: xml
	
	<?xml version="1.0" encoding="UTF-8"?>
	<factura n_fac="f999">
	  <datos_empresa>
	    <nombre>Equipos Digitales S.L.</nombre>
	    <dir>Av. Valladolid</dir>
	    <poblacion cod_postal="28043">Madrid</poblacion>
	    <provincia>Madrid</provincia>
	    <cif>Q-9876543</cif>
	    <telefono/>
	  </datos_empresa>
	  <datos_cliente n_cli="c879">
	    <nombre>Dario, Bueno Gutierrez</nombre>
	    <dir_env>Av. Oporto nº7 4ºd</dir_env>
	    <poblacion cod_postal="28043">Madrid</poblacion>
	    <provincia>Madrid</provincia>
	  </datos_cliente>
	  <datos_factura n_ped="p731" iva="16" f_pago="efectivo" moneda="euro">
	    <fecha>12-01-2005</fecha>
	    <linea>
	      <ref>MII93000F/8</ref>
	      <desc>MICRO PENTIUM IV 3000MHZ FB800</desc>
	      <cant>1</cant>
	      <precio>230</precio>
	      <importe>266,80</importe>
	    </linea>
	    <linea>
	      <ref>MB8QDIP4</ref>
	      <desc>PLACA BASE QDI P4</desc>
	      <cant>1</cant>
	      <precio>180</precio>
	      <importe>208,80</importe>
	    </linea>
	    <linea>
	      <ref>MEDD512M32</ref>
	      <desc>DIMM DDR 512MB 3200</desc>
	      <cant>2</cant>
	      <precio>40</precio>
	      <importe>92,80</importe>
	    </linea>
	    <linea>
	      <ref>HD250GSA7</ref>
	      <desc>DISCO DURO 250GB S-ATA 7200</desc>
	      <cant>4</cant>
	      <precio>120</precio>
	      <importe>556,80</importe>
	    </linea>
	    <base>970,00</base>
	    <cuota_iva>155,20</cuota_iva>
	    <total>1125,20</total>
	  </datos_factura>
	</factura>
	
..

Solución
--------

.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE factura SYSTEM "Factura.dtd">
	<factura n_fac="f999"> 
	  <datos_empresa> 
	    <nombre>Equipos Digitales S.L.</nombre> 
	    <dir>Av. Valladolid</dir> 
	    <poblacion cod_postal="28043">Madrid</poblacion> 
	    <provincia>Madrid</provincia> 
	    <cif>Q-9876543</cif> 
	    <telefono/> 
	  </datos_empresa> 
	  <datos_cliente n_cli="c879"> 
	    <nombre>Dario, Bueno Gutierrez</nombre> 
	    <dir_env>Av. Oporto nº7 4ºd</dir_env> 
	    <poblacion cod_postal="28043">Madrid</poblacion> 
	    <provincia>Madrid</provincia> 
	  </datos_cliente> 
	  <datos_factura n_ped="p731" iva="16" f_pago= "efectivo" moneda="euro"> 
	    <fecha>12-01-2005</fecha> 
	    <linea> 
	      <ref>MII93000F/8</ref> 
	        <desc>MICRO PENTIUM IV 3000MHZ FB800</desc> 
	        <cant>1</cant> 
	        <precio>230</precio> 
	        <importe>266,80</importe> 
	    </linea> 
	    <linea> 
	      <ref>MB8QDIP4</ref> 
	      <desc>PLACA BASE QDI P4</desc> 
	      <cant>1</cant> 
	      <precio>180</precio> 
	      <importe>208,80</importe> 
	    </linea> 
	    <linea> 
	      <ref>MEDD512M32</ref> 
	      <desc>DIMM DDR 512MB 3200</desc> 
	      <cant>2</cant> 
	      <precio>40</precio> 
	      <importe>92,80</importe> 
	    </linea> 
	    <linea> 
	      <ref>HD250GSA7</ref> 
	      <desc>DISCO DURO 250GB S-ATA 7200</desc> 
	      <cant>4</cant> 
	      <precio>120</precio> 
	      <importe>556,80</importe> 
	    </linea> 
	    <base>970,00</base> 
	    <cuota_iva>155,20</cuota_iva>
	    <total>1125,20</total> 
	  </datos_factura>
	</factura> 

..

.. code-block:: dtd

 <!ELEMENT factura (datos_empresa, datos_cliente, datos_factura)>
 <!ELEMENT datos_empresa (nombre,dir,poblacion,provincia,cif,telefono?,fax?)>
 <!ELEMENT datos_cliente (nombre, dir_env, poblacion, provincia)>
 <!ELEMENT datos_factura (fecha, linea*, base, cuota_iva, total)>
 <!ELEMENT linea (ref, desc, cant, precio, importe)>
 <!ELEMENT ref (#PCDATA)>
 <!ELEMENT desc (#PCDATA)>
 <!ELEMENT cant (#PCDATA)>
 <!ELEMENT precio (#PCDATA)>
 <!ELEMENT importe (#PCDATA)>
 <!ELEMENT nombre (#PCDATA)>
 <!ELEMENT dir (#PCDATA)>
 <!ELEMENT poblacion (#PCDATA)>
 <!ELEMENT provincia (#PCDATA)>
 <!ELEMENT cif (#PCDATA)>
 <!ELEMENT telefono EMPTY>
 <!ELEMENT fax EMPTY>
 <!ELEMENT dir_env (#PCDATA)>
 <!ELEMENT fecha (#PCDATA)>
 <!ELEMENT base (#PCDATA)>
 <!ELEMENT cuota_iva (#PCDATA)>
 <!ELEMENT total (#PCDATA)>

 <!-- Definicion de atributos -->
 <!ATTLIST factura n_fac ID #REQUIRED>
 <!ATTLIST telefono num_tel CDATA #FIXED "917776688">
 <!ATTLIST fax num_fax CDATA #FIXED "917776699">
 <!ATTLIST datos_cliente n_cli ID #REQUIRED>
 <!ATTLIST datos_factura n_ped ID #REQUIRED>
 <!ATTLIST datos_factura iva NMTOKEN #REQUIRED>
 <!ATTLIST datos_factura f_pago (efectivo|tarjeta|plazos) #REQUIRED>
 <!ATTLIST datos_factura moneda CDATA #FIXED "euro">
 <!ATTLIST poblacion cod_postal CDATA "">

..


Ejercicio 2
-----------

Definir una DTD que valide el documento XML que se muestra a continuacion. Construir un documento XML con DTD interna y otro con DTD externa. Comprobar la buena formacion y la validez del documento en ambos casos.
Se deben tener en cuenta las siguientes caracteristicas:

• El titulo original de una pelicula solo aparecera cuando la pelicula no sea espanola.

• Es posible que en un momento dado una pelicula este pendiente de clasificacion. En caso de que este clasificada siempre debera indicar los anos para los que se recomienda: tp (todos los publicos), 8, 12, 16 o 18.

• No siempre existe una web con la informacion de la pelicula.

• Se quiere guardar informacion sobre el fichero grafico que contiene el cartel de la pelicula. Este fichero no siempre esta disponible.

• En caso de que no se proporcione el ano de una pelicula se asumira que es el 2003.

• En el reparto debera aparecer un actor como minimo.


.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE cartelera SYSTEM "Cartelera.dtd">
	<cartelera>
	  <pelicula codigo="p1" duracion="152" ano="2002">
	    <titulo>AQUELLAS JUERGAS UNIVERSITARIAS</titulo>
	    <titulo_original>Old School</titulo_original>
	    <nacionalidad>Estados Unidos</nacionalidad>
	    <genero>Comedia</genero>
	    <clasificacion edad="tp"/>
	    <sinopsis>
	      Mitch, Frank y Beanie son tres amigos treintaneros cuyas vidas no son
	      exactamente lo que esperaban. Mitch tiene una novia un poco alocada.
	      Frank se ha casado y su matrimonio nada tiene que ver con las juergas
	      salvajes que organizaban anos atras. Y Beanie es un padre de familia que
	      se muere por recuperar su alocada juventud. Pero las cosas cambian
	      cuando Beanie sugiere que creen su propia fraternidad, en la nueva casa
	      que Mitch tiene junto al campus de la universidad. Una ocasion para
	      revivir tiempos gloriosos, hacer nuevos amigos y de volver a sus viejas,
	      salvajes y desmadradas juergas de estudiantes.
	    </sinopsis>
	    <director>Todd Philips</director>
	    <reparto>
	      <actor>Luke Wilson</actor>
	      <actor>Will Farrel</actor>
	      <actor>Vince Vaughn</actor>
	    </reparto>
	    <web>http://www.uip.es</web>
	    <cartel>caratulas/Aquellas juergas.jpg</cartel>
	  </pelicula>
	  <pelicula codigo="p17" duracion="06">
	    <titulo>EL ORO DE MOSCu</titulo>
	    <nacionalidad>Espana</nacionalidad>
	    <genero>Comedia</genero>
	    <sin_clasificar/>
	    <sinopsis>
	      Por una extrana coincidencia del destino, alguien recibe una
	      informacion extraconfidencial de un anciano en sus ultimos
	      segundos de vida: el secreto mejor guardado de la historia. El
	      receptor, un trabajador de hospital, se lo comunica secretamente
	      a un supuesto amigo. Ambos inician una aventura rocambolesca y
	      llena de misterio. Ante la inutilidad de sus intentos y muy a
	      su pesar, tienen que recurrir a otras personas que asi mismo van
	      cayendo en el pozo sin fondo que conlleva descifrar el enigma.
	    </sinopsis>
	    <director>Jesus Bonilla</director>
	    <reparto>
	      <actor>Jesus Bonilla</actor>
	      <actor>Santiago Segura</actor>
	      <actor>Alfredo Landa</actor>
	      <actor>Concha Velasco</actor>
	      <actor>Antonio Resines</actor>
	      <actor>Gabino Diego</actor>
	      <actor>Maria Barranco</actor>
	    </reparto>
	  </pelicula>
	</cartelera>

..

Solución 
--------

.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE cartelera SYSTEM "Cartelera.dtd">
	<cartelera>
		<pelicula codigo="p1" duracion="152" ano="2002">
			<titulo>AQUELLAS JUERGAS UNIVERSITARIAS</titulo>
			<titulo_original>Old School</titulo_original>
			<nacionalidad>Estados Unidos</nacionalidad>
			<genero>Comedia</genero>
			<clasificacion edad="tp"/>
			<sinopsis>
				Mitch, Frank y Beanie son tres amigos treintaneros cuyas vidas no son exactamente lo que esperaban. Mitch tiene una novia ninfomana que se 				mete en la cama con el primero que agarra. Frank se ha casado y su 				matrimonio nada tiene que ver con las juergas salvajes que organizaban 			anos atras. Y Beanie es un padre de familia que se muere por recuperar 				su alocada juventud. Pero las cosas cambian cuando Beanie sugiere que 				creen su propia fraternidad, en la nueva casa que Mitch tiene junto al 				campus de la universidad. Una ocasion para revivir tiempos gloriosos, 				hacer nuevos amigos y de volver a sus viejas, salvajes y desmadradas 				juergas de estudiantes.
			</sinopsis>
			<director>Todd Philips</director>
			<reparto>
				<actor>Luke Wilson</actor>
				<actor>Will Farrel</actor>
				<actor>Vince Vaughn</actor>
			</reparto>
			<web>http://www.uip.es</web>
			<cartel>caratulas/Aquellas juergas.jpg</cartel>
		</pelicula>
		<pelicula codigo="p17" duracion="06">
			<titulo>EL ORO DE MOSCu</titulo>
			<nacionalidad>Espana</nacionalidad>
			<genero>Comedia</genero>
			<sin_clasificar/>
			<sinopsis>
	Por una extrana coincidencia del destino, alguien recibe una informacion extraconfidencial de un anciano en sus ultimos segundos de vida: el secreto mejor guardado de la Historia. El receptor, un trabajador de hospital, se lo comunica secretamente a un supuesto amigo. Ambos inician una aventura rocambolesca y llena de misterio. Ante la inutilidad de sus intentos y muy a
	su pesar, tienen que recurrir a otras personas que asi mismo van cayendo en el pozo sin fondo que conlleva descifrar el enigma.
			</sinopsis>
			<director>Jesus Bonilla</director>
			<reparto>
				<actor>Jesus Bonilla</actor>
				<actor>Santiago Segura</actor>
				<actor>Alfredo Landa</actor>
				<actor>Concha Velasco</actor>
				<actor>Antonio Resines</actor>
				<actor>Gabino Diego, Maria Barranco</actor>
				<actor>Maria Barranco</actor>
			</reparto>
		</pelicula>
	</cartelera>

..

.. code-block:: dtd

	<!-- DEFINICIoN DE ELEMENTOS -->
	 <!ELEMENT cartelera (pelicula)*>
	 <!ELEMENT pelicula (titulo, titulo_original?, nacionalidad, genero, (clasificacion | sin_clasificar), sinopsis, director, reparto, web?, cartel?) >
	 <!ELEMENT titulo (#PCDATA)>
	 <!ELEMENT titulo_original (#PCDATA)>
	 <!ELEMENT nacionalidad (#PCDATA)>
	 <!ELEMENT genero (#PCDATA)>
	 <!ELEMENT clasificacion EMPTY>
	 <!ELEMENT sin_clasificar EMPTY>
	 <!ELEMENT sinopsis (#PCDATA)>
	 <!ELEMENT director (#PCDATA)>
	 <!ELEMENT reparto (actor)+>
	 <!ELEMENT web (#PCDATA)>
	 <!ELEMENT cartel (#PCDATA)>
	 <!ELEMENT actor (#PCDATA)>
	
	 <!-- Definicion de atributos -->
	 <!ATTLIST pelicula codigo ID #REQUIRED>
	 <!ATTLIST pelicula duracion CDATA "">
	 <!ATTLIST pelicula ano CDATA "2003">
	 <!ATTLIST clasificacion edad (8 | 12 | 16 | 18 | tp) #REQUIRED>

..

XSD
======

Enunciado
------------

Creación de documentos XML e esquemas XML completos. Neste exemplo imos crear esquemas XML que respondan as especificacións que se determinan que deben cumprir os documentos XML que se queren validar, empregando todos os conceptos explicados na UD. Elaboraremos o esquema XML tendo en conta que:

• O número de rúa debe ser un número positivo que non superará o 2000.

• O código postal consta unicamente de 5 díxitos.

• Valida que os meses do ano teñan un valor correcto.

• O ano debe ter un valor de ano correcto

• O alquiler é verdadeiro ou falso, e é obrigatorio.

• O valor debe ser un número con dous decimais

Solución
----------
.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<edificio alquiler="verdadeiro" valor="410.50"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="edificio.xsd">
	    <enderezo>
	        <rua>Ponzano</rua>
	        <numero>66</numero>
	        <poboacion>Madrid</poboacion>
	        <provincia>Madrid</provincia>
	        <codigoPostal>28003</codigoPostal>
	    </enderezo>
	    <dataConstrucion mes="Febreiro" ano="1989" />
	    <material>formigón</material>
	</edificio>

..

.. code-block:: xsd

	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	
	<xs:element name="edificio">
	<xs:complexType>
	    <xs:sequence>
	        <xs:element ref="enderezo"/>
	        <xs:element ref="dataConstrucion"/>
	        <xs:element ref="material" minOccurs="0"/>
	    </xs:sequence>
	    <xs:attribute name="valor" type="tipoValor"/>
	    <!--O alquiler é verdadeiro ou falso, e é obrigatorio.-->
	    <xs:attribute name="alquiler" use="required">
	    <xs:simpleType>
	        <xs:restriction base="xs:NMTOKEN">
	          <xs:enumeration value="verdadeiro"/>
	          <xs:enumeration value="falso"/>
	        </xs:restriction>
	    </xs:simpleType>
	    </xs:attribute>
	</xs:complexType>
	</xs:element>
	
	<xs:element name="enderezo" type="enderezo"/>
	<xs:element name="dataConstrucion" type="tipoDataConstrucion"/>
	<xs:element name="material" type="xs:string"/>
	
	<xs:complexType name="enderezo">
	<xs:sequence>
	    <xs:element ref="rua"/>
	    <xs:element ref="numero"/>
	    <xs:element ref="poboacion"/>
	    <xs:element ref="provincia"/>
	    <xs:element ref="codigoPostal"/>
	</xs:sequence>
	</xs:complexType>
	
	<xs:element name="rua" type="xs:string"/>
	<xs:element name="numero" type="tipoNumero"/>
	<xs:element name="poboacion" type="xs:string"/>
	<xs:element name="provincia" type="xs:string"/>
	<xs:element name="codigoPostal" type="tipoCodigoPostal"/>
	
	<!--O código postal consta unicamente de 5 díxitos.-->
	<xs:simpleType name="tipoCodigoPostal">
	<xs:restriction base="xs:string">
	    <xs:pattern value="\d{5}"/>
	</xs:restriction>
	</xs:simpleType>
	
	<!--O valor debe ser un número con dous decimais.-->
	<xs:simpleType name="tipoValor">
	<xs:restriction base="xs:decimal">
	    <xs:fractionDigits value="2"/>
	</xs:restriction>
	</xs:simpleType>
	
	<!--O número de rúa debe ser un número positivo que non superará o 2000.-->
	<xs:simpleType name="tipoNumero">
	<xs:restriction base="xs:unsignedShort">
	    <xs:maxInclusive value="2000"/>
	</xs:restriction>
	</xs:simpleType>
	
	<xs:complexType name="tipoDataConstrucion">
	    <xs:attribute name="mes" type="tipoMes" use="required"/>
	    <xs:attribute name="ano" type="xs:gYear" use="required"/><!--ano con 4 dígitos-->
	</xs:complexType>
	
	<!--Valida que os meses do ano teñan un valor correcto.-->
	<xs:simpleType name="tipoMes">
	    <xs:restriction base="xs:string">
	        <xs:enumeration value="Xaneiro"/>
	        <xs:enumeration value="Febreiro"/>
	        <xs:enumeration value="Marzo"/>
	        <xs:enumeration value="Abril"/>
	        <xs:enumeration value="Maio"/>
	        <xs:enumeration value="Xuño"/>
	        <xs:enumeration value="Xullo"/>
	        <xs:enumeration value="Agosto"/>
	        <xs:enumeration value="Setembro"/>
	        <xs:enumeration value="Outubro"/>
	        <xs:enumeration value="Novembro"/>
	        <xs:enumeration value="Decembro"/>
	    </xs:restriction>
	</xs:simpleType>
	
	</xs:schema>

..

Enunciado2
------------

Creación de documentos XML e esquemas XML completos. Neste exemplo imos crear esquemas XML que respondan as especificacións que se determinan que deben cumprir os documentos XML que se queren validar, empregando todos os conceptos explicados na UD. Elaboraremos o esquema XML tendo en conta que:

• Introducimos un elemento para almacenar o NSS dos empregados, que deberá estar formado por doce díxitos.

• Queremos introducir información de qué empregados son os xefes de departamento, validando que estes sexan empregados válidos.

• Crearemos un elemento contactos que permita gardar ata catro teléfonos de cada empregado. No caso de non coñecer ningún teléfono do empregado deberemos deixar constancia disto asignandolle un valor nulo a este elemento. O formato do teléfono será de nove díxigos. Por exemplo: <contactos>989898989 987654321 978787878</contactos>

• O esquema debe estar documentado para que informa sobre as validacións que se fan neste

Solución
----------

.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<empresa  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			 xsi:noNamespaceSchemaLocation="empresa.xsd">
	    <empregado>
	        <nss>272727272727</nss>
	        <nome>Iria</nome>
	        <departamento>IFC</departamento>
	        <contactos>999888777 987987789</contactos>
	    </empregado>
	    <empregado>
	      <nss>151515151515</nss>
	      <nome>Mariña</nome>
	      <departamento>IFC</departamento>
	      <contactos>989898989 987654321 978787878</contactos>
	    </empregado>
	    <empregado>
	       <nss>272727363636</nss>
	      <nome>Xoel</nome>
	      <departamento>CON</departamento>
	    </empregado>
	    <departamento codigo="IFC" xefe="272727363636">
	       <nome>Informática</nome>
	    </departamento>
	    <departamento codigo="CON" xefe="272727272727">
	        <nome>Contabilidade</nome>
	    </departamento>
	</empresa>

..

.. code-block:: xsd

	<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:annotation>
	    <xs:documentation>
	        Valida que o empregado pertenza a un departamento existente. 
	        Garda información de quén é o xefe de departamento.
			    O NSS debe ter 12 díxitos.
			    Poden almacenarse ata 4 teléfonos nunha lista chamada contactos.
	    </xs:documentation>
	</xs:annotation>
	<xs:element name="empresa">
	  <xs:complexType>
	    <xs:sequence>
	        <xs:element name="empregado" type="tipoEmpregado" maxOccurs="200"/>
	        <xs:element name="departamento" type="tipoDepartamento" maxOccurs="8"/>
	    </xs:sequence>
	  </xs:complexType>
	 
	 <!-- Os departamentos onde traballan os empleados deben existir--> 
	  <xs:key name="depUnico">
	    <xs:selector xpath="departamento"/>
	    <xs:field xpath="@codigo"/>
	  </xs:key>
	  <xs:keyref name="departamentoPertence" refer="depUnico">
	        <xs:selector xpath="empregado"/>
	        <xs:field xpath="departamento"/>
	  </xs:keyref> 
	  
	  <!--Queremos introducir información de qué empregados son os xefes de departamento,
	   validando que estes sexan empregados válidos -->
	  <xs:key name="xefeDepartamento">
	    <xs:selector xpath="empregado"/>
	    <xs:field xpath="nss"/>
	  </xs:key>
	  <xs:keyref name="departamentoXefe" refer="xefeDepartamento">
	        <xs:selector xpath="departamento"/>
	        <xs:field xpath="@xefe"/>
	  </xs:keyref>
	</xs:element>
	
	  <xs:complexType name="tipoEmpregado">
	    <xs:sequence>
	        <xs:element name="nss" type="tipoNSS"/>
	        <xs:element name="nome" type="xs:string"/>
	        <xs:element name="departamento" type="xs:string"/>
	        <!--Crea un elemento contactos que permita gardar ata catro teléfonos de cada empregado.-->
	        <xs:element name="contactos" type="telefonos" minOccurs="0"/>
	    </xs:sequence>
	  </xs:complexType>
	  
	  <xs:complexType name="tipoDepartamento">
	    <xs:sequence>
	        <xs:element name="nome" type="xs:string"/>
	    </xs:sequence>
	    <xs:attribute name="codigo" type="xs:string" use="required"/>
	    <xs:attribute name="xefe" type="tipoNSS" use="required"/>
	  </xs:complexType>  
	
	<!--  O NSS dos empregados, que deberá estar formado por doce díxitos  -->
	  <xs:simpleType name="tipoNSS">
	    <xs:restriction base="xs:string">
	            <xs:pattern value="[0-9]{12}"/>
	    </xs:restriction>
	  </xs:simpleType>
	
	<!--O formato do teléfono será de nove díxigos.-->
	  <xs:simpleType name="tipoTelefono">
	    <xs:restriction base="xs:string">
	            <xs:pattern value="[0-9]{9}"/>
	    </xs:restriction>
	  </xs:simpleType>
	
	  <xs:simpleType name="listaTelefonos">
	     <xs:list itemType="tipoTelefono"/>
	  </xs:simpleType>
	
	  <xs:simpleType name="telefonos">
	    <xs:restriction base="listaTelefonos">
	        <xs:maxLength value="4"/>
	    </xs:restriction>
	  </xs:simpleType>
	
	</xs:schema>

..

Enunciado3
-----------

Creación de documentos XML e esquemas XML completos. Neste exemplo imos crear esquemas XML que respondan as especificacións que se determinan que deben cumprir os documentos XML que se queren validar, empregando todos os conceptos explicados na UD. Elaboraremos o esquema XML tendo en conta que:

• O grupo de atributos creado para o nome completo e a validación dos nomes e apelidos debe gardarse nun esquema xml aparte e facer referencia a este dende o noso esquema.

• O esquema coas definicións comúns debe estar documentado para indicar as definicións que contén.

• Para os alumnos debemos gardar a súa altura. A altura dun alumno pode tomar os valores

• Alto, Baixo ou un número positivo maior que 20 que gardará a altura en cm.


Solución
----------

.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<instituto xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			 xsi:noNamespaceSchemaLocation="alumno.xsd">
	    <alumno numExpedente="123" nome="Alicia María" apelido1="Casal" apelido2="Ferreiro">
	        <altura>156</altura>
	    </alumno>
	    <alumno numExpedente="155" nome="Paloma" apelido1="Pereiró">
	        <altura>Baixo</altura>
	    </alumno>
	    <profesor NRP="1234A590" nome="Carme" apelido1="Bouza" apelido2="Dominguez"/>
	    <profesor NRP="3332A590" nome="Mariña" apelido1="Cerviño" apelido2="Dominguez"/>
	    <alumno numExpedente="3442" nome="Fernando" apelido1="Puga" apelido2="Prado">
	        <altura>178</altura>
	    </alumno>
	</instituto>

..

.. code-block:: xsd

	<?xml version="1.0" encoding="UTF-8"?>
	<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:include schemaLocation="alumno_2.xsd"/>
	<xs:annotation>
	    <xs:documentation>
	       Definicións comúns para validar o seguinte:
	       * Nomes que so poden ter letras (inluíndo acentos e ñ) e espazos en branco.
	       * A altura, que pode tomar os valores Alto, Baixo ou a altura en cm (valida que non sexa menor que 20)
	    </xs:documentation>
	</xs:annotation>
	
	<!--Para os alumnos debemos gardar a súa altura. A altura dun alumno pode tomar os valores Alto, Baixo 
	ou un número positivo maior que 20 que gardará a altura en cm-->
	<xs:simpleType name="tipoAltura">
	    <xs:union>
	        <xs:simpleType>
		   	    	<xs:restriction base="xs:string">
				        	<xs:enumeration value="Alto"/>
				        	<xs:enumeration value="Baixo"/>
		       		</xs:restriction>
		    	</xs:simpleType>
			    <xs:simpleType>
		   	    	<xs:restriction base="xs:unsignedByte">
					        <xs:minInclusive value="20"/>
		   		    </xs:restriction>
			    </xs:simpleType>
		  </xs:union>
	</xs:simpleType>
	
		<xs:element name="instituto">
			<xs:complexType>
				<xs:choice maxOccurs="unbounded">
					  <xs:element ref="alumno"/>
					  <xs:element ref="profesor"/>
				</xs:choice>
			</xs:complexType>
		</xs:element>
		
		<xs:element name="alumno">
			<xs:complexType>
			   	<xs:sequence>
				      <xs:element name="altura" type="tipoAltura" minOccurs="0"/>
			   	</xs:sequence>
			  	<xs:attribute name="numExpedente" type="tipoNumExpedente"
	          use="required"/>
				  <xs:attributeGroup ref="grupoNome"/>
			</xs:complexType>
		</xs:element>
		
		<xs:element name="profesor">
			<xs:complexType>
				  <xs:attribute name="NRP" type="tipoNRP" use="required"/>
				  <xs:attributeGroup ref="grupoNome"/>
			</xs:complexType>
		</xs:element>
	
	<!-- O número de expedente debe constar de 3 ou 4 díxitos. -->
		<xs:simpleType name="tipoNumExpedente">
			<xs:restriction base="xs:string">
				<xs:pattern value="\d{3,4}"/>
			</xs:restriction>
		</xs:simpleType>
		
		<!--O NRP debe comezar por 3 ou 4 díxitos, seguidos dunha letra entre a A e a E, 
	  e a continuación outros 3 díxitos. -->
		<xs:simpleType name="tipoNRP">
			<xs:restriction base="xs:string">
				<xs:pattern value="\d{3,4}[A-E]\d{3}"/>
			</xs:restriction>
		</xs:simpleType>
	</xs:schema>

..
