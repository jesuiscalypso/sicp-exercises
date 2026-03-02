# Ejercicio 1.7
## Enunciado

La prueba `good-enough?` utilizada para calcular raíces cuadradas no será muy efectiva al encontrar las raices cuadradas de números muy pequeños. Aparte de eso, en computadoras reales, la operaciones arimetméticas casi siempre son realizadas con precisión limitada. Esto hace que nuestro predicado no sea adecuado para números muy grandes.

Explica lo mencionado anteriormente, con ejemplos que muestran el fallo del predicado. 

Una estrategia alternativa para implementar `good-enough?` es ver como el valor elegido cambia de una iteración a la siguiente y esperar a que el cambio sea una fracción muy pequeña del elegido. Diseña un nuevo predicado utilizando estos principios. ¿Funciona mejor para numeros grandes y pequeños?

## Exploración
### Inicial
```scheme
;iteración actual de la función

(define (good-enough? guess x)
    (< (abs ( - (square guess) x)) 0.001))

```

Resultados de trabajar con numeros grandes y pequeños:

```
1 ]=> (sqrt 0.000000000005782731095)

;Value: .03125000006162223 (Se esperaba 2.404730981835598e-6)


1 ]=> (sqrt 0.00056)

;Value: .03700193611450846 (Se esperaba 2.3664319132398463e-2)

1 ]=> (sqrt 0.0004)

;Value: .0354008825558513 (Se esperaba .02)

1 ]=> (sqrt 1000000000000000)
(El programa se detiene, se esperaba 31622776.60168379)
```
### ¿Que podría estar pasando?

La razón por la que las raices cuadradas aproximadas fallan con los numeros pequeños se debe a que el valor que se usa como criterio de parada no es lo suficientemente pequeño como para capturar los cambios necesarios. Si bien la diferencia entre 4.0005423 y 4.000546 no es mucho cuando se trata de la raiz de un numero grande, cuando hablamos de una pequeña, hay una gran diferencia entre 0.000523412 y 0.000643543, aunque ambos esten en el rango de 0.001 de diferencia. Aumentar el numero de ceros a la derecha del punto decimal hace que el resultado sea mas exacto, pero siempre habra algún punto en que se rompa.

Por su parte, los numeros muy grandes entran en un ciclo infinito / demasiado largo por la razón opuesta. Ya que las operaciones en un computador se realizan con una precisión limitada, llevar a cabo operaciones con numeros tan grandes incurre una pérdida de exactitud que resulta en que el calculo de la distancia nunca sea suficiente para obtener una respuesta satisfactoria (en el ejemplo de intentar calcular la raíz cuadrada de 1.000.000.000.000.000, la distancia termina siendo .125 sin importar que)

### Nueva función

```scheme
(define (square x) (* x x))

(define (good-enough? guess previous-guess) 
    (< (abs (- previous-guess guess)) 0.001))

(define (avg x y) 
  (/ (+ x y) 2))

(define (improve guess x) 
  (avg guess (/ x guess)))

(define (sqrt-iter-cont guess previous-guess x)
  (if (good-enough? guess previous-guess)
        guess
        (sqrt-iter-cont (improve guess x) guess x)
    ))

(define (sqrt-iter guess x)
  (sqrt-iter-cont guess (+ guess 1) x))
```

Este nuevo acercamiento si funciona mejor para grandes numeros, y para pequeños dentro de cierto limite.
