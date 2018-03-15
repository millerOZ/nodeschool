

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

```javascript

```
5. FILTERED LS

```javascript

```
6. MAKE IT MODULAR

```javascript

```
