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


Patrones XSLT
~~~~~~~~~~~~~

Los patrones indican una transformación que se realizará en ciertos elementos del documento original. La forma más común de indicar los elementos del documento original a los que se aplicará el patrón es mediante el uso de una expresión XPath con el atributo "match". Por ejemplo, si queremos aplicar el patrón al documento XML completo, utilizaremos el valor "/" en el atributo match. De esta manera se selecciona el elemento raíz y se aplica la plantilla a todo el documento XML.

.. code-block:: xml

   <xsl:template match="/">
      …
   </xsl:template>
..

El patrón puede contener texto y etiquetas (por ejemplo, código en formato HTML), que se copiarán en el documento de salida.

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/">
   <HTML>
      <HEAD>
         <TITLE>Documento HTML</TITLE>
      </HEAD>
      <BODY>
         <h2>Colección de música</h2>
         <table border="1">
            <tr bgcolor="#9acd32">
               <th>Título</th>
               <th>Artista</th>
            </tr>
            <tr>
               <td>.</td>
               <td>.</td>
            </tr>
         </table>
      </BODY>
   </HTML>
   </xsl:template>
   </xsl:stylesheet>
..


Resumidamente, la transformación se realiza de la siguiente manera:

#. El documento origen se pasa al procesador XSLT.
#. El procesador carga una hoja de estilos XSLT.
#. Luego, el procesador:

      * Carga los patrones especificados en la hoja de estilo...
      * Recorre el documento XML origen, nodo por nodo...
      * Para cada nodo, busca un patrón que lo referencie en su atributo "match".
      * Una vez encontrado el patrón, aplica la transformación definida en el mismo al nodo del documento origen.
      * Proporciona el resultado en un nuevo documento.

Es muy importante tener en cuenta que cuando el procesador encuentra un patrón que hace referencia al nodo que está procesando, después de aplicar la transformación correspondiente, marca al nodo y a todos sus hijos como procesados, por lo que no buscará otro patrón con el que transformarlos. Por ejemplo:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="ciclo">
       …
   </xsl:template>
   <xsl:template match="módulo">
       …
   </xsl:template>
   <xsl:template match="profesor">
       …
   </xsl:template>
   </xsl:stylesheet>
..

El primer nodo del documento origen que procesa es "<ciclo>", y una vez aplicada la transformación que indica su patrón correspondiente, los nodos "módulo" y "profesor" también quedan marcado como procesados, por lo que el segundo patrón del documento XSLT nunca se ejecutará. Más adelante, se verá cómo se llevan a cabo las transformaciones XSLT con varios patrones.


Patrones XSLT predefinidos
~~~~~~~~~~~~~~~~~~~~~~~~~~

Cuando se emplean patrones fijos, estos se aplican a aquellos elementos que no han sido procesados por ningún otro patrón.
Cuando usamos las expresiones "/" o "/ciclo", estas cubren todos sus hijos y, por lo tanto, todo el documento original. No queda ningún elemento del documento original sin procesar.

Al usar la expresión "/ciclo/módulo" en el patrón (<xsl:template match="/ciclo/módulo">), el resultado obtenido no es el que inicialmente podríamos esperar. Los elementos "<ciclo>" y "<profesor>" no están cubiertos por él; por lo tanto, el procesador XSLT les aplica un patrón predefinido. Básicamente, el comportamiento de estos patrones predefinidos es procesar el elemento y todos sus hijos, copiando al documento de salida el texto que contienen.

En nuestro ejemplo (Exemplo02b.xml y Exemplo02b.xsl):

* Al procesar el elemento "<ciclo>", el procesador XSLT no encuentra un patrón y aplica el patrón predefinido. Esto copia al documento de salida el salto de línea que existe antes del elemento "<módulo>". Por eso aparece una línea vacía al inicio del documento resultante.

* El elemento "<módulo>" está cubierto por el patrón "/ciclo/módulo", y al procesarlo se copian en el documento de salida las etiquetas y el contenido correspondientes al documento HTML.

* Por último, el procesador XSLT llega al elemento "<profesor>", que tampoco tiene un patrón específico, por lo que también copia su contenido (el nombre del profesor) al documento de salida.
