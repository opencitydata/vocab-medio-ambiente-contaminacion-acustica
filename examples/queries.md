## Ejemplos de consultas sobre contaminación acústica

A continuación se presentan algunos ejemplos de consultas utilizando como referencia un extracto de los  conjuntos de datos de contaminación acústica publicados por el ayuntamiento de Madrid como datos abiertos.

Por ejemplo, en esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0APREFIX+sosa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%0D%0APREFIX+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+%3Fname+%3Fresult%0D%0AWHERE+%7B%0D%0A++%3Fs+a+noise%3AObservacion+%3B%0D%0A++++noise%3AtipoMedida+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-medicion%2FLAS99%3E+%3B%0D%0A++++noise%3AtipoIntervaloReferencia+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-intervalo-referencia%2FD%3E+%3B%0D%0A++++sosa%3AmadeBySensor+%3Fsensor+%3B%0D%0A++++sosa%3AhasSimpleResult+%3Fresult+%3B%0D%0A++++sosa%3AresultTime+%222019-12-21T00%3A00%3A00%22%5E%5Exsd%3AdateTime+.%0D%0A++%3Fsensor+dct%3Aidentifier+%223%22%5E%5Exsd%3Astring+%3B%0D%0A++++schema%3Aname+%3Fname%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pide el nivel de presión sonora con ponderación frecuencial A y ponderación temporal Slow, que se sobrepasa durante el 99% del tiempo de observación el 21 de diciembre de 2019 entre las 7 y las 19 para la estación de medida número 3.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>
PREFIX sosa: <http://www.w3.org/ns/sosa/>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX schema: <http://schema.org/>

SELECT ?name ?result
WHERE {
  ?s a noise:Observacion ;
    noise:tipoMedida <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-medicion/LAS99> ;
    noise:tipoIntervaloReferencia <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-intervalo-referencia/D> ;
    sosa:madeBySensor ?sensor ;
    sosa:hasSimpleResult ?result ;
    sosa:resultTime "2019-12-21T00:00:00"^^xsd:dateTime .
  ?sensor dct:identifier "3"^^xsd:string ;
    schema:name ?name
}
```

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0APREFIX+sosa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fname+%3Ftime+%3Fresult%0D%0AWHERE+%7B%0D%0A++%3Fs+a+noise%3AObservacion+%3B%0D%0A++++noise%3AtipoMedida+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-medicion%2FLAeq24%3E+%3B%0D%0A++++sosa%3AresultTime+%3Ftime+%3B%0D%0A++++sosa%3AhasSimpleResult+%3Fresult+%3B%0D%0A++++sosa%3AmadeBySensor+%3Fsensor+.%0D%0A++%3Fsensor+schema%3Aname+%3Fname%0D%0A%7D%0D%0AORDER+BY+DESC+%28%3Fs%29+%0D%0ALIMIT+1&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene la estación tuvo el mayor índice de nivel sonoro medio a largo plazo ponderado A, determinado a lo largo de todos los períodos diarios (24 horas) del mes de enero de 2020.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>
PREFIX sosa: <http://www.w3.org/ns/sosa/>
PREFIX schema: <http://schema.org/>

SELECT DISTINCT ?name ?time ?result
WHERE {
  ?s a noise:Observacion ;
    noise:tipoMedida <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-medicion/LAeq24> ;
    sosa:resultTime ?time ;
    sosa:hasSimpleResult ?result ;
    sosa:madeBySensor ?sensor .
  ?sensor schema:name ?name
}
ORDER BY DESC (?s) 
LIMIT 1
```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0APREFIX+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+sf%3A+%3Chttp%3A%2F%2Fwww.opengis.net%2Fdoc%2FIS%2Fgeosparql%2F1.0%23%3E%0D%0APREFIX+geo_core%3A+%3Chttps%3A%2F%2Fdatos.ign.es%2Fdef%2Fgeo_core%23%3E%0D%0A%0D%0ASELECT+%3Fname+%3Flong+%3Flat+%3FxERTS+%3FyERTS%0D%0AWHERE+%7B%0D%0A++%3Fs+a+noise%3AEstacionMedida+%3B%0D%0A+++++dct%3Aidentifier+%221%22%5E%5Exsd%3Astring+%3B%0D%0A+++++schema%3Aname+%3Fname+%3B%0D%0A+++++sf%3AhasGeometry+%3Fpoint+.%0D%0A++%3Fpoint+geo%3Along+%3Flong+%3B%0D%0A++++geo%3Alat+%3Flat+%3B%0D%0A++++geo_core%3AxERTS89+%3FxERTS+%3B%0D%0A++++geo_core%3AyERTS89+%3FyERTS+.%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene las coordenadas de la estación de medición acústica número 1.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX schema: <http://schema.org/>
PREFIX sf: <http://www.opengis.net/doc/IS/geosparql/1.0#>
PREFIX geo_core: <https://datos.ign.es/def/geo_core#>

SELECT ?name ?long ?lat ?xERTS ?yERTS
WHERE {
  ?s a noise:EstacionMedida ;
     dct:identifier "1"^^xsd:string ;
     schema:name ?name ;
     sf:hasGeometry ?point .
  ?point geo:long ?long ;
    geo:lat ?lat ;
    geo_core:xERTS89 ?xERTS ;
    geo_core:yERTS89 ?yERTS .
}
```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0A%0D%0ASELECT+%3Fs%0D%0AWHERE+%7B%0D%0A++%3Fs+a+noise%3AObservacion+.%0D%0A++%3Fs+noise%3AtipoEmisorPredominante+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-emisor-predominante%2Fferrocarriles%3E+.%0D%0A++%3Fs+noise%3AtipoIntervaloReferencia+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-intervalo-referencia%2FD%3E+.%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene el listado de todas las observaciones producidas por ferrocarriles como emisor predominante entre las 7 y las 19 horas.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>

SELECT ?s
WHERE {
  ?s a noise:Observacion .
  ?s noise:tipoEmisorPredominante <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-emisor-predominante/ferrocarriles> .
  ?s noise:tipoIntervaloReferencia <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-intervalo-referencia/D> .
}
```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0APREFIX+sosa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%0D%0A%0D%0ASELECT+%3Fs+%3Fresult+%3Ffechaobs%0D%0AWHERE+%7B%0D%0A++%7B+%3Fs+a+noise%3AObservacion+%3B%0D%0A+++noise%3AtipoIntervaloReferencia+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-intervalo-referencia%2FD%3E+%3B%0D%0A+++sosa%3AhasSimpleResult+%3Fresult+%3B%0D%0A+++sosa%3AresultTime+%3Ffechaobs+.%0D%0A+++FILTER+%28+STRDT+%28+%3Ffechaobs%2C+xsd%3AdateTime+%29+%3E+%222020-07-01T00%3A00%3A00%22%5E%5Exsd%3AdateTime+%29%0D%0A+++FILTER+%28+STRDT+%28+%3Ffechaobs%2C+xsd%3AdateTime+%29+%3C+%222020-07-31T00%3A00%3A00%22%5E%5Exsd%3AdateTime+%29%0D%0A++%7D%0D%0A+UNION+%7B%0D%0A++%3Fs+a+noise%3AObservacion+%3B%0D%0A+++noise%3AtipoIntervaloReferencia+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fmedio-ambiente%2Fcontaminacion-acustica%2Ftipo-intervalo-referencia%2FE%3E+%3B%0D%0A+++sosa%3AhasSimpleResult+%3Fresult+%3B%0D%0A+++sosa%3AresultTime+%3Ffechaobs+.%0D%0A+++FILTER+%28+STRDT+%28+%3Ffechaobs%2C+xsd%3AdateTime+%29+%3E+%222020-07-01T00%3A00%3A00%22%5E%5Exsd%3AdateTime+%29%0D%0A+++FILTER+%28+STRDT+%28+%3Ffechaobs%2C+xsd%3AdateTime+%29+%3C+%222020-07-31T00%3A00%3A00%22%5E%5Exsd%3AdateTime+%29%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene el listado del índice sonoro medio a largo plazo ponderado A, durante los periodos de tarde (de 19 a 23 horas) y durante los periodos día (de 7 a 19 horas) durante el mes de julio de 2020.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>
PREFIX sosa: <http://www.w3.org/ns/sosa/>

SELECT ?s ?result ?fechaobs
WHERE {
  { ?s a noise:Observacion ;
   noise:tipoIntervaloReferencia <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-intervalo-referencia/D> ;
   sosa:hasSimpleResult ?result ;
   sosa:resultTime ?fechaobs .
   FILTER ( STRDT ( ?fechaobs, xsd:dateTime ) > "2020-07-01T00:00:00"^^xsd:dateTime )
   FILTER ( STRDT ( ?fechaobs, xsd:dateTime ) < "2020-07-31T00:00:00"^^xsd:dateTime )
  }
 UNION {
  ?s a noise:Observacion ;
   noise:tipoIntervaloReferencia <http://vocab.linkeddata.es/datosabiertos/kos/medio-ambiente/contaminacion-acustica/tipo-intervalo-referencia/E> ;
   sosa:hasSimpleResult ?result ;
   sosa:resultTime ?fechaobs .
   FILTER ( STRDT ( ?fechaobs, xsd:dateTime ) > "2020-07-01T00:00:00"^^xsd:dateTime )
   FILTER ( STRDT ( ?fechaobs, xsd:dateTime ) < "2020-07-31T00:00:00"^^xsd:dateTime )
  }
}
```

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0APREFIX+esequip%3A+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Furbanismo-infraestructuras%2Fequipamiento-municipal%2F%3E%0D%0APREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0A%0D%0ASELECT+distinct+%3Fname+%3Falta%0D%0AWHERE+%7B%0D%0A++%3Fs+a+noise%3AEstacionMedida+%3B%0D%0A+++++schema%3Aname+%3Fname+%3B%0D%0A+++++esequip%3AfechaAlta+%3Falta+.%0D%0A++FILTER+%28+%3Falta+%3E+%222000%2F01%2F01%22%5E%5Exsd%3AdateTime+%29%0D%0A%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene información sobre cuantas estaciones de medida se han incluido desde el 01/01/2000.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>
PREFIX esequip: <http://vocab.linkeddata.es/datosabiertos/def/urbanismo-infraestructuras/equipamiento-municipal/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX schema: <http://schema.org/>

SELECT distinct ?name ?alta
WHERE {
  ?s a noise:EstacionMedida ;
     schema:name ?name ;
     esequip:fechaAlta ?alta .
  FILTER ( ?alta > "2000/01/01"^^xsd:dateTime )
}
```

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+noise%3A+%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fmedio-ambiente%2Fcontaminacion-acustica%23%3E%0D%0APREFIX+esequip%3A+%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Furbanismo-infraestructuras%2Fequipamiento-municipal%2F%3E%0D%0APREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0A%0D%0ASELECT+%28COUNT+%28%3Fs%29+as+%3FnuevasEstaciones%29%0D%0AWHERE+%7B%0D%0A++%3Fs+a+noise%3AEstacionMedida+%3B%0D%0A+++++esequip%3AfechaAlta+%3Falta+.%0D%0A++FILTER+%28+%3Falta+%3E+%222000%2F01%2F01%22%5E%5Exsd%3AdateTime+%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene sólamente el número de estaciones añadidas.

```
PREFIX noise: <http://vocab.ciudadesabiertas.es/def/medio-ambiente/contaminacion-acustica#>
PREFIX esequip: <http://vocab.linkeddata.es/datosabiertos/def/urbanismo-infraestructuras/equipamiento-municipal/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT (COUNT (?s) as ?nuevasEstaciones)
WHERE {
  ?s a noise:EstacionMedida ;
     esequip:fechaAlta ?alta .
  FILTER ( ?alta > "2000/01/01"^^xsd:dateTime )
}
```
