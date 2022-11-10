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

## Array method

### Foreach

Si tenemos un array, nosotros podemos recorrerlo facilmente con un bucle for, pero no va a ser lo normal
Lo más seguro es que utilicemos algun método relacionando con arrays
Los datos los tenemos que manipular dentro de la función

```JS
const getCharacters = async () => {
	try{
		const res = await fetch('https://rickandmortyapi.com/api/character');
		
        const { results } = await res.json();

		for (let i = 0; i < results.length; i++) {
            const character = results[i];
            console.log(character.name)
        }

	}catch (error){
		console.log(error)
	}
}

getCharacters();
```

Para hacerlo mas sencillo podemos utilizar el metodo foreach, 
el foreach recibe como parametro una funcion que al ejecutarse nos va a retornar
el valor que la funcion esta recibiendo
El foreach va recorriendo los elementos y a medida que los recorre, la funcion lo recibe como parametro

```JS
results.forEach(function(character){
            console.log(character.name)
        })
```

### Map / Spread Operator

Usaremos un Map cuando queramos generar un array nuevo. El Map nos retorna un nuevo array
Crea un nuevo array con los resultados de la llamada a la función
Esto nos siver para depurar la respuesta que obtenemos
El map no modifica el array anterior, sino que crea uno nuevo

Vamos a crearnos nuestro propio array de objetos con lo que a nosotros nos interesa

```JS
const getCharacters = async () => {
	try{
		const res = await fetch('https://rickandmortyapi.com/api/character');
		
        const { results } = await res.json();

        console.log(results);

        /*results.forEach(function(character){
            console.log(character.name)
        })*/

        const charactersBasic = results.map(character => {
            return {
                id: character.id,
                name: character.name,
                status: character.status,
                idName : `${character.id} - ${character.name}`
            }
        })

        console.log(charactersBasic);

	}catch (error){
		console.log(error)
	}
}

getCharacters();
```

Ahora imaginaros que digo, vale, quiero lo que ya tenía antes y además añadirle propiedades que me interesan a mi,
para ello tenemos algo llamado Spread Operator que nos permite romper el objeto anterior para crear uno nuevo
de esta forma no tenemos que ir añadiendo propiedad por propiedad

```JS
const getCharacters = async () => {
	try{
		const res = await fetch('https://rickandmortyapi.com/api/character');
		
        const { results } = await res.json();

        console.log(results);

        /*results.forEach(function(character){
            console.log(character.name)
        })*/

        const charactersBasic = results.map(character => {
            return {
                ...character,
                id: character.id,
                name: character.name,
                status: character.status,
                id : `${character.id} - ${character.name}`,
                idName : `${character.id} - ${character.name}`
            }
        })

        console.log(charactersBasic);

	}catch (error){
		console.log(error)
	}
}

getCharacters();
```

Para limpiar el return, recordamos que no podemos poner directamente llaves {} porque JS cree que estamos dentro del cuerpo de la función
Asi que lo que tenemos que hacer es simplemente añadirle parentesis () y solucionado

```JS
const charactersBasic = results.map(character => ({
                ...character,
                id: character.id,
                name: character.name,
                status: character.status,
                id : `${character.id} - ${character.name}`,
                idName : `${character.id} - ${character.name}`
        }))
```

### Filter

Al igual que el map, podemos recoger elementos, pero además podemos añadirle una condición y si se cumple la condición nos va a devolver un array nuevo

Sino copnemos una condición, nos devuelve un array vacio

```JS
const charactersFiltered = results.filter(character => {
            console.log(character)
        })

        console.log(charactersFiltered); // []
```

A diferencia del map, sino devolvemos nada, optenemos un undefined por elemento

```JS
const charactersFiltered = results.map(character => {
            console.log(character)
        })

        console.log(charactersFiltered); // [undefined,...]
```

Ahora, si queremos solo a los personajes que están vivos

```JS
const charactersFiltered = results.filter(character => {
            if(character.status === 'Alive'){
                return true;
            }
        })

        console.log(charactersFiltered);
```

Este código se podría resumir de la siguiente manera

```JS
const charactersFiltered = results.filter(character => character.status === 'Alive')
console.log(charactersFiltered);
```

Incluso, si nuestro objetivo es añadir úna propiedad más a nuestros objetos y además filtrarlos, 
podemos hacer lo siguiente

```JS
const characters = results.map(character => ({
            ...character,
            id: character.id,
            name: character.name,
            status: character.status,
            id : `${character.id} - ${character.name}`,
            idName : `${character.id} - ${character.name}`
        })).filter(character => character.status === 'Alive')
console.log(characters);
```

### Reduce

Si yo quisiese obtener la suma de todos los puntos de los personajes
La diferencia principal es que en lugar de obtener como primer parametro el objeto que se está recorriendo en ese momento,
recibimos primero un acumulador y seguido el objeto que recorremos.
Terminada nuestra función de flecha le pasamos al reducer como segundo parametro el valor por defecto del acumulador, en este caso el "cero"

```JS
const sumPoints = characters.reduce((total, character) => {
            return total + character.points
        }, 0)

console.log(sumPoints);
```

Esto se puede dejar en una sola linea de la siguiente manera

```JS
const sumPoints = characters.reduce((total, character) => total + character.points, 0)
console.log(sumPoints);
```

Ahora vamos a hacerlo un poco más complicado, lo que quiero es saber es cuantas especies tengo en mi array de personajes
Para ello hacemos lo siguiente

```JS
const totalSpecies = characters.reduce((total, character) => [...total, character.species], [])
console.log(totalSpecies);
```

Como podeis ver, tenemos especies dublicadas, yo no quiero eso, para eso hay una clase relativamente nueva en JS
que es Set, simplemente englobamos nuestro nuevo array dentro de un Set y de esta forma si existe un elemento en el array, 
no nos lo va volver a añadir

```JS
const totalSpecies = characters.reduce((total, character) => [...total, character.species], [])
console.log(totalSpecies);
```

Pero, claro, ahora hemos perdido nuestro array, para que esto vuelva a ser un array simplemente
Envolvemos nuestro código dentro de un Array.from

```JS
const totalSpecies = characters.reduce((total, character) => 
            Array.from(new Set([...total, character.species])), 
            []
        )

        console.log(totalSpecies);
```
