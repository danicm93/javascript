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

Si hacemos un if, vemos que el var no se limita al scope

```JS
var edad = 10

if(1==1){
	var edad = 20
	console.log('Scope', edad) // 20
}

console.log('Fuera Scope', edad) // 20
```

Si reemplazamos el Var por Let veremos como la consola nos lanza un error.
La principal diferencia entre el Var y el Let es que nos permite limitar su alcance al scope

```JS
let edad = 10
let edad = 20
console.log(edad) // error
```

```JS
// solución
let edad = 10
edad = 20
console.log(edad) // 20
```
