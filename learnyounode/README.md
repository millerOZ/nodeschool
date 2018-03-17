

1.  HELLO WORLD 
```javascript
'use strict'
console.log("HELLO WORLD")
```
2. BABY STEPS
>  Escribe un programa que reciba uno o más números como argumentos de la consola e imprima la suma de dichos números a consola(stdout).

_process:_ objecto global de __nodejs__, _argv_ es una propiedad de process que es un array
#### Ejemplo
> $ node program.js 1 2 3  

>  La salida estándar a consola será algo parecido a:  

_[ 'node', '/path/to/your/program.js', '1', '2', '3' ]_

```javascript
'use strict'
var numeroLineas = function(){
  var contador = 0
/*  El primer elemento de la lista siempre es
  'node', el segundo es la ruta al program.js; por ende, debes comenzar a
  iterar en el tercer elemento (índice 2 de la lista)*/
  for(var i = 2; i < process.argv.length; i++){
  	contador += Number(process.argv[i]);
  }
  return contador;
}
console.log(numeroLineas())
```
3. _MY FIRST I/O_
>Escribe un programa que, usando una llamada síncrona al sistema de  archivos, lea un archivo recibido por argumento e imprima a consola la cantidad de saltos de línea ('\n') que contiene. Similar a ejecutar _cat file | wc -l._  
El programa recibirá la ruta al archivo como único argumento.  

```javascript
'use strict';
var fs = require('fs');
var file = process.argv[2];
var llamadaSincronica = function(file){
	let buffer = fs.readFileSync(file,'utf8');
	let saltosLinea = buffer.split('\n').length -1;

	return saltosLinea;
}
console.log(llamadaSincronica(file));
```
4. MY FIRST ASYNC I/0
> Escribe un programa que use operación de sistema de archivos asíncrona para leer un archivo e imprimir en consola el número de saltos de línea  
  ('\n') que contiene. Similar a  ejecutar cat file | wc -l.  
   El programa recibirá la ruta al archivo como único argumento.

```javascript
'use strict';
var fs = require('fs');
const files = process.argv[2];

var fileasyn = function(file){
 if(file != null){
    fs.readFile(file,'utf-8',function(err,data){
       if(err){
       		return console.log(err);
       	}
       return console.log(data.split('\n').length -1);
    });
  }else{
  	console.log("Error archivo null")
  }
}
fileasyn(files);
```
5. FILTERED LS
>  Crea un programa que dado un directorio imprima una lista de archivos  
  filtrados por la extensión. El primer argumento será la ruta al directorio  
  (ej: '/path/dir/') y el segundo la extensión a filtrar, por ejemplo si  
  recibes 'txt' deberás filtrar todos los archivos que terminen en .txt.  
  Nota: el segundo argumento no incluye el punto '.'.  
  La lista de archivos a imprimir en consola debe hacerse un archivo por  
  línea y debes utilizar Async I/O.

```javascript
var fs = require('fs');
var path = require('path');

var ext = '.'+ process.argv[3]; /*[3] ext de archivos */
var url = process.argv[2]
fs.readdir(url,function(err,files){
	if(err){ return console.error(err)}

	files.forEach(function(file){
		if(path.extname(file) === ext){   /*extname devuelve ext del archivo comprobar para filtrar por su ext*/
			console.log(file);
		}
	});

});

```
6. MAKE IT MODULAR
> Este problema es similar al anterior e introduce la idea de módulos.  
  Deberás crear dos archivos para resolver el ejercicio.  
  El programa debe imprimir el listado de archivos de un directorio  
  filtrando por extensión. Nuevamente el primer argumento será la ruta al  
  directorio (ej: '/path/dir/') y el segundo la extensión a filtrar, por  
  ejemplo si recibes 'txt' deberás filtrar todos los archivos que terminen  
  en .txt. Debes usar Async I/O.  
  Deberás escribir un archivo modular para hacer la tarea. Dicho módulo debe  
  exportar una función que reciba tres parámetros en orden: la ruta del  
  directorio, la extensión para filtrar y una función de callback. La idea  
  es encapsular toda la lógica dentro del módulo.  
  En Node, los callbacks suelen tener una firma convencional de tener  
  (error, data). Esto implica que si hay un error el primer parámetro  
  devuelve el error sino viene null y el segundo parámetro son los datos.  
  Para este ejercicio los datos a devolver es la lista de archivos en forma  
  de Array. Si occurre un error, por ejemplo en la llamada a fs.readdir(),  
  el callback debe llamarse con dicho error.  
  Para completar el ejercicio no debes imprimir desde el módulo, sólo desde  
  el programa principal. En caso de que el módulo devuelva un error a tu  
  programa principal, simplemente compruébalo y escribe un mensaje  
  informativo en consola.  
  El módulo debe cumplir el siguiente contrato:  
   1. Exportar una función que reciba los parámetros mencionados.  
   2. Llamar al callback una única vez cuando ocurre un error o con la lista  
      correspondiente.  
   3. No debe modificar variables globales o stdout.  
   4. Capturar los posibles errores y devolverlos en el callback.  
  La ventaja de usar contratos es que el módulo puede ser usado por  
  cualquiera que asuma este contrato.  

```javascript
//mymodule.js
var fs = require('fs');
var path = require('path');

module.exports = function (dir,filter, cb){
    fs.readdir(dir,function (err,array){

        if(err){
        	return cb(err) //devuelve errores en el callback
        }
        array = array.filter(function(file){
            return path.extname(file) === '.' + filter;
        })
        cb(null,array);
    })
}
```
```javascript
const filterFn = require('./mymodule');
const dir = process.argv[2];
const filter = process.argv[3];//ext del archivo a filtrar

filterFn(dir, filter, function(err, array){
	  if(err){
	    return console.error("There was an error: ", err);
	  }
	  array.forEach(function(file){
	    console.log(file);
	  })
})

```
7. HTTP CLIENT
> Escribe un programa que reciba como argumento una URL y realice una  
  petición HTTP GET a la misma. Luego, deberá imprimir por consola el  
  contenido de cada evento "data" de la petición, uno por línea.  

```javascript
const http = require('http');

var url = process.argv[2];

http.get(url, function(res){
	res.setEncoding('utf8') //convierte la data recibida a String
	res.on('data', function(data){
		console.log(data)
	})
	res.on('error',console.error)

}).on('error', console.error)

```
8. HTTP COLLECT
> Escribe un programa que realice una petición HTTP GET a una URL provista  
  como primer argumento del programa. Almacena todos los datos recibidos del  
  servidor, es decir no sólo el primer evento "data", y luego escribe a  
  consola dos líneas:  
   » En la primera escribe la cantidad de caracteres recibidos.                  
   » En la segunda escribe la totalidad de caracteres recibidos (todo el string).

```javascript
var http = require('http');
var bl = require('bl');

const url = process.argv[2];

http.get(url,function(res){

	res.pipe(bl(function(err,data){
		if(err){
			return console.err(err)
		}
		data = data.toString()
		console.log(data.length)
		console.log(data)
	}))
})
```
9.JUGGLING ASIC
> Este ejercicio es similar al anterior puesto que debes usar http.get().  
  Sin embargo, esta vez tu programa recibirá tres URLs como argumentos.  
  Tu programa deberá imprimir el contenido de cada una de las URLs en  
  consola en el mismo orden que fueron recibidos los argumentos. No deberás  
  imprimir el largo, solo el contenido como String, pero debes respetar el  
  orden de llegada de los argumentos.

```javascript
//tiene un error que no entiendo como se soluciona
var http = require('http');
var bl = require('bl');

dataList = []

for (var i = 0; i < 3; i++){

	http.get(process.argv[i],function(res){

		res.pipe(bl(function(err,data){
			if(err){
				return console.err(err)
			}
			dataList[i] = data.toString()

			/*console.log(data)*/
		}))
    })
}
for(i = 0; i < 3; i++){
	console.log(dataList[i])
}
```
10. TIME SERVER
> ¡Crea un Servidor de tiempo y hora TCP !  
  El servidor debe escuchar conexiones TCP en el puerto indicado por el  
  primer argumento del programa. Para cada conexión debes escribir la fecha  
  actual y la hora en formato 24hs del siguiente modo:  
     "AAAA-MM-DD hh:mm"  
  seguido por un carácter newline('\n'). Tanto el mes, el día como la hora y  
  minuto deben tener un 0 para ocupar 2 espacios, por ejemplo:  
     "2013-07-06 17:42"

```javascript
var net = require('net');
var port = process.argv[2]
function formato(mes){
	if(Number(mes) < 9){
		mes = mes + 1
		return '0' + mes
	}
}

var server = net.createServer(function(socket){
	var date = new Date()

	let anio = date.getFullYear()
	let mes = formato(date.getMonth())
	let dia = date.getDate()
	let hora = date.getHours()
	let min = date.getMinutes()

	var fecha = anio + "-"+ mes+"-"+dia+" "+hora+":"+min+"\n";
	socket.write(fecha)
	socket.end()
})
server.listen(port)
```
11. FILE SERVER HTTP
> Escribe un servidor HTTP que sirva un mismo archivo de texto para todas  
  las peticiones que reciba.  
  El servidor deberá escuchar en un puerto cuyo número será el primer  
  argumento del programa. Como segundo argumento recibirá la ruta a la  
  ubicación del archivo. Debes usar fs.createReadStream() para servir como  
  stream los contenidos del archivo en la respuesta del servicio.

```javascript
var http = require('http')
var fs = require('fs')
var file = process.argv[3]

server = http.createServer(function(req, res){
	fs.createReadStream(file).pipe(res)
});
server.listen(process.argv[2])

```
12.UPPERCASE HTTP
>   
  Escribe un servidor HTTP que reciba sólo peticiones POST y convierta los  
  caracteres del cuerpo de la petición a mayúsculas y lo devuelva al  
  cliente.  
  El servidor deberá escuchar en un puerto cuyo número será el primer  
  argumento del programa.  

```javascript
var http = require('http')
var map = require('through2-map')

server = http.createServer(function(req, res){
	if(req.method == 'POST'){
		req.pipe(map(function(chunk){
			return chunk.toString().toUpperCase();
		})).pipe(res);

	}
});
server.listen(process.argv[2]);
```
