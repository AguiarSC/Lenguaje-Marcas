¿Qué es XSLT?
----------------------------

Es un lenguaje XML que se utiliza, junto con XPath, para convertir un documento XML en un documento HTML, en un documento de texto o en otro documento XML. Es decir, XSL permite definir la forma en que queremos ver los datos almacenados en un documento XML. En realidad, XSL es un lenguaje que define la transformación entre un documento XML de entrada y otro documento XML de salida.

Para realizar las transformaciones, necesitamos un procesador XSLT. En el proceso de transformación, XSLT utiliza XPath para definir partes del documento fuente que deben coincidir con una o más plantillas predefinidas. Cuando encuentra una coincidencia, XSLT transformará la parte coincidente del documento fuente en el documento resultante.

Estructura del documento XSLT
-----------------------------

Comenzaremos con una transformación sencilla de Ejemplo.xml:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <ciclo>
      <módulo sesións="5" horas="133">Linguaxes de marcas</módulo>
      <profesor>Xaime Louzán</profesor>
   </ciclo>
..


La transformación a realizar se almacenará en un documento XSLT (.xsl) y se deberá vincular con el XML. En el XML original se debe de añadir la siguiente declaración: 

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <?xml-stylesheet type="text/xsl" href="Ejemplo.xsl"?>
   <ciclo>
      <módulo sesións="5" horas="133">Linguaxes de marcas</módulo>
      <profesor>Xaime Louzán</profesor>
   </ciclo>
..


Respecto al documento XSLT, tiene una estructura específica y deberá de comenzar con un prólogo XML:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
..


El elemento raíz del XSLT puede ser cualquiera de estas dos etiquetas, puesto que son sinónimas:

.. code-block:: xml

   <stylesheet>
   <transform>
..


Además, deberá de indicar la versión, así como una referencia en el documento al espacio de nombres (las qe contienen las instrucciones destinadas al procesador XSLT). Como este tipo de documentos suele contener otras etiquetas no exclusivas del procesador, es aconsejable emplear un prefijo (comúnmente xsl):

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
      ........................
   </xsl:stylesheet>
..


Así las cosas, el documento XSLT de la transformación del XML anterior sería:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <!-- Exemplo01.xsl -->
   <xsl:template match="/">
   <HTML>
      <HEAD>
         <TITLE>Ciclo</TITLE>
      </HEAD>
      <BODY>
         <H1><xsl:value-of select="//módulo"/></H1>
         <H2>- <xsl:value-of select="//profesor"/></H2>
         <P><xsl:value-of select="//módulo/@horas"/> horas
            (<xsl:value-of select="//módulo/@sesións"/> sesións semanais.)</P>
      </BODY>
   </HTML>
   </xsl:template>
   </xsl:stylesheet>
..



Formatos de salida
~~~~~~~~~~~~~~~~~~

Con la siguiente etiqueta, definimos las características de salida del documento. Solo presenta un atributo no opcional (method) que indica el formato del documento resultante. Si no se incluye, el formato de salida por defecto es XML (salvo que el elemento raíz del documento resultante sea HTML, caso en el que sería HTML).

.. code-block:: xml

   <xsl:output>
..


Elaboración de transformaciones XSLT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Se realiza una relación jerárquica (nodos de un árbol).
* Serie de reglas que determinan la transformación. Cada regla contiene uno o varios elementos del XML.
* Estas reglas, sintácticamente, tienen tres partes:
   
   # Etiqueta de apertura que contiene un atributo "match" que describe a qué partes del documento afecta la regla. Su sintaxis debe seguir las especificaciones de XPath. Y debe tener el atributo "name" para definir el nombre de la plantilla.
   
   # Parte central que describe qué debe hacerse en caso de coincidencia.
   
   # Etiqueta de cierre.

.. code-block:: xml

   <xsl:template match="expression-xpath" name="nombre">
      <!-- ... -->
   </xsl:template>
..


