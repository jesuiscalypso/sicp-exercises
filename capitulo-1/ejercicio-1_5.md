# Ejecicio 1.5.

## Enunciado

Ben Bitdiddle ha inventado una prueba para determinar si el intérprete que está utilizando para programar en LISP evalua sus expresiones en orden normal o en orden de aplicación. Para ello define los siguientes procedimientos:

```scheme
    (define (p) (p))
    (define (test x y)
        (if (= x 0) 0 y))
```

Entonces pasa a evaluar la siguiente expresión:

```
    (test 0 (p))
```

¿Que comportamiento observará Ben en cada caso? Explica tu respuesta

## Respuesta (INCORRECTA)

Cuando hablamos de un intérprete que hace evaluación en orden normal, significa que expande todas las expresiones hasta el punto en que la combinación esté compuesta solamente de valores y operadores primitivos antes de evaluar si quiera una vez. Por lo tanto, la expresión anterior quedaría expresada de la siguiente manera:

<pre>
    (test 0 (p))
    // reemplazamos test por su cuerpo y sus parametros, x = 0, y = (p)
    -> (if (= 0 0) 0 (p))
    // remplazamos (p) por sus parametros, (p) = (p)
    -> (if (= 0 0) 0 (p))
    // remplazamos (p) por sus parametros, (p) = (p)
    -> (if (= 0 0) 0 (p))
    //... ad infinitum
</pre>


Según entiendo, como la evaluación en orden normal requiere que se expanda la expresión hasta llegar a una que solo tenga valores primitivos, un intérprete que lo utilice se quedaría atrapado en la expansión. Una especia de bucle infinito.

Por su parte, llevar a cabo evaluación en orden de aplicación implica reemplazar los parametros formales por los actuales y luego evaluar inmediatamente. Por lo tanto, en el caso de un intérprete de esta naturaleza, tendriamos el siguiente resultado:

<pre>
    (test 0 (p))
    // reemplazamos t por el cuerpo de la funcion
    -> (if (= x 0) 0 y)
    // reemplazamos los operandos, x = 0, (p) = (p)
    -> (if (= 0 0) 0 (p))
    // evaluamos la expresión. como 0 = 0, devolvemos el valor de x (0)
    -> 0
</pre>

Por lo menos, esto es lo que entiendo.

## Respuesta Correcta

Las respuestas estan al revés. Se puede usar las siguientes frases como base:

- En el modelo aplicativo, el interprete **evalua todos los parametros** y luego aplica los operadores
- En el normal, el interprete **solamente evalua los parametros cuando es necesario**
