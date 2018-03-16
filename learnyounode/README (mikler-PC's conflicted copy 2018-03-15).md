

1. HELLO WORLD
```javascript
console.log("HELLO WORLD")
```
1. BABY STEPS
>  Escribe un programa que reciba uno o más números como argumentos de la consola e imprima la suma de dichos números a consola(stdout).

_process:_ objecto global de __nodejs__, _argv_ es una propiedad de process que es un array
#### Ejemplo
> $ node program.js 1 2 3  

>  La salida estándar a consola será algo parecido a:  

  [ 'node', '/path/to/your/program.js', '1', '2', '3' ]  

```javascript

var contador = 0

for(var i = 2; i < process.argv.length; i++){
	contador += Number(process.argv[i]);
}
console.log(contador)
```
3. _MY FIRST I/O_
>Escribe un programa que, usando una llamada síncrona al sistema de  archivos, lea un archivo recibido por argumento e imprima a consola la cantidad de saltos de línea ('\n') que contiene. Similar a ejecutar _cat file | wc -l._  
El programa recibirá la ruta al archivo como único argumento.  

```javascript
var fs = require('fs');
//buffer esta en un formato eficiente como es ASCII, binario,UTF-8.
var buffer = fs.readFileSync(process.argv[2]);
var text = buffer.toString(); // se convierte a String para detectar '\n' los saltos de linea

console.log(text.split('\n').length -1);
```
4. MY FIRST ASYNC I/0
> Escribe un programa que use operación de sistema de archivos asíncrona para leer un archivo e imprimir en consola el número de saltos de línea  
  ('\n') que contiene. Similar a  ejecutar cat file | wc -l.  
   El programa recibirá la ruta al archivo como único argumento.

```javascript
var fs = require('fs');
fs.readFile(process.argv[2],'utf-8', function(err, data){
	if(err){return console.log(err)}
	console.log(data.split('\n').length -1);
})
```
5. FILTERED LS
> Crea un programa que dado un directorio imprima una lista de archivos  
  filtrados por la extensión. El primer argumento será la ruta al directorio  
  (ej: '/path/dir/') y el segundo la extensión a filtrar, por ejemplo si  
  recibes 'txt' deberás filtrar todos los archivos que terminen en .txt.  
   Nota: el segundo argumento no incluye el punto '.'.  
   La lista de archivos a imprimir en consola debe hacerse un archivo por  
  línea y debes utilizar Async I/O.

```javascript
var fs = require('fs');
var path = require('path');

var ext = '.'+ process.argv[3];/*[3] ext de archivos */
var url = process.argv[2]
fs.readdir(url,function(err,files){
	if(err){ return console.error(err)}

	files.forEach(function(file){
		if(path.extname(file) === ext){/* comprobar para filtrar por su ext*/
			console.log(file);
		}
	});

});
```
6. MAKE IT MODULAR

```javascript

```

7.
8.
9.
10.
11.
>> Escribe un servidor HTTP que sirva un mismo archivo de texto para todas las peticiones que reciba.  
El servidor deberá escuchar en un puerto cuyo número será el primer argumento del programa. Como segundo argumento recibirá la ruta a la ubicación del archivo. Debes usar fs.createReadStream() para servir como stream los contenidos del archivo en la respuesta del servicio.  

> Los parámetros requesty response son los objetos que representan la petición y su respuesta respectivamente. La petición provee propiedades, como ser el encabezado y los parámetros de la misma. La respuesta permite devolverle al cliente encabezados y un cuerpo (body).
