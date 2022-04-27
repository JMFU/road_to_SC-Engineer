## Level 0: Hello Ethernaut

Este es el primer nivel de la interfaz Ethernauts, interfaz que sirve para aprender sobre seguridad en contratos inteligentes.

# Pre-Requisitos

- Para este nviel cero solo necesitamos un poco de conocimiento de la consola de nuestro navegador.

- Tener una billetera Metamask

- Algo de Ether de prueba para la red con la que estes trabajando, en mi caso es Rickerbi.


# Manos a la obra

Para comenzar solo necesitamos leer las instrucciones. En ellas viene todo lo que necesitas saber para finalizar exitosamente este nivel.

Lo primero que nos pide esiniciar una instancia del contrato, para ellos simplemente damos clik en el botón de empezar instancia.

Acontinuación, dentro de la consola tecleamos lo primero que nos pide, solicitar indormación del contrato con info().

```javascript
await contract.info()

// Output: 'You will find what you need in info1().'
```
Observemos arriba, que en consola nos aparece un mensaje con la siguiente instrucción la cual nos pide introducir info1().

```javascript
await contract.info1()

// Output: 'Try info2(), but with "hello" as a parameter.'
```
Interesante, no pide que ahora usemos info2("hello") en la consola. Hagamoslo.

```javascript
await contract.info2("hello")

// Output: 'The property infoNum holds the number of the next info method to call.'
```

Vamos avanzando maravillosamente. siento que estamos llegando a algo empleemos infoNum para descubrir como romper el código

```javascript
await contract.infoNum()

// Output: galimatias
```

Probemos algo, intenemos volver dicho galimatías un número
```javascript
await contract.infoNum().then(v => v.toString())

// Output: 42
```

Genial, eso si es algo con lo que podemos trabajar, sigamos con nuestro objetivo, que este contrato no se rompera solo.

De acuerdo con las instrucciones, tenemos lo siguiente debemos usar info y el número 42, por lo tanto escribiremos en la consola info42().

```javascript
await contract.info42()

// Output: 'theMethodName is the name of the next method.'
```

Paso muy curioso el siguiente, parece ser que ya no debemos usar info. Escribamos pues theMethodName()

```javascript
await contract.theMethodName()

// Output: 'The method name is method7123949.'
```

Funcinó y de paso tenemos evidencia de que debemos continuar  con method7123949(). Let´s do it
```javascript
await contract.method7123949()

// Output: 'If you know the password, submit it to authenticate().'
```

Oh no, ya no nos pone que debemos hacer, pero viendo el help() obtenemos información nueva.
El help() nos revela que contract tienen varias opciones, por lo cual despues de escribir contract en la terminal obtenemos  lo siguiente:

```javascript
contract

// Output: { abi: ..., address: ..., ...., password: f () }
```

Intereserting, se ve una parte que dice password, llamemosla en consola.

```javascript
await contract.password()

// Output: 'ethernaut0`
```

Etselen, sigamos la última instrucción.
```javascript
await contract.authenticate('ethernaut0`)

```

Hecho todo eso, confirmamos en el metamask y listo, hemos completado este nivel cero.

Gracias a todo este trabajo y esfuerzo, podemos darlo por finalizado. Continuaremos con el nivel 1 en una siguiente entrada.
