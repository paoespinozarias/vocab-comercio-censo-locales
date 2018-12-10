## Ejemplos de consultas sobre censo de locales y licencias de apertura

A continuación se presentan algunos ejemplos de consultas, utilizando como referencia un extracto de los conjuntos de datos proporcionados por el Ayuntamiento de Madrid, que se corresponden con los ficheros de censo de locales y sus actividades, terrazas, y licencias otorgadas.

Por ejemplo, en esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fbarrio+%3Frotulo+WHERE%7B%0D%0A++++++++%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+esadm%3Abarrio+%3FuriBarrio+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%22DELICIAS%22+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%3Fbarrio+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+escom%3AtipoSituacion+%3FuriSituacion+.%0D%0A++++++++%0D%0A%7D%0D%0A+LIMIT+10&format=text%2Fhtml&timeout=0&debug=on) se piden 10 locales en situación activa que se encuentren ubicados en el barrio "DELICIAS".  
```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>

SELECT DISTINCT ?barrio ?rotulo WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal esadm:barrio ?uriBarrio .
        ?uriBarrio dc:title "DELICIAS" .
        ?uriBarrio dc:title ?barrio .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal escom:tipoSituacion ?uriSituacion .
        ?uriSituacion skos:prefLabel "activo" .         
}
 LIMIT 10
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Frotulo+%3Fdireccion+%3Fdistrito+%3Fbarrio+WHERE%7B%0D%0A%09%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%22DECORACIONES+EMBAJADORES+157%22+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+schema%3Aaddress+%3Fdireccion+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+esadm%3Abarrio+%3FuriBarrio+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%3Fbarrio+.%0D%0A%0D%0A%7D+limit+10%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen los datos relacionados con un local específico. En este caso el local con rótulo "DECORACIONES EMBAJADORES 157".

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX rdfs:<http://www.w3.org/2000/01/rdf-schema#>
PREFIX schema:<http://schema.org/>
PREFIX geosparql:<http://www.opengis.net/ont/geosparql#>
PREFIX geo_core:<https://datos.ign.es/def/geo_core#>

SELECT DISTINCT ?rotulo ?direccion ?distrito ?barrio ?coordenadaX ?coordenadaY WHERE{
	?uriLocal a escom:LocalComercial .
        ?uriLocal escom:rotulo "DECORACIONES EMBAJADORES 157" .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal schema:address ?direccion .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal esadm:barrio ?uriBarrio .
        ?uriBarrio dc:title ?barrio .
        ?uriLocal geosparql:hasGeometry ?uriPoint .
        ?uriPoint geo_core:xETRS89 ?coordenadaX .
        ?uriPoint geo_core:yETRS89 ?coordenadaY
}

```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+geosparql%3A%3Chttp%3A%2F%2Fwww.opengis.net%2Font%2Fgeosparql%23%3E%0D%0APREFIX+geo_core%3A%3Chttps%3A%2F%2Fdatos.ign.es%2Fdef%2Fgeo_core%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Frotulo+%3Fdireccion+%3Fdistrito+%3Fbarrio+%3FcoordenadaX+%3FcoordenadaY+WHERE%7B%0D%0A%09%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+escom%3AtipoActividadEconomica+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Fcnae%2FCod4%2F9602%3E+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+schema%3Aaddress+%3Fdireccion+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+esadm%3Abarrio+%3FuriBarrio+.%0D%0A++++++++%3FuriBarrio+dc%3Atitle+%3Fbarrio+.%0D%0A++++++++%3FuriLocal+geosparql%3AhasGeometry+%3FuriPoint+.%0D%0A++++++++%3FuriPoint+geo_core%3AxETRS89+%3FcoordenadaX+.%0D%0A++++++++%3FuriPoint+geo_core%3AyETRS89+%3FcoordenadaY+++++++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen todos los locales en los que se realiza la actividad “Peluquería y otros tratamientos de belleza”.

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX schema:<http://schema.org/>
PREFIX geosparql:<http://www.opengis.net/ont/geosparql#>
PREFIX geo_core:<https://datos.ign.es/def/geo_core#>

SELECT DISTINCT ?rotulo ?direccion ?distrito ?barrio ?coordenadaX ?coordenadaY WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal escom:tipoActividadEconomica ?uriActividad .     
        ?uriActividad rdfs:label "Peluquería y otros tratamientos de belleza"@es .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal schema:address ?direccion .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal esadm:barrio ?uriBarrio .
        ?uriBarrio dc:title ?barrio .
        ?uriLocal geosparql:hasGeometry ?uriPoint .
        ?uriPoint geo_core:xETRS89 ?coordenadaX .
        ?uriPoint geo_core:yETRS89 ?coordenadaY .      
}
```
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+escom-skos-situacion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Ftipo-situacion%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fdistrito%3Frotulo+WHERE%7B%0D%0A++++++++%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%22ARGANZUELA%22+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+escom%3AtipoSituacion+escom-skos-situacion%3Aactivo+.%0D%0A++++++++%3FuriLocal+escom%3AtieneTerraza+%3FuriTerraza+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen los rotulos de aquellos locales, ubicados en el distrito "ARGANZUELA", que tienen terrazas autorizadas.

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX escom-skos-situacion:<http://vocab.linkeddata.es/datosabiertos/kos/comercio/tipo-situacion/>

SELECT DISTINCT ?distrito?rotulo WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title "ARGANZUELA" .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal escom:tipoSituacion escom-skos-situacion:activo .
        ?uriLocal escom:tieneTerraza ?uriTerraza .
        ?uriLocal escom:rotulo ?rotulo .
}
```
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fhorario+%3FnumeroSillasAutorizadas+%3FnumeroMesasAutorizadas+%3Fsuperficie+WHERE%7B%0D%0A++++++++%3FuriTerraza+a+escom%3ATerraza+.%0D%0A++++++++%3FuriTerraza+escom%3AperteneceALocal+%3FuriLocal+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%22CAFETERIA+MARKITOS%22+.%0D%0A++++++++%3FuriTerraza+schema%3AopeningHours+%3Fhorario+.%0D%0A++++++++%3FuriTerraza+escom%3AnumeroSillasAutorizadas+%3FnumeroSillasAutorizadas+.%0D%0A++++++++%3FuriTerraza+escom%3AnumeroMesasAutorizadas+%3FnumeroMesasAutorizadas+.%0D%0A++++++++%3FuriTerraza+escom%3Asuperficie+%3Fsuperficie+.+++%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on) se obtiene información del horario de funcionamiento, número de sillas y mesas autorizadas, y la superficie de la terraza que pertenece al local "CAFETERIA MARKITOS".

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX schema:<http://schema.org/>

SELECT DISTINCT ?horario ?numeroSillasAutorizadas ?numeroMesasAutorizadas ?superficie WHERE{
        ?uriTerraza a escom:Terraza .
        ?uriTerraza escom:perteneceALocal ?uriLocal .
        ?uriLocal escom:rotulo "CAFETERIA MARKITOS" .
        ?uriTerraza schema:openingHours ?horario .
        ?uriTerraza escom:numeroSillasAutorizadas ?numeroSillasAutorizadas .
        ?uriTerraza escom:numeroMesasAutorizadas ?numeroMesasAutorizadas .
        ?uriTerraza escom:superficie ?superficie .   
}
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+escom-skos-situacion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Ftipo-situacion%2F%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fdistrito+%3Frotulo+%3Fdireccion+WHERE%7B%0D%0A++++++++%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%22ARGANZUELA%22+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+escom%3AtipoSituacion+escom-skos-situacion%3Acerrado+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+schema%3Aaddress+%3Fdireccion+.%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen los locales en situación cerrado del distrito "ARGANZUELA".
```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX escom-skos-situacion:<http://vocab.linkeddata.es/datosabiertos/kos/comercio/tipo-situacion/>
PREFIX schema:<http://schema.org/>

SELECT DISTINCT ?distrito ?rotulo ?direccion WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title "ARGANZUELA" .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal escom:tipoSituacion escom-skos-situacion:cerrado .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal schema:address ?direccion .
}
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+escom-skos-situacion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Ftipo-situacion%2F%3E%0D%0APREFIX+escom-skos-acceso%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Ftipo-acceso%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fdistrito+%3Frotulo+%3Fdireccion+WHERE%7B%0D%0A++++++++%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+escom%3AtipoSituacion+escom-skos-situacion%3Aactivo+.%0D%0A++++++++%3FuriLocal+escom%3AtipoAcceso+escom-skos-acceso%3Apuerta-calle+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A++++++++%3FuriLocal+schema%3Aaddress+%3Fdireccion+.%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se obtienen los locales en situación activo con tipo de acceso puerta de calle.

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX schema:<http://schema.org/>
PREFIX escom-skos-situacion:<http://vocab.linkeddata.es/datosabiertos/kos/comercio/tipo-situacion/>
PREFIX escom-skos-acceso:<http://vocab.linkeddata.es/datosabiertos/kos/comercio/tipo-acceso/>

SELECT DISTINCT ?distrito ?rotulo ?direccion WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal escom:tipoSituacion escom-skos-situacion:activo .
        ?uriLocal escom:tipoAcceso escom-skos-acceso:puerta-calle .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal escom:rotulo ?rotulo .
        ?uriLocal schema:address ?direccion .
}
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+esadm%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Fterritorio%23%3E%0D%0APREFIX+escom-skos-situacion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Ftipo-situacion%2F%3E%0D%0A+%0D%0ASELECT+DISTINCT+%28count%28%3Frotulo%29+as+%3Ftotal%29+WHERE%7B%0D%0A++++++++%3FuriLocal+a+escom%3ALocalComercial+.%0D%0A++++++++%3FuriLocal+esadm%3Adistrito+%3FuriDistrito+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%22ARGANZUELA%22+.%0D%0A++++++++%3FuriDistrito+dc%3Atitle+%3Fdistrito+.%0D%0A++++++++%3FuriLocal+escom%3AtipoSituacion+escom-skos-situacion%3Aactivo+.%0D%0A++++++++%3FuriLocal+escom%3AtipoActividadEconomica+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fcomercio%2Fcnae%2FCod4%2F5610%3E+.%0D%0A++++++++%3FuriLocal+escom%3AtipoActividadEconomica+%3FuriActividad+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.+++++++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on) se muestra el total de locales activos que tienen la actividad "Restaurantes y puestos de comidas" en el distrito "ARGANZUELA".

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX esadm:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX rdfs:<http://www.w3.org/2000/01/rdf-schema#>
PREFIX escom-skos-situacion:<http://vocab.linkeddata.es/datosabiertos/kos/comercio/tipo-situacion/>

SELECT DISTINCT (count(?rotulo) as ?total) WHERE{
        ?uriLocal a escom:LocalComercial .
        ?uriLocal esadm:distrito ?uriDistrito .
        ?uriDistrito dc:title "ARGANZUELA" .
        ?uriDistrito dc:title ?distrito .
        ?uriLocal escom:tipoSituacion escom-skos-situacion:activo .
        ?uriLocal escom:tipoActividadEconomica ?uriActividad .
        ?uriActividad rdfs:label "Restaurantes y puestos de comidas"@es .
        ?uriLocal escom:rotulo ?rotulo .       
}
```
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fciudadesabiertas.linkeddata.es%2Fcenso-locales&query=PREFIX+escom%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fcomercio%2Ftejido-comercial%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Frotulo+WHERE%7B%0D%0A++++++++%3FuriAgrupacion+a+escom%3AAgrupacionComercial+.%0D%0A%3FuriAgrupacion+schema%3Aname+%22MERCADO+MUNICIPAL+SANTA+MARIA+LA+CABEZA%22+.%0D%0A++++++++%3FuriAgrupacion+escom%3AcontieneLocalComercial+%3FuriLocal+.%0D%0A++++++++%3FuriLocal+escom%3Arotulo+%3Frotulo+.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on) se obtienen los rótulos de los locales comerciales que contiene la agrupación comercial "MERCADO MUNICIPAL SANTA MARIA LA CABEZA".

```
PREFIX escom:<http://vocab.ciudadesabiertas.es/def/comercio/tejido-comercial#>
PREFIX schema:<http://schema.org/>

SELECT DISTINCT ?nombre ?rotulo WHERE{
        ?uriAgrupacion a escom:AgrupacionComercial .
        ?uriAgrupacion schema:name "MERCADO MUNICIPAL SANTA MARIA LA CABEZA" .
        ?uriAgrupacion escom:contieneLocalComercial ?uriLocal .
        ?uriLocal escom:rotulo ?rotulo .
}
```
