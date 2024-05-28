DTD
---

DTD en el propio documento
==========================

.. code-block:: xml

    <!DOCTYPE nombre [
     ... declaraciones ...
    ]>

DTD en un documento externo para una única aplicación
=====================================================

.. code-block:: xml

    <!DOCTYPE nombre SYSTEM "uri">

Combinar una DTD externa con una DTD interna
============================================

.. code-block:: xml

    <!DOCTYPE nombre SYSTEM "uri" [
     ... declaraciones ...
    ]>

DTD en un documento externo para varias aplicaciones
====================================================

.. code-block:: xml

    <!DOCTYPE nombre PUBLIC "fpi" "uri">

Combinar una DTD externa con una DTD interna
============================================

.. code-block:: xml

    <!DOCTYPE nombre PUBLIC "fpi" "uri" [
     ... declaraciones ...
    ]>

En todos estos casos:
- "nombre" es el nombre del tipo de documento XML, que debe coincidir con el nombre del elemento raíz del documento XML.
- "uri" es el camino (absoluto o relativo) hasta la DTD.
- "fpi" es un identificador público formal (Formal Public Identifier).


Entidades internas
==================

.. code-block:: xml

    <!ENTITY nombreEntidad "valorEntidad">

Entidad externa (archivo de texto)
==================================

.. code-block:: xml

    <!ENTITY nombreEntidad SYSTEM "uri">
    <!ENTITY nombreEntidad PUBLIC "fpi" "uri">

Entidad externa (archivo no de texto)
=====================================

.. code-block:: xml

    <!ENTITY nombreEntidad SYSTEM "uri" NDATA tipo>
    <!ENTITY nombreEntidad PUBLIC "fpi" "uri" NDATA tipo>

Entidades paramétricas
======================

.. code-block:: xml

    <!ENTITY % nombreEntidad "valorEntidad">
    <!ENTITY % nombreEntidad SYSTEM "uri">
    <!ENTITY % nombreEntidad SYSTEM "uri" NDATA tipo>

En todos estos casos:
- "nombreEntidad" es el nombre de la entidad.
- "valorEntidad" es el valor de la entidad.
- "uri" es el camino (absoluto o relativo) hasta un archivo.
- "tipo" es el tipo de archivo (gif, jpg, etc).
- "fpi" es un identificador público formal (Formal Public Identifier).


Declaración de notaciones
==========================

Las notaciones se usan en XML para definir las entidades externas que no va a analizar en procesador XML (aunque sí lo hará la aplicación que trate un documento). Para hacer referencia estas entidades no se utiliza la notación habitual (&nombreEntidad;), sino que se utiliza el nombre de la entidad directamente.


Elementos
=========

.. code-block:: xml

    <!ELEMENT nombreElemento (contenido)>

Contenido
=========

- EMPTY: elemento vacío.
- (#PCDATA): texto
- ANY: cualquier cosa.
- , (coma): elementos en el orden indicado.
- | (o lógico): contiene uno de los dos elementos.
- ?: elemento puede aparecer o no, pero sólo una vez.
- *: elemento puede no aparecer o aparecer una o más veces.
- +: elemento tiene que aparecer una o más veces (no puede no aparecer).
- (): agrupar expresiones.


Atributos
=========

.. code-block:: xml

    <!ATTLIST nombreElemento nombreAtributo tipoAtributo valorInicialAtributo >
    <!ATTLIST nombreElemento nombreAtributo1 tipoAtributo1 valorInicialAtributo1>
    <!ATTLIST nombreElemento nombreAtributo2 tipoAtributo2 valorInicialAtributo2>
    <!ATTLIST nombreElemento
      nombreAtributo1 tipoAtributo1 valorInicialAtributo1
      nombreAtributo2 tipoAtributo2 valorInicialAtributo2
     >

En la que:
- "nombreElemento" es el nombre del elemento para el que se define un atributo.
- "nombreAtributo" es el nombre del atributo.
- "tipoAtributo" es el tipo de datos.
- "valorInicialAtributo" es el valor predeterminado del atributo (aunque también puede indicar otras cosas).

Tipos de atributos
==================

- CDATA: caracteres (sin restricciones).
- NMTOKEN: letras, dígitos, y los caracteres punto ".", guión "-", subrayado "_" y dos puntos ":".
- NMTOKENS: letras, dígitos, y los caracteres punto ".", guión "-", subrayado "_", dos puntos ":" (como el tipo NMTOKEN) y también espacios en blanco.
- valores: valores de una lista. Lista entre paréntesis, con términos separados por una barra vertical "|". términos entre comillas simples o dobles si contienen espacios en blanco.
- ID: valor no se puede repetir en otros elementos o atributos.
- IDREF: valor debe coincidir con el valor del atributo ID de otro elemento.
- IDEREFS: valor es una serie de valores separados por espacios que coinciden con el valor del atributo ID de otros elementos.
- ENTITY: entidad definida en la DTD.
- ENTITIES: alguna de las entidades de una lista de entidades definida en la DTD.
- NOTATION: notación definida en la DTD.

Valores iniciales
=================

- #REQUIRED: el atributo es obligatorio, aunque no se especifica ningún valor predeterminado.
- #IMPLIED: el atributo no es obligatorio y no se especifica ningún valor predeterminado.
- #FIXED valor: el atributo tiene un valor fijo.
- valor: el atributo tiene un valor predeterminado.
