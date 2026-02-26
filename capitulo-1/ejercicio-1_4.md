# Ejecicio 1.4.

## Enunciado

Observa que nuestro modelo de evaluación permite combinaciones cuyos operadores son expresiones compuestas. Utiliza esta observación para describir el comportamiento del procedimiento que se muestra a continuación

## Respuestas

El procedimiento que se define es el siguiente:

```scheme
(define (a-plus-abs-b a b) 
  (if (> b 0) + -) a b))
```

Puede ser descrito en lenguaje natural de la siguiente manera:

```
CREAR UN PROCEDIMIENTO LLAMADO 'a-plus-abs-b' QUE TOMA DOS PARAMETROS FORMALES: A Y B
FUNCIONA DE LA SIGUIENTE MANERA:
	SI 'b' ES MAYOR QUE CERO (0), SUMARLE 'a' A 'b'
	SI NO, RESTARLE 'b' a 'a'
```

Esto se apoya en la naturaleza flexible de LISP. Podemos devolver operadores como resultado de procedimientos, de una manera similar a funciones de orden mayor. Por lo tanto, el valor de b siempre sera positivo:

- Si es positivo, se le resta a A
- Si no lo es, se le resta, pero como es negativo, se convierte en una sumatoria.

Por lo que efectivamente es como si el valor de B estuviera en el dominio y rango de la función valor absoluto. Podriamos replicar este comportamiento de manera menos obtusa asi:

```scheme
(define (a-plus-abs-b a b) 
  (+ a (abs b))
```

Pero calramente eso iria en contra del espiritu del ejercicio.
