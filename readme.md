# TypeScript en 5 minutos



Comencemos creando una aplicación web simple con TypeScript.

## Instalación de TypeScript

Hay dos formas principales de obtener las herramientas TypeScript:

- Vía npm (el administrador de paquetes Node.js)
- Al instalar los complementos de Visual Studio de TypeScript

Visual Studio 2017 y Visual Studio 2015 Update 3 incluyen TypeScript de forma predeterminada. Si no instaló TypeScript con Visual Studio, aún puede [descargarlo](https://www.typescriptlang.org/#download-links) .

Para usuarios de NPM:

```bash
npm install -g typescript
```

## Construyendo su primer archivo TypeScript

En su editor, escriba el siguiente código JavaScript en `greeter.ts`:

```ts
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

## Compilando su código

Utilizamos una `.ts`extensión, pero este código es solo JavaScript. Podría haber copiado / pegado esto directamente desde una aplicación JavaScript existente.

En la línea de comando, ejecute el compilador TypeScript:

```bash
tsc greeter.ts
```

El resultado será un archivo `greeter.js`que contiene el mismo JavaScript que usted introdujo. ¡Estamos funcionando con TypeScript en nuestra aplicación JavaScript!

Ahora podemos comenzar a aprovechar algunas de las nuevas herramientas que ofrece TypeScript. Agregue una `: string`anotación de tipo al argumento de la función 'persona' como se muestra aquí:

```ts
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Miguel Céspedes";

document.body.textContent = greeter(user);
```

## Escribir anotaciones

Las anotaciones de tipo en TypeScript son formas ligeras de registrar el contrato previsto de la función o variable. En este caso, pretendemos llamar a la función de saludo con un solo parámetro de cadena. Podemos intentar cambiar la llamada de bienvenida para pasar una matriz en su lugar:

```ts
function greeter(person: string) {
    return "Hello, " + person;
}

let user = [0, 1, 2];

document.body.textContent = greeter(user);
```

Al volver a compilar, ahora verá un error:

```shell
error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'.
```

Del mismo modo, intente eliminar todos los argumentos de la llamada de bienvenida. TypeScript le informará que ha llamado a esta función con un número inesperado de parámetros. En ambos casos, TypeScript puede ofrecer un análisis estático basado tanto en la estructura de su código como en las anotaciones de tipo que proporcione.

Tenga en cuenta que aunque hubo errores, el `greeter.js`archivo aún se crea. Puede usar TypeScript incluso si hay errores en su código. Pero en este caso, TypeScript advierte que su código probablemente no se ejecutará como se esperaba.

## Interfaces

Desarrollemos más nuestra muestra. Aquí usamos una interfaz que describe objetos que tienen un campo de nombre y apellido. En TypeScript, dos tipos son compatibles si su estructura interna es compatible. Esto nos permite implementar una interfaz simplemente teniendo la forma que requiere la interfaz, sin una `implements`cláusula explícita .

```ts
interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Miguel", lastName: "Céspedes" };

document.body.textContent = greeter(user);
```

## Clases

Finalmente, ampliemos el ejemplo una última vez con clases. TypeScript admite nuevas características en JavaScript, como el soporte para programación orientada a objetos basada en clases.

Aquí vamos a crear una `Student`clase con un constructor y algunos campos públicos. Observe que las clases y las interfaces juegan bien juntas, permitiendo que el programador decida sobre el nivel correcto de abstracción.

También es de destacar que el uso de `public`argumentos en el constructor es una forma abreviada que nos permite crear automáticamente propiedades con ese nombre.

```ts
class Student {
    fullName: string;
    constructor(public firstName: string, public middleInitial: string, public lastName: string) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    middleInitial: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.middleInitial + " " + person.lastName;
}

let user = new Student("Miguel", "A.", "Céspedes");

document.body.textContent = greeter(user);
```

Vuelva a ejecutar `tsc greeter.ts`y verá que el JavaScript generado es el mismo que el código anterior. Las clases en TypeScript son solo una abreviatura para el mismo OO basado en prototipos que se usa con frecuencia en JavaScript.

## Ejecutando su aplicación web TypeScript

Ahora escriba lo siguiente en `greeter.html`:

```html
<!DOCTYPE html>
<html>
    <head><title>TypeScript Greeter</title></head>
    <body>
        <script src="greeter.js"></script>
    </body>
</html>
```

¡Abre `greeter.html`en el navegador para ejecutar tu primera aplicación web TypeScript simple!

Opcional: abra `greeter.ts`en Visual Studio o copie el código en el área de juegos de TypeScript. Puede pasar el cursor sobre los identificadores para ver sus tipos. Tenga en cuenta que en algunos casos estos tipos se infieren automáticamente para usted. Vuelva a escribir la última línea y vea las listas de finalización y la ayuda de parámetros en función de los tipos de elementos DOM. Coloque el cursor sobre la referencia a la función de bienvenida y presione F12 para ir a su definición. Observe también que puede hacer clic con el botón derecho en un símbolo y usar la refactorización para cambiarle el nombre.

La información de tipo proporcionada funciona junto con las herramientas para trabajar con JavaScript a escala de aplicación. Para obtener más ejemplos de lo que es posible en TypeScript, consulte la sección Muestras del sitio web.