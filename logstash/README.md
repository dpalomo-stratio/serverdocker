# ELK mas REDIS

En esta composicion tenemos un entorno elk y un redis. Logstash estara leyendo sobre un lista de redis con la clave logstash y todo lo que lea lo indexara en elasticsearch y se podra visualizar en kibana.
A su vez se elimina el registro en redis.

## Usage
Una vez arrancado el entorno podemos acceder a los servicios en los siguientes puertos:
* Elasticsearch: localhost:9200
* Kibana: localhost:5601
* Redis: localhost:6379

Y para probar nuestra indexacion tendremos que añadir un valor en redis sobre la clave logstash con formato de lista.


```bash
 RPUSH logstash  '{ "arrayColores":[{ "nombreColor":"rojo", "valorHexadec":"#f00"  }, {  "nombreColor":"verde", "valorHexadec":"#0f0" }, { "nombreColor":"azul", "valorHexadec":"#00f" }]}'
```

La configuracion de logstash se encuentra en la carpeta config dentro del proyecto.


