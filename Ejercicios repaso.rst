Ejercicio 1
-----------

Definir una DTD que valide el documento XML que se muestra a continuación.
Construir un documento XML con DTD interna y otro con DTD externa. Comprobar la buena formación y la validez del documento en ambos casos.
Se deben tener en cuenta las siguientes características:

• El número de factura (n_fac), número de cliente (n_cli) y número de pedido (n_ped) son valores únicos, por cada factura, cliente y pedido distintos, y son obligatorios.

• Los números de teléfono (telefono) y fax (fax) de la empresa no tienen porqué aparecer en la factura, pero siempre que lo hagan deberán tener los mismos valores (teléfono 917776688, fax 917776699).

• La forma de pago puede tomar los valores “efectivo”, “tarjeta” y “plazos”.

• La moneda tiene que aparecer siempre, y siempre toma al valor “euro”.

• El iva tiene que aparecer siempre, y su valor no puede contener caracteres especiales.


.. code-block:: xml
	
	<?xml version="1.1" encoding="UTF-8"?>
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
	    <nombre>Darío, Bueno Gutiérrez</nombre>
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

	<?xml version="1.1" encoding="UTF-8"?>
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
	    <nombre>Darío, Bueno Gutiérrez</nombre> 
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

 <!-- Definición de atributos -->
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

Definir una DTD que valide el documento XML que se muestra a continuación. Construir un documento XML con DTD interna y otro con DTD externa. Comprobar la buena formación y la validez del documento en ambos casos.
Se deben tener en cuenta las siguientes características:

• El título original de una película solo aparecerá cuando la película no sea española.

• Es posible que en un momento dado una película esté pendiente de clasificación. En caso de que esté clasificada siempre deberá indicar los años para los que se recomienda: tp (todos los públicos), 8, 12, 16 o 18.

• No siempre existe una web con la información de la película.

• Se quiere guardar información sobre el fichero gráfico que contiene el cartel de la película. Este fichero no siempre está disponible.

• En caso de que no se proporcione el año de una película se asumirá que es el 2003.

• En el reparto deberá aparecer un actor como mínimo.


.. code-block:: xml

	<cartelera>
	  <película código="p1" duración="152" año="2002">
	    <título>AQUELLAS JUERGAS UNIVERSITARIAS</título>
	    <título_original>Old School</título_original>
	    <nacionalidad>Estados Unidos</nacionalidad>
	    <género>Comedia</género>
	    <clasificación edad="tp"/>
	    <sinopsis>
	      Mitch, Frank y Beanie son tres amigos treintañeros cuyas vidas no son
	      exactamente lo que esperaban. Mitch tiene una novia un poco alocada.
	      Frank se ha casado y su matrimonio nada tiene que ver con las juergas
	      salvajes que organizaban años atrás. Y Beanie es un padre de familia que
	      se muere por recuperar su alocada juventud. Pero las cosas cambian
	      cuando Beanie sugiere que creen su propia fraternidad, en la nueva casa
	      que Mitch tiene junto al campus de la universidad. Una ocasión para
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
	  </película>
	  <película código="p17" duración="06">
	    <título>EL ORO DE MOSCÚ</título>
	    <nacionalidad>España</nacionalidad>
	    <género>Comedia</género>
	    <sin_clasificar/>
	    <sinopsis>
	      Por una extraña coincidencia del destino, alguien recibe una
	      información extraconfidencial de un anciano en sus últimos
	      segundos de vida: el secreto mejor guardado de la historia. El
	      receptor, un trabajador de hospital, se lo comunica secretamente
	      a un supuesto amigo. Ambos inician una aventura rocambolesca y
	      llena de misterio. Ante la inutilidad de sus intentos y muy a
	      su pesar, tienen que recurrir a otras personas que así mismo van
	      cayendo en el pozo sin fondo que conlleva descifrar el enigma.
	    </sinopsis>
	    <director>Jesús Bonilla</director>
	    <reparto>
	      <actor>Jesús Bonilla</actor>
	      <actor>Santiago Segura</actor>
	      <actor>Alfredo Landa</actor>
	      <actor>Concha Velasco</actor>
	      <actor>Antonio Resines</actor>
	      <actor>Gabino Diego</actor>
	      <actor>María Barranco</actor>
	    </reparto>
	  </película>
	</cartelera>

..

Solución 
--------

.. code-block:: xml

	<?xml version="1.1" encoding="UTF-8"?>
	<!DOCTYPE cartelera SYSTEM "Cartelera.dtd">
	<cartelera>
		<película código="p1" duración="152" año="2002">
			<título>AQUELLAS JUERGAS UNIVERSITARIAS</título>
			<título_original>Old School</título_original>
			<nacionalidad>Estados Unidos</nacionalidad>
			<género>Comedia</género>
			<clasificación edad="tp"/>
			<sinopsis>
				Mitch, Frank y Beanie son tres amigos treintañeros cuyas vidas no son exactamente lo que esperaban. Mitch tiene una novia ninfómana que se 				mete en la cama con el primero que agarra. Frank se ha casado y su 				matrimonio nada tiene que ver con las juergas salvajes que organizaban 			años atrás. Y Beanie es un padre de familia que se muere por recuperar 				su alocada juventud. Pero las cosas cambian cuando Beanie sugiere que 				creen su propia fraternidad, en la nueva casa que Mitch tiene junto al 				campus de la universidad. Una ocasión para revivir tiempos gloriosos, 				hacer nuevos amigos y de volver a sus viejas, salvajes y desmadradas 				juergas de estudiantes.
			</sinopsis>
			<director>Todd Philips</director>
			<reparto>
				<actor>Luke Wilson</actor>
				<actor>Will Farrel</actor>
				<actor>Vince Vaughn</actor>
			</reparto>
			<web>http://www.uip.es</web>
			<cartel>caratulas/Aquellas juergas.jpg</cartel>
		</película>
		<película código="p17" duración="06">
			<título>EL ORO DE MOSCÚ</título>
			<nacionalidad>España</nacionalidad>
			<género>Comedia</género>
			<sin_clasificar/>
			<sinopsis>
	Por una extraña coincidencia del destino, alguien recibe una información extraconfidencial de un anciano en sus últimos segundos de vida: el secreto mejor guardado de la Historia. El receptor, un trabajador de hospital, se lo comunica secretamente a un supuesto amigo. Ambos inician una aventura rocambolesca y llena de misterio. Ante la inutilidad de sus intentos y muy a
	su pesar, tienen que recurrir a otras personas que así mismo van cayendo en el pozo sin fondo que conlleva descifrar el enigma.
			</sinopsis>
			<director>Jesús Bonilla</director>
			<reparto>
				<actor>Jesús Bonilla</actor>
				<actor>Santiago Segura</actor>
				<actor>Alfredo Landa</actor>
				<actor>Concha Velasco</actor>
				<actor>Antonio Resines</actor>
				<actor>Gabino Diego, María Barranco</actor>
				<actor>María Barranco</actor>
			</reparto>
		</película>
	</cartelera>

..

.. code-block:: dtd

	<!-- DEFINICIÓN DE ELEMENTOS -->
	 <!ELEMENT cartelera (película)*>
	 <!ELEMENT película (título, título_original?, nacionalidad, género, (clasificación | sin_clasificar), sinopsis, director, reparto, web?, cartel?) >
	 <!ELEMENT título (#PCDATA)>
	 <!ELEMENT título_original (#PCDATA)>
	 <!ELEMENT nacionalidad (#PCDATA)>
	 <!ELEMENT género (#PCDATA)>
	 <!ELEMENT clasificación EMPTY>
	 <!ELEMENT sin_clasificar EMPTY>
	 <!ELEMENT sinopsis (#PCDATA)>
	 <!ELEMENT director (#PCDATA)>
	 <!ELEMENT reparto (actor)+>
	 <!ELEMENT web (#PCDATA)>
	 <!ELEMENT cartel (#PCDATA)>
	 <!ELEMENT actor (#PCDATA)>
	
	 <!-- Definición de atributos -->
	 <!ATTLIST película código ID #REQUIRED>
	 <!ATTLIST película duración CDATA "">
	 <!ATTLIST película año CDATA "2003">
	 <!ATTLIST clasificación edad (8 | 12 | 16 | 18 | tp) #REQUIRED>

..
