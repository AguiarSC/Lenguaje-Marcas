## Simple XML Schema
~~~~
<?xml version="1.0"?>
<xs:schema xmlns:xsi="http://www.w3.org/2001/XMLSchema" targetNamespace="http://interoperabilnost.hr" xmlns="http://interoperabilnost.hr" elementFormDefault="qualified">
  <xs:element name="note">
    <xs:complexType>
      <xs:sequence>
	<xs:element name="to" type="xs:string"/>
	<xs:element name="from" type="xs:string"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema> 
~~~~

<br />

## Simple Types

  - xs:string
  - xs:decimal
  - xs:integer
  - xs:boolean
  - xs:date
  - xs:time

### Example
~~~~
<xs:element name="start_date" type="xs:date"/>
~~~~

<br />

## XML Facets

Facets are used to define restrictions on simple types. They limit the range of values that an element can have.

  - xs:minInclusive 
  - xs:maxInclusive
  - xs:minExclusive
  - xs:maxExclusive
  - xs:enumeration
  - xs:pattern
  - xs:whiteSpace
  - xs:length
  - xs:minLength
  - xs:maxLength
  - xs:totalDigits
  - xs:fractionDigits

### Min-max

Defines minimum and maximum inclusive values for an element.
~~~~
<xs:element name="age">
  <xs:simpleType>
    <xs:restriction base="xs:integer">
      <xs:minInclusive value="0"/>
      <xs:maxInclusive value="120"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element> 
~~~~

### Enumeration

Restricts an element to a set of predefined values.
~~~~
<xs:element name="car" type="carType"/>

<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>
~~~~

### Pattern

Uses regular expressions to define a pattern for the value of an element.
~~~~
<xs:restriction base="xs:string">
  <xs:pattern value="([a-z])+"/>
</xs:restriction>
~~~~

### WhiteSpace
Controls how whitespace is handled.
- preserve: keep whitespaces
- replace: replace whitespace characters with spaces
- collapse: collapse all whitespace characters to a single space

~~~~
<xs:restriction base="xs:string">
  <xs:whiteSpace value="preserve"/>
</xs:restriction>
~~~~

<br />

## Complex Elements

Complex elements can have multiple elements and/or attributes. They are more versatile than simple elements.

- empty elements
- elements that contain only other elements
- elements that contain only text
- elements that contain both other elements and text

### Complex Example

Defines a complex element `personinfo` which is used by `employee` and `student`. `professor` extends `personinfo` to include additional elements.
~~~~
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
~~~~

### Empty Element

Defines an element with attributes but no child elements.
~~~~
<xs:complexType name="prodtype">
  <xs:attribute name="prodid" type="xs:positiveInteger"/>
</xs:complexType>
~~~~

### Text only + attribute

Defines an element that contains only text and an attribute.
~~~~
<xs:complexType name="shoetype">
  <xs:simpleContent>
    <xs:extension base="xs:integer">
      <xs:attribute name="country" type="xs:string" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
~~~~

### Integer only + Attribute + attribute restriction

Defines an element with integer content and an attribute with restrictions.
~~~~
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
~~~~
<br />

## Element Indicators

Indicators define how elements can appear in the XML document.

- **All**: Elements can appear in any order but only once.
- **Choice**: Only one of the elements can appear.
- **Sequence**: Elements must appear in a specific order.

- **minOccurs**: Minimum number of occurrences.
- **maxOccurs**: Maximum number of occurrences.

<br />

## Data Types

### String

- xs:string

### Date

XML Schema provides a variety of date and time formats.

| Name          | Description   |
| ------------- |-------------:|
| xs:date      | YYYY-MM-DD |
| xs:dateTime     | YYYY-MM-DDThh:mm:ss      |
| xs:duration | PnYnMnDTnHnMnS |
| xs:gDay | DD      |
| xs:gMonth | MM      |
| xs:gMonthDay | MM-DD      |
| xs:gYear | YYYY      |
| xs:gYearMonth | YYYY-MM      |
| xs:time | hh:mm:ss      |

### Numeric

Various numeric data types are available for different ranges and precisions.

- xs:byte
- xs:decimal
- xs:int
- xs:integer
- xs:long
- xs:negativeInteger
- xs:nonNegativeInteger
- xs:nonPositiveInteger
- xs:positiveInteger
- xs:short
- xs:unsignedLong
- xs:unsignedInt
- xs:unsignedShort
- xs:unsignedByte
- xs:float
- xs:double

### Boolean

- xs:boolean
