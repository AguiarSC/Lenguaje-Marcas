::

  La biblioteca municipal precisa disponer de información para sus colecciones de libros, así como para la gestión de sus 
  miembros y eventos. Por lo tanto, decidieron generar un documento XML con dicha información, así como documentos de 
  validación. Aunque el técnico informático ha pensado en generarlo dinámicamente a partir de la información almacenada en una 
  base de datos, necesitan preparar un documento XML y un DTD asociado que sirva como plantilla.
  
  Características:

  - Un elemento raíz llamado biblioteca.

  - Todos los atributos del XML serán obligatorios.

  - La biblioteca tiene un número variable de libros, miembros y eventos. Puede no haber ninguno.

  - Cada libro tiene:

    - Atributos, todos obligatorios: id (identificador único para cada libro).

    - Título (titulo), autor (autor), y género (genero). Todos obligatorios.

    - Publicación (publicado), con atributos año y idioma, ambos obligatorios.

    - Disponibilidad (disponibilidad), que puede incluir estado (estado), ubicación (ubicacion, opcional) y fecha de 
      devolución (fecha_devolucion, opcional).

  - Cada miembro tiene:

    - Atributos, todos obligatorios: id (identificador único para cada miembro).

    - Nombre (nombre). Obligatorio.

    - Membresía (membresia), con tipo (tipo) que puede ser Anual o Mensual, fecha de inicio (fecha_inicio) y fecha de fin 
      (fecha_fin), todos obligatorios.

    - Contacto (contacto), que incluye correo (correo) con un atributo tipo que puede ser empresa o personal, y teléfono 
      (telefono). El correo es opcional y puede haber varios, el teléfono es obligatorio y puede haber varios.

    - Libros prestados (libros_prestados), puede no haber.

    - Sexo (sexo), que puede ser masculino o femenino.

  - Cada evento tiene:

    - Atributos, todos obligatorios: id (identificador único para cada evento).

    - Nombre (nombre), fecha (fecha), hora (hora), y ubicación (ubicacion). Todos obligatorios.

    - Participantes (participantes), puede incluir varios miembros.


.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE biblioteca SYSTEM "biblioteca.dtd">
  <biblioteca>
      <libro id="1">
          <titulo>El Quijote</titulo>
          <autor>Miguel de Cervantes</autor>
          <genero>Ficción</genero>
          <publicado año="1605" idioma="Español"/>
          <disponibilidad>
              <estado>Disponible</estado>
              <ubicacion>Sección A - Estante 3</ubicacion>
          </disponibilidad>
      </libro>
      
      <libro id="2">
          <titulo>1984</titulo>
          <autor>George Orwell</autor>
          <genero>Distorpía</genero>
          <publicado año="1949" idioma="Inglés"/>
          <disponibilidad>
              <estado>Prestado</estado>
              <fecha_devolucion>2024-06-15</fecha_devolucion>
          </disponibilidad>
      </libro>
  
      <miembro id="1001">
          <nombre>Juan Pérez</nombre>
          <membresia tipo="Anual">
              <fecha_inicio>2023-01-01</fecha_inicio>
              <fecha_fin>2024-01-01</fecha_fin>
          </membresia>
          <contacto>
              <correo tipo="personal">juan.perez@example.com</correo>
              <telefono>+34 600 123 456</telefono>
          </contacto>
          <libros_prestados>
              <libro id="2" fecha_prestamo="2024-05-01"/>
          </libros_prestados>
          <sexo>masculino</sexo>
      </miembro>
  
      <miembro id="1002">
          <nombre>Maria García</nombre>
          <membresia tipo="Mensual">
              <fecha_inicio>2024-05-01</fecha_inicio>
              <fecha_fin>2024-05-31</fecha_fin>
          </membresia>
          <contacto>
              <correo tipo="empresa">maria.garcia@example.com</correo>
              <telefono>+34 600 654 321</telefono>
          </contacto>
          <libros_prestados/>
          <sexo>femenino</sexo>
      </miembro>
      
      <evento id="E001">
          <nombre>Reunión del Club de Lectura</nombre>
          <fecha>2024-06-20</fecha>
          <hora>18:00</hora>
          <ubicacion>Sala de Conferencias</ubicacion>
          <participantes>
              <miembro id="1001"/>
              <miembro id="1002"/>
          </participantes>
      </evento>
      
      <evento id="E002">
          <nombre>Charla del Autor: Isabel Allende</nombre>
          <fecha>2024-07-05</fecha>
          <hora>19:00</hora>
          <ubicacion>Sala Principal</ubicacion>
          <participantes>
              <miembro id="1001"/>
          </participantes>
      </evento>
  </biblioteca>

..


.. code-block:: dtd

  <!ELEMENT biblioteca (libro*, miembro*, evento*)>
  
  <!ELEMENT libro (titulo, autor, genero, publicado, disponibilidad)>
  <!ATTLIST libro
      id ID #REQUIRED>
  <!ELEMENT titulo (#PCDATA)>
  <!ELEMENT autor (#PCDATA)>
  <!ELEMENT genero (#PCDATA)>
  <!ELEMENT publicado EMPTY>
  <!ATTLIST publicado
      año CDATA #REQUIRED
      idioma CDATA #REQUIRED>
  <!ELEMENT disponibilidad (estado, ubicacion?, fecha_devolucion?)>
  <!ELEMENT estado (#PCDATA)>
  <!ELEMENT ubicacion (#PCDATA)>
  <!ELEMENT fecha_devolucion (#PCDATA)>
  
  <!ELEMENT miembro (nombre, membresia, contacto, libros_prestados, sexo)>
  <!ATTLIST miembro
      id ID #REQUIRED>
  <!ELEMENT nombre (#PCDATA)>
  <!ELEMENT membresia (fecha_inicio, fecha_fin)>
  <!ATTLIST membresia
      tipo (Anual | Mensual) #REQUIRED>
  <!ELEMENT fecha_inicio (#PCDATA)>
  <!ELEMENT fecha_fin (#PCDATA)>
  <!ELEMENT contacto (correo, telefono)>
  <!ELEMENT correo (#PCDATA)>
  <!ATTLIST correo
      tipo (personal | empresa) #IMPLIED>
  <!ELEMENT telefono (#PCDATA)>
  <!ELEMENT libros_prestados (libro*)>
  <!ELEMENT libro EMPTY>
  <!ATTLIST libro
      id IDREF #REQUIRED
      fecha_prestamo CDATA #IMPLIED>
  <!ELEMENT sexo (#PCDATA)>
  <!ATTLIST sexo
      sex (masculino | femenino) #REQUIRED>
  
  <!ELEMENT evento (nombre, fecha, hora, ubicacion, participantes)>
  <!ATTLIST evento
      id ID #REQUIRED>
  <!ELEMENT nombre (#PCDATA)>
  <!ELEMENT fecha (#PCDATA)>
  <!ELEMENT hora (#PCDATA)>
  <!ELEMENT ubicacion (#PCDATA)>
  <!ELEMENT participantes (miembro*)>
  <!ELEMENT miembro EMPTY>
  <!ATTLIST miembro
      id IDREF #REQUIRED>

.. 
