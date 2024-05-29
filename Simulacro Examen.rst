ENUNCIADO EXAMEN
----------------

XML Y DTD
=========

La Biblioteca Nacional necesita gestionar la información sobre sus libros y préstamos. Para ello, han decidido crear un documento XML con la información relevante, así como un documento de validación DTD. Aunque el técnico informático ha considerado generarlo dinámicamente a partir de una base de datos, se requiere preparar un documento XML y un DTD asociado que sirva como plantilla.

Características:
- Un elemento raíz llamado biblioteca.
- Todos los atributos del XML serán obligatorios.
- La biblioteca tiene un número variable de libros y préstamos. Puede no haber ninguno.
- Cada libro tiene:
  - Atributos obligatorios: código de libro (codigoLibro), formado por la letra L seguida de cinco números, por ejemplo, L12345; título (titulo); autor (autor); género (genero) con los valores: "Ficción", "No Ficción", "Ciencia", "Historia".
- Cada préstamo tiene:
  - Atributos obligatorios: código del libro (codigoLibro), que debe coincidir con un libro existente; fecha de inicio (fechaInicio) y fecha de fin (fechaFin) con atributos día (dia), mes (mes) y año (año), obligatorios. El atributo mes sólo puede tomar los valores de los nombres de los meses del año.
  - Observaciones (observaciones), un texto opcional, sólo puede haber uno.

Ejercicio:

a) Modifica el documento XML, biblioteca.xml, para que se ajuste a las características anteriores. (0,25 puntos)
b) Realiza un documento DTD, biblioteca.dtd, que valide el XML creado. (2,5 puntos)

XML sin modificar:

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8" standalone="no"?>

    <!-- Nombre completo del alumno o alumna -->

    <biblioteca>
        <libro codigoLibro="L12345" titulo="El Quijote" autor="Miguel de Cervantes" genero="Ficción">
        </libro>
        <libro codigoLibro="L54321" titulo="1984" autor="George Orwell" genero="Ficción">
        </libro>
        <prestamo codigoLibro="L12345">
            <fechaInicio año="2023" mes="Enero" dia="10"></fechaInicio>
            <fechaFin año="2023" mes="Febrero" dia="10"></fechaFin>
            <observaciones>Devolución retrasada</observaciones>
        </prestamo>
    </biblioteca>

XML SCHEMA
==========

Elige una de las dos opciones:

Opción a (biblioteca_2a.xml y biblioteca_2a.xsd): (3,5 puntos)
---------------------------------------------------------------

Modifica el documento XML Schema que valide el documento XML generado en el ejercicio 1:
- Define un tipo de dato, llamado "tipoFecha" para reutilizar y emplear en el elemento fechaInicio y fechaFin. (0,8 puntos)
- Define un tipo de dato simple, llamado "tipoCodigoLibro" para reutilizar en los atributos codigoLibro y definir el patrón. (0,7 puntos)
- Define ATRIBUTO "genero" para restringir los valores "Ficción", "No Ficción", "Ciencia" y "Historia". (0,6 puntos)
- Define las referencias entre las claves. (0,8 puntos)

Opción b (biblioteca_2b.xml y biblioteca_2b.xsd): (5,25 puntos)
----------------------------------------------------------------

Genera un nuevo documento XML a partir del creado en el ejercicio 1, teniendo en cuenta que:
- Existe un nuevo elemento, socio, que aparece dentro de préstamo. (0,25 puntos)
- El socio es un elemento que contiene solo texto con el código de socio. El código de socio es de la forma S123456, es decir, una letra "S" seguida de 6 números. (0,5 puntos)
- Ahora, el préstamo puede tener, o el elemento socio o las observaciones, pero no ambos a la vez. (1 punto)

Modifica el documento XML Schema que valide el documento XML creado en esta opción:
- Define un tipo de dato, llamado "tipoFecha" para reutilizar y emplear en el elemento fechaInicio y fechaFin. (0,8 puntos)
- Define un tipo de dato simple, llamado "tipoCodigoLibro" para reutilizar en los atributos codigoLibro y definir el patrón. (0,7 puntos)
- Define ATRIBUTO "genero" para restringir los valores "Ficción", "No Ficción", "Ciencia" y "Historia". (0,6 puntos)
- Define las referencias entre las claves. (0,8 puntos)

XML Schema (esqueleto):

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8"?>

    <!-- Nombre completo del alumno o alumna -->

    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

        <!-- TIPO DE DATO complejo para guardar fechas:  tipoFecha -->
        <!-- Define un tipo de dato, llamado "tipoFecha" para reutilizar 
        y emplear en el elemento fechaInicio y fechaFin -->
        
        <!-- TIPO DE DATO simple para identificador libro:  tipoCodigoLibro -->
        <!-- Define un tipo de dato simple, llamado "tipoCodigoLibro" para reutilizar 
        en los atributos codigoLibro y definir el patrón.-->
        
        <!-- Define ATRIBUTO "genero" para restringir valores 
        "Ficción", "No Ficción", "Ciencia" y "Historia"  -->
        
        <!-- ELEMENTOS PRINCIPALES -->
        
        <!-- biblioteca -->
        <xs:element name="biblioteca">
            <xs:complexType>
                <xs:sequence>
                    <xs:element ref="libro" minOccurs="0" maxOccurs="unbounded"/>
                    <xs:element ref="prestamo" minOccurs="0" maxOccurs="unbounded"/>
                </xs:sequence>
            </xs:complexType>
        </xs:element>
        
        <!-- libro -->
        <xs:element name="libro">
            <xs:complexType>
                <xs:attribute name="codigoLibro" type="tipoCodigoLibro" use="required"/>
                <xs:attribute name="titulo" type="xs:string" use="required"/>
                <xs:attribute name="autor" type="xs:string" use="required"/>
                <xs:attribute name="genero" type="xs:string" use="required"/>
            </xs:complexType>
        </xs:element>
            
        <!-- prestamo -->
        <xs:element name="prestamo">
            <xs:complexType>
                <xs:sequence>
                    <xs:element name="fechaInicio" type="tipoFecha"/>
                    <xs:element name="fechaFin" type="tipoFecha"/>
                    <xs:element name="observaciones" type="xs:string" minOccurs="0"/>
                </xs:sequence>
                <xs:attribute name="codigoLibro" type="tipoCodigoLibro" use="required"/>
            </xs:complexType>
        </xs:element>

    </xs:schema>



SOLUCIÓN EXAMEN
---------------
