# Fundamentos

## Fundamentos

Un Var llamado edad y ésta sea 10, nosotros podemos nuevamente declarar que esa variable.
Y ahora que sea 20.
En el console.log podemos ver que son 20 y no nos pinta ningun tipo de error.
Esto puede ser un problema, si te va la hoya porque tienes mucho código.

```JS
var edad = 10
var edad = 20
console.log(edad) // 20
```

Si reemplazamos el Var por Let veremos como la consola nos lanza un error.
La principal diferencia entre el Var y el Let es que nos permite limitar su alcance al scope

```JS
let edad = 10
let edad = 20
console.log(edad) // error
```


Otro beneficio y la principal diferencia entre el Let y el Var
Si hacemos un if, vemos que el var no se limita al scope

```JS
var edad = 10

if(1==1){
	var edad = 20
	console.log('Scope', edad) // 20
}

console.log('Fuera Scope', edad) // 20
```

Esto mismo con Let, vemos que nos respeta el valor de 20 dentro del scope y fuera seguimos teniendo un 10

```JS
let edad = 10

if(1==1){
	let edad = 20
	console.log('Scope', edad) // 20
}

console.log('Fuera Scope', edad) // 10
```


Por otro lado tenemos las constantes,estas no van a cambiar con el tiempo (aunque tiene excepciones)
tambien limitadas por el scope, mismo ejemplo

```JS
const edad = 10

if(1==1){
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
