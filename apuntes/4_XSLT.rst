¿Qué es XSLT?
----------------------------

Es un lenguaje XML que se utiliza, junto con XPath, para convertir un documento XML en un documento HTML, en un documento de texto o en otro documento XML. Es decir, XSL permite definir la forma en que queremos ver los datos almacenados en un documento XML. En realidad, XSL es un lenguaje que define la transformación entre un documento XML de entrada y otro documento XML de salida.

Para realizar las transformaciones, necesitamos un procesador XSLT. En el proceso de transformación, XSLT utiliza XPath para definir partes del documento fuente que deben coincidir con una o más plantillas predefinidas. Cuando encuentra una coincidencia, XSLT transformará la parte coincidente del documento fuente en el documento resultante.

Estructura del documento XSLT
-----------------------------

Comenzaremos con una transformación sencilla:

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


Además, deberá de indicar la versión, así como una referencia en el documento al espacio de nombres (las qe contienen las instrucciones destinadas al procesador XSLT). Como este tipo de documentos suele contener otras etiquetas no exclusivas del procesador, es aconsejable emplear un prefijo (comúnmente ``xsl``):

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

Los patrones indican una transformación que se realizará en ciertos elementos del documento original. La forma más común de indicar los elementos del documento original a los que se aplicará el patrón es mediante el uso de una expresión XPath con el atributo ``match``. Por ejemplo, si queremos aplicar el patrón al documento XML completo, utilizaremos el valor ``/`` en el atributo ``match``. De esta manera se selecciona el elemento raíz y se aplica la plantilla a todo el documento XML.

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

El primer nodo del documento origen que procesa es ``<ciclo>``, y una vez aplicada la transformación que indica su patrón correspondiente, los nodos ``módulo`` y ``profesor`` también quedan marcado como procesados, por lo que el segundo patrón del documento XSLT nunca se ejecutará. Más adelante, se verá cómo se llevan a cabo las transformaciones XSLT con varios patrones.


Texto
~~~~~

El elemento ``<xsl:text>`` se utiliza para incluir texto en el documento resultante. El resultado es similar a escribir directamente el texto dentro del patrón, pero en este caso tenemos un mayor control sobre los espacios y los saltos de línea. Por ejemplo:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/">
      Documento HTML
   </xsl:template>
   </xsl:stylesheet>
..

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/">
      <xsl:text>Documento HTML</xsl:text>
   </xsl:template>
   </xsl:stylesheet>
..

Estos dos bloques de código se diferencian únicamente en un salto de línea y unos espacios. 
El elemento ``<xsl:text>`` deberá de contener solamente texto, sin otras etiquetas, por lo que el siguiente bloque dará error al procesarlo:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/">
      <xsl:text><HTML></xsl:text>
   </xsl:template>
   </xsl:stylesheet>
..


Elementos
~~~~~~~~~

Dentro de un patrón podemos emplear ``<xsl:element>`` para crear un nuevo elemento en el documento de salida. Es obligatorio indicar el nombre del nuevo elemento mediante el atributo ``name``. Por ejemplo, si quisiéramos obtener un documento de salida con el elemento raíz ``documento`` vacío:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0 xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/">
      <documento />
   </xsl:template>
   </xsl:stylesheet>
..

o también podríamos:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0 xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/">
      <xsl:element name="documento" />
   </xsl:template>
   </xsl:stylesheet>
..

Una buena razón para utilizar ``<xsl:element>`` es que el contenido del atributo "name" puede estar calculado utilizando expresiones XPath (por ejemplo, a partir de texto, variables, valores devueltos por funciones, etc.). En este caso, la expresión debe estar entre llaves.

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <?xml-stylesheet type="text/xsl" href="Generar_elementos.xsl" ?>
   <ciclo>
       <módulo sesións="5" horas="133">Linguaxes de marcas</módulo>
   </ciclo>

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0 xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/ciclo">
      <xsl:element name="{concat(name(), '_DAW')}" />
   </xsl:template>
   </xsl:stylesheet>
..

Cuando creamos un nuevo elemento en el documento de salida utilizando ``<xsl:element>``, también podemos especificar sus atributos. Simplemente tendremos que añadir como hijos de este tantos elementos ``<xsl:attribute>`` como necesitemos, indicando en cada uno de ellos su nombre con el atributo ``name``. Su valor será el texto que contenga.

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:template match="/ciclo">
      <xsl:element name="{concat(name(), '_DAW')}">
         <xsl:attribute name="duración">2000 horas</xsl:attribute>
      </xsl:element>
   </xsl:template>
   </xsl:stylesheet>
..


Valores
~~~~~~~

En algunos casos queremos obtener el valor de un elemento o atributo del documento de origen para utilizarlo como parte del documento de salida.

.. code-block:: xml

   <xsl:value-of select="expression-xpath" />
..

Por ejemplo, partiendo del siguiente XML:

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <?xml-stylesheet type="text/xsl" href="hoja.xsl"?>
   <catalogo>
      <cd>
         <titulo>Thriller</titulo>
         <artista>Michael Jackson</artista>
      </cd>
      <cd>
         <titulo>The Wall</titulo>
         <artista>Pink Floyd</artista>
      </cd>
      <cd>
         <titulo>Abbey Road</titulo>
         <artista>The Beatles</artista>
      </cd>
   </catalogo>   
..

Le aplicamos un documento XSLT:

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
      <xsl:template match="/">
         <html>
            <body>
               <h2>Colección de música</h2>
               <table border="1">
                  <tr bgcolor="#9acd32">
                     <th>Título</th>
                     <th>Artista</th>
                  </tr>
                  <tr>
                     <td>
                        <xsl:value-of select="catalogo/cd/titulo" />
                     </td>
                     <td>
                        <xsl:value-of select="catalogo/cd/artista" />
                     </td>
                  </tr>
               </table>
            </body>
         </html>
      </xsl:template>
   </xsl:stylesheet>   
..

Obtenemos un documento HTML en el que solo se mostrará la primera ocurrencia del ``catálogo/cd/titulo`` y de ``catalogo/cd/artista``.


Conjunto de atributos
~~~~~~~~~~~~~~~~~~~~~

También es posible definir un conjunto de atributos para luego usarlo en uno o varios elementos. El conjunto de atributos se define usando ``<xsl:attribute-set>``. Se debe indicar el nombre del conjunto con el atributo ``name``.

.. code-block:: xml

   <xsl:attribute-set name="atr_módulo">
      <xsl:attribute name="nome">
         <xsl:value-of select="ciclo/módulo" />
      </xsl:attribute>
      <xsl:attribute name="sesións_anuais">
         <xsl:value-of select="ciclo/módulo/@horas * 1.2"/>
      </xsl:attribute>
   </xsl:attribute-set>
..

``¡OJO!`` La definición del conjunto de atributos debe hacerse como hijo directo del elemento raíz ``<xsl:stylesheet>`` fuera de cualquier patrón. 
Para emplear el conjunto de atributos en la definición de un elemento se añade el atributo ``use-attribute-sets``. Por ejemplo:

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
      <xsl:output encoding="UTF-8" indent="yes" method="xml"/>
      <xsl:attribute-set name="atr_módulo">
         <xsl:attribute name="nome">
            <xsl:value-of select="ciclo/módulo" />
         </xsl:attribute>
         <xsl:attribute name="sesións_anuais">
            <xsl:value-of select="ciclo/módulo/@horas * 1.2"/>
         </xsl:attribute>
      </xsl:attribute-set>
      <xsl:template match="/">
         <xsl:element name="módulo" use-attribute-sets="atr_módulo">
         </xsl:element>
      </xsl:template>
   </xsl:stylesheet>
..


Comentarios
~~~~~~~~~~~

Para crear comentarios se utiliza ``<xsl:component>``.


XSLT con diferentes patrones
-----------------------------

Ya hemos visto lo que sucede cuando no existe un patrón para algún elemento del documento XML de origen. Y hasta ahora hemos estado usando documentos XSLT con un único patrón. Veamos qué pasa cuando tenemos un documento XSLT con varios patrones, como el siguiente ejemplo (Variospatrons1.xml y Variospatrons1.xsl).

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:output method="xml" indent="yes" />
   <xsl:template match="/módulo/profesor">
      <Profesor />
   </xsl:template>
   <xsl:template match="/módulo">
      <Módulo />
   </xsl:template>
   </xsl:stylesheet>

Cuando aplicamos la anterior transformación al documento XML:

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8"?>
   <módulo>
   <profesor>Xaime Louzán</profesor>
   </módulo>

Obtenemos como salida.

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
      <Módulo />


¡¡OJO!! El primer patrón no se procesa. ¿Cuál es la explicación de este comportamiento?

La razón es que el procesador XSLT toma los nodos del documento original (el .xml) uno por uno, comenzando con el elemento raíz y buscando algún patrón que se le pueda aplicar. Por tanto, el elemento raíz del documento fuente, "<módulo>", es el primero en procesarse, y con él todos sus hijos. El patrón seleccionado por el procesador XSLT para este elemento es "<xsl:template match="/module">" y, como resultado, "<Module />" se copia en el documento de salida. Una vez que se han procesado el elemento raíz y sus hijos, no hay más nodos para procesar en el documento original, por lo que el patrón "<xsl:template match="/module/teacher"> no se ejecuta.

Veamos otro ejemplo (prioridad.xml y prioridad.xsl):

Considere el siguiente documento XML:

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <?xml-stylesheet type="text/xsl" href="prioridad.xsl"?>
   <catalogo>
      <cd>
         <titulo>Thriller</titulo>
         <artista>Michael Jackson</artista>
      </cd>
      <cd>
         <titulo>The Wall</titulo>
         <artista>Pink Floyd</artista>
      </cd>
      <cd>
         <titulo>Abbey Road</titulo>
         <artista>The Beatles</artista>
      </cd>
   </catalogo>

Le aplicamos el siguiente XSL:

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <xsl:stylesheetversion="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
   <xsl:output method="text" />
   <xsl:template match="cd">
      <xsl:value-of select="titulo"/>
      <xsl:value-of select="artista"/>
   </xsl:template>
   <xsl:template match="titulo">TÍTULO</xsl:template>
   </xsl:stylesheet>

La transformación da como resultado el siguiente documento de texto:

Como podemos ver, el texto TÍTULO no se incluye ya que prevalece la primera plantilla: el elemento cd está más cerca del catálogo (elemento raíz) que del título.


