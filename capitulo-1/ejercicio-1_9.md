# Ejercicio 1.8.
## Enunciado

Los siguientes procedimientos definen un método para sumar dos enteros positivos según los términos del procedimiento `inc`, el cual aumenta el el argumento por 1, y `dec`, que lo decrementa por 1.

```scheme
(define (+ a b)
    (if (= a 0) b (inc (+ (dec a) b))))

(define (+ a b)
    (if (= a 0) b (+ (dec a) (inc b)))
```

Utilizando el modelo de sustitiución, ilustra el proceso generado por cada proceso al evaluar `(+ 4 5)`. ¿Son estos procesos iterativos o recursivos?

## Respuesta

El primer procedimiento es recursivo, mientras que el segundo es iterativo.
