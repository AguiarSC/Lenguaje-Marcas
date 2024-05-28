Enunciado
-------------

1. Definir una DTD que valide el documento XML que se muestra a continuación.
Construir un documento XML con DTD interna y otro con DTD externa. Comprobar la buena formación y la validez del documento en ambos casos.
Se deben tener en cuenta las siguientes características:

• El número de factura (n_fac), número de cliente (n_cli) y número de pedido (n_ped) son valores únicos, por cada factura, cliente y pedido distintos, y son obligatorios.

• Los números de teléfono (telefono) y fax (fax) de la empresa no tienen porqué aparecer en la factura, pero siempre que lo hagan deberán tener los mismos valores (teléfono 917776688, fax 917776699).

• La forma de pago puede tomar los valores “efectivo”, “tarjeta” y “plazos”.

• La moneda tiene que aparecer siempre, y siempre toma al valor “euro”.

• El iva tiene que aparecer siempre, y su valor no puede contener caracteres especiales.

2. Definir una DTD que valide el documento XML que se muestra a continuación. Construir un documento XML con DTD interna y otro con DTD externa. Comprobar la buena formación y la validez del documento en ambos casos.
Se deben tener en cuenta las siguientes características:

• El título original de una película solo aparecerá cuando la película no sea española.

• Es posible que en un momento dado una película esté pendiente de clasificación. En caso de que esté clasificada siempre deberá indicar los años para los que se recomienda: tp (todos los públicos), 8, 12, 16 o 18.

• No siempre existe una web con la información de la película.

• Se quiere guardar información sobre el fichero gráfico que contiene el cartel de la película. Este fichero no siempre está disponible.

• En caso de que no se proporcione el año de una película se asumirá que es el 2003.

• En el reparto deberá aparecer un actor como mínimo.

