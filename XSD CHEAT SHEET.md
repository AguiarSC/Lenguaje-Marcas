## XML SCHEMA (XSD)

## Tipos Simples

  - `xs:string`: Representa una cadena de caracteres.
  - `xs:decimal`: Representa un número decimal.
  - `xs:integer`: Representa un número entero.
  - `xs:boolean`: Representa un valor booleano (verdadero o falso).
  - `xs:date`: Representa una fecha en el formato YYYY-MM-DD.
  - `xs:time`: Representa una hora en el formato hh:mm:ss.

### Ejemplo

```xsd
<xs:element name="start_date" type="xs:date"/>
```

<br />

## Facetas XML

Las facetas se utilizan para definir restricciones en los tipos simples. Limitan el rango de valores que un elemento puede tener.

  - `xs:minInclusive`: Valor mínimo inclusivo.
  - `xs:maxInclusive`: Valor máximo inclusivo.
  - `xs:minExclusive`: Valor mínimo exclusivo.
  - `xs:maxExclusive`: Valor máximo exclusivo.
  - `xs:enumeration`: Define un conjunto de valores permitidos.
  - `xs:pattern`: Define un patrón mediante una expresión regular.
  - `xs:whiteSpace`: Controla cómo se manejan los espacios en blanco.
  - `xs:length`: Longitud exacta de una cadena.
  - `xs:minLength`: Longitud mínima de una cadena.
  - `xs:maxLength`: Longitud máxima de una cadena.
  - `xs:totalDigits`: Número total de dígitos permitidos.
  - `xs:fractionDigits`: Número máximo de dígitos fraccionarios permitidos.

### Min-máx

Define valores mínimos y máximos inclusivos para un elemento.

```xsd
<xs:element name="age">
  <xs:simpleType>
    <xs:restriction base="xs:integer">
      <xs:minInclusive value="0"/>
      <xs:maxInclusive value="120"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element> 
```

### Enumeración

Restringe un elemento a un conjunto de valores predefinidos.

```xsd
<xs:element name="car" type="carType"/>

<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>
```

### Patrón

Utiliza expresiones regulares para definir un patrón para el valor de un elemento.

```xsd
<xs:restriction base="xs:string">
  <xs:pattern value="([a-z])+"/>
</xs:restriction>
```

### Espacios en blanco
Controla cómo se manejan los espacios en blanco.
- `preserve`: Mantener los espacios en blanco.
- `replace`: Reemplazar los caracteres de espacio en blanco con espacios.
- `collapse`: Colapsar todos los caracteres de espacio en blanco en un solo espacio.

```xsd
<xs:restriction base="xs:string">
  <xs:whiteSpace value="preserve"/>
</xs:restriction>
```

<br />

## Elementos Complejos

Los elementos complejos pueden tener múltiples elementos y/o atributos. Son más versátiles que los elementos simples.

- `elementos vacíos`: Elementos que no contienen ningún dato.
- `elementos que contienen solo otros elementos`: Elementos que contienen otros elementos, pero no texto.
- `elementos que contienen solo texto`: Elementos que contienen texto, pero no otros elementos.
- `elementos que contienen tanto otros elementos como texto`: Elementos que contienen tanto texto como otros elementos.

### Ejemplo Complejo

Define un elemento complejo `personinfo` que es usado por `employee` y `student`. `professor` extiende `personinfo` para incluir elementos adicionales.

```xsd
<xs:element name="employee" type="personinfo"/>
<xs:element name="student" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>

<xs:element name="professor" type="fullpersoninfo"/>

<xs:complexType name="fullpersoninfo">
  <xs:complexContent>
    <xs:extension base="personinfo">
      <xs:sequence>
        <xs:element name="address" type="xs:string"/>
        <xs:element name="city" type="xs:string"/>
        <xs:element name="country" type="xs:string"/>
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType> 
```

### Elemento Vacío

Define un elemento con atributos pero sin elementos secundarios.

```xsd
<xs:complexType name="prodtype">
  <xs:attribute name="prodid" type="xs:positiveInteger"/>
</xs:complexType>
```

### Solo texto + atributo

Define un elemento que contiene solo texto y un atributo.

```xsd
<xs:complexType name="shoetype">
  <xs:simpleContent>
    <xs:extension base="xs:integer">
      <xs:attribute name="country" type="xs:string" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

### Solo entero + Atributo + restricción de atributo

Define un elemento con contenido entero y un atributo con restricciones.

```xsd
<xs:complexType>
  <xs:simpleContent>
    <xs:extension base="xs:integer">
      <xs:attribute name="unit">
        <xs:simpleType>
          <xs:restriction base="xs:string">
            <xs:length value="3" />
          </xs:restriction>
        </xs:simpleType>
      </xs:attribute>
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

<br />

## Indicadores de Elementos

Los indicadores definen cómo pueden aparecer los elementos en el documento XML.

- `All`: Los elementos pueden aparecer en cualquier orden, pero solo una vez.
- `Choice`: Solo uno de los elementos puede aparecer.
- `Sequence`: Los elementos deben aparecer en un orden específico.

- `minOccurs`: Número mínimo de ocurrencias.
- `maxOccurs`: Número máximo de ocurrencias.

<br />

## Tipos de Datos

### Cadena

- `xs:string`: Representa una cadena de caracteres.

### Fecha

El esquema XML proporciona una variedad de formatos de fecha y hora.

| Nombre          | Descripción   |
| ------------- |-------------:|
| `xs:date`      | YYYY-MM-DD |
| `xs:dateTime`     | YYYY-MM-DDThh:mm:ss      |
| `xs:duration` | PnYnMnDTnHnMnS |
| `xs:gDay` | DD      |
| `xs:gMonth` | MM      |
| `xs:gMonthDay` | MM-DD      |
| `xs:gYear` | YYYY      |
| `xs:gYearMonth` | YYYY-MM      |
| `xs:time` | hh:mm:ss      |

### Numérico

Varios tipos de datos numéricos están disponibles para diferentes rangos y precisiones.

- `xs:byte`: Entero de 8 bits con signo.
- `xs:decimal`: Número decimal.
- `xs:int`: Entero de 32 bits con signo.
- `xs:integer`: Número entero.
- `xs:long`: Entero de 64 bits con signo.
- `xs:negativeInteger`: Entero negativo.
- `xs:nonNegativeInteger`: Entero no negativo.
- `xs:nonPositiveInteger`: Entero no positivo.
- `xs:positiveInteger`: Entero positivo.
- `xs:short`: Entero de 16 bits con signo.
- `xs:unsignedLong`: Entero de 64 bits sin signo.
- `xs:unsignedInt`: Entero de 32 bits sin signo.
- `xs:unsignedShort`: Entero de 16 bits sin signo.
- `xs:unsignedByte`: Entero de 8 bits sin signo.
- `xs:float`: Número de punto flotante de precisión simple.
- `xs:double`: Número de punto flotante de precisión doble.

### Booleano

- `xs:boolean`: Representa un valor booleano (verdadero o falso).
