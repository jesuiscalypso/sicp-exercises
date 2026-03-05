# Ejercicio 1.6.

## Enunciado

Alyssa P. Hacker no entiende porque es necesario que el constrcutor`if` debe ser definido de manera especial por el intérprete. 

> "¿or qué no puedo definirlo como un procedimiento ordinario en términos de `cond`?"

Su amiga, Eva Lu Adora dice que esto puede hacerse, y define una nueva versión de la siguiente manera:

```scheme
(define (new-if predicate then-clause else-clause)
  (cond (predicate then-clause)
        (else else-clause)))
```

Eva luego le desmuestra el programa a Alyssa de la siguiente manera:

```scheme
(new-if (= 2 3) 0 5)
5
(new-if (= 1 1) 0 5)
0
```

Encantada, Alyssa utiliza `new-if` para re-escribir el programa de la raiz cuadrada:

```scheme
(define (sqrt-iter2 guess x)
  (new-if (good-enough? guess x)
          guess
          (sqrt-iter (improve guess x) x)))
```

**¿Qué ocurre cuando Alyssa intenta utilizar esto para calcular las raices cuadradas? Explícalo**

## Exploración

```scheme
(define (new-if predicate then-clause else-clause)
  (cond (predicate then-clause)
        (else else-clause)))

(define (sqrt-iter guess x)
  (new-if (good-enough? guess x)
          guess
          (sqrt-iter (improve guess x) x)))

(define (improve guess x)
(average guess (/ x guess)))

(define (average x y)
(/ (+ x y) 2))


(define (good-enough? guess x)
(< (abs (- (square guess) x)) 0.001))
```

## Resultado

El procedimiento `new-if` causa que el programa entre en un bucle infinito. Esto ocurre porque a diferencia de la forma especial `if`, evalua ansiosamente todos los parametros (el predicado y las clausulas) lo que resulta que se tranque en la ejecución recursiva de `sqrt-iter`

