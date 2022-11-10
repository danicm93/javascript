# Fundamentos

## Var, let, const

Un Var llamado edad y ésta sea 10, nosotros podemos nuevamente declarar que esa variable.
Y ahora que sea 20.
En el console.log podemos ver que son 20 y no nos pinta ningun tipo de error.
Esto puede ser un problema, si te va la hoya porque tienes mucho código.

```JS
var num = 10
var num = 20
console.log(num) // 20
```

Si reemplazamos el Var por Let veremos como la consola nos lanza un error.
La principal diferencia entre el Var y el Let es que nos permite limitar su alcance al scope

```JS
let num = 10
let num = 20
console.log(num) // error
```


Otro beneficio y la principal diferencia entre el Let y el Var
Si hacemos un if, vemos que el var no se limita al scope

```JS
var num = 10

if(true){
	var num = 20
	console.log('Scope', num) // 20
}

console.log('Fuera Scope', num) // 20
```

Esto mismo con Let, vemos que nos respeta el valor de 20 dentro del scope y fuera seguimos teniendo un 10

```JS
let num = 10

if(true){
	let num = 20
	console.log('Scope', num) // 20
}

console.log('Fuera Scope', num) // 10
```

Por otro lado tenemos las constantes,estas no van a cambiar con el tiempo (aunque tiene excepciones)
tambien limitadas por el scope, mismo ejemplo

```JS
const edad = 10

if(true){
	const edad = 20
	console.log('Scope', edad) // 20
}

console.log('Fuera Scope', edad) // 10
```

Si intentamos declarar la misma constante dos veces, obtenemos un error

```JS
const edad = 10
const edad = 20 // SyntaxError

const edad = 10
edad = 20 // Error: "edad" is read-only
```

Excepciones de las contanstes
Podemos utilizar funciones que modifican el array, si nos permite realizar dicha acción
Esto mismo pasa con los objetos ...

```JS
const nums = [10,20,30]
nums.push(40)
console.log(nums)
```

Tenemos un objeto al que le vamos a cambiar la edad y el apellido

```JS
const persona = {
  nombre: 'Paco',
  edad: 29
}

persona.edad = 21
persona.apellido = 'Garcia'

console.log(persona)
```

Que no se podría hacer, porque, porque estas reasignando

```JS
const persona = {
  nombre: 'Paco',
  edad: 29
}

persona.edad = 21
persona.apellido = 'Garcia'

persona = {
  nombre: 'Alberto',
  edad: 34
}

console.log(persona) //Uncaught TypeError: Assignment to constant variable.
```

Como hacer que no se modifique una constante

```JS
const persona = Object.freeze({
  nombre: 'Paco',
  edad: 29
});

persona.edad = 21
persona.apellido = 'Garcia'

console.log(persona)
```

## Funciones

Funcion clásica a función de flecha

```JS
function sum (left, right) {
  console.log(left + right)
}
sum(10, 20)

const sumArrow = (left, right) => {
  console.log(left + right)
}

sumArrow(10, 20)
```

Ventajas de las funciones de fecha, podemos reducir código

```JS
function sum (num) {
  console.log(num)
}
sum(10)

const sumArrow = num => {
  console.log(num)
}

sumArrow(20)
```

Podemos omitir returns

```JS
const sum = (left, right) => 'la suma es: ' + (left + right)
console.log(sum(10, 20))
```

Asignar valor por defecto

```JS
const sum = (sum = 10) => sum + 20
console.log(sum())
```

Podriamos tambien devolver un objeto desde una funcion de flecha
El objeto sin parentesis falla porque JS piensa que es el cuerpo de la función

```JS
const number = () => 22;
const array = () => [1,2,3];
const objectFail = () => {name : 'Jose'} // Fall
const object = () => ({name : 'Jose'}) // El bueno

console.log(number())
console.log(array())
console.log(objectFail())
console.log(object())
```

Otra cosa importante que debemos saber es que una funcion en JS puede devolvernos otra función

```JS
function hello(){
    return function(){
        return "Hola Digi"
    }
}

console.log(hello());
```

Podemos ejecutar la función interior simplemente colocando otros parentesis

```JS
console.log(hello()());
```

También podemos crear una función y ejecutarla al mismo tiempo

```JS
console.log(function greet(){
    return 'Hello people!'
}())
```

Incluso podemos quitarle el nombre, esto se utiliza mucho cuando trabajamos con eventos

```JS
console.log(function (){
    return 'Hello people!'
}())
```

## Template String

De esta forma podemos concatenar variables con string, hacer formulas, ...

```JS
const numero = (num1, num2) => {
  return `el numero es: ${num1 + num2}` 
}
```

## Objetos

Declaramos un objeto persona y vamos a añadirle diferentes propiedades

```JS
const persona = {
    nombre: 'Paco',
    apellido: 'Garcia',
    edad: 29,
    deportes: ['futbol', 'waterpolo', 'ping pong'],
    casado: true,
    links: {
      social: {
        twitter: 'https://twitter.com/nombre',
        facebook: 'https://facebook.com/nombre.developer',
      },
      web: {
        blog: 'https://nombre.com'
      }
    },
    enviarEmail : function () {
        return 'correo enviado';
    },
  };
  
console.log(persona)
console.log(persona.nombre)
console.log(persona.enviarEmail())
```

Podemos hacer mñas simple la función escribiendola de la siguiente manera

```JS
const persona = {
    nombre: 'Paco',
    apellido: 'Garcia',
    edad: 29,
    deportes: ['futbol', 'waterpolo', 'ping pong'],
    casado: true,
    links: {
      social: {
        twitter: 'https://twitter.com/nombre',
        facebook: 'https://facebook.com/nombre.developer',
      },
      web: {
        blog: 'https://nombre.com'
      }
    },
    enviarEmail() {
        return 'correo enviado';
    },
  };
```

Podemos acortar nombres si la constante o variable se llama igual que la clave

```JS
const name = 'Eva'
const age = '25'

const person = {
    name: name,
    age: age
}
    
console.log(person)
```

```JS
const person = {
    name,
    age,
}
console.log(person)
```


### Destructuring object

Para desestructurar un objeto, abrimos llaves y colo camos la propiedad que nos interesa sacar dentro de las llaves

```JS
const { apellido } = persona;
console.log(apellido)
```

Podemos desestructurar dentro de los parametros de una funcion

```JS
function printName(persona){
    console.log(persona.nombre)
}

printName(persona)

//Solucion
function printName({nombre}){
    console.log(nombre)
}
```

Podemos renombrar propiedades

```JS
const { twitter: tweet, facebook: fb } = wes.links.social;
console.log(tweet, fb)
```

Podemos desestructurar un segundo nivel y ademas

```JS
// Nivel 2
const { links: {web} } = persona
console.log(web)

//Nivel 3
const { links: {web : {blog} } } = persona
console.log(blog)
```

## Fetch API

La API Fetch proporciona una interfaz JavaScript para acceder y manipular partes del canal HTTP.
Necesitamos un then porque vamos a esperar una promesa
El then necesita una funcion de flecha y a está funcion le pasamos la respuesta
en un segundo then obtenemos la respuesta

```JS
fetch('https://rickandmortyapi.com/api/character')
.then(res => res.json())
.then(data => {
	console.log(data)
})
```

También tenemos el  catch

```JS
fetch('https://rickandmortyapi.com/api/character')
.then(res => res.json())
.then(data => {
	console.log(data)
})
.catch(error => console.log(error))
```

## Async / Await

Nos sinver para trabajar con promesas pero sin tener el engorro de encadenar los .then()
Los await van a funcionar siempre que estén dentro de una función async, hay excepciones, pero de momento nos quedamos con esto

```JS
const getCharacters = async () => {
	try{
		const res = await fetch('https://rickandmortyapi.com/api/character');
		const data = await res.json();
		console.log(data);
	}catch (error){
		console.log(error)
	}
}

getCharacters();
```

# Array method

Si tenemos un array, nosotros podemos recorrerlo facilmente con un bucle for



### Map

Crea un nuevo array con los resultados de la llamada a la función
Esto nos siver para depurar la respuesta que obtenemos


### Filter




