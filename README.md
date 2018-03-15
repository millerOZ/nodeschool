## nodeschool
* [learnyounode](learnyounode/README.md)


1. HELLO WORLD
```javascript
console.log("HELLO WORLD")
```
1. BABY STEPS

_process:_ objecto global de __nodejs__ 

```javascript

var acum = 0

for(var i = 2; i < process.argv.length; i++){
	acum += Number(process.argv[i]);
}
console.log(acum)
```
3. _MY FIRST I/O_

```javascript
var fs = require('fs');
var buffer = fs.readFileSync(process.argv[2]);
var str = buffer.toString();

var value = str.split('\n').length -1;
console.log(value);
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
