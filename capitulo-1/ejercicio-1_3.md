# Ejecicio 1.3.

## Enunciado

Define un procedimiento que toma tres numeros como argumentos y devuelve la suma de los cuadrados de los dos numeros mas grandes

## Respuestas

```scheme
(define (square x) (* x x))

(define (sum-of-squares x y) (+ (square x) (square y)))

(define (>= x y) (or (> x y) (= x y)))

(define (greater-num x y) (if (>= x y) x y))

(define (sum-of-greatest-squares x y z) 
  (cond ((and (>= x z) (>= y z)) (sum-of-squares x y)) 
        ((and (>= x y) (>= z y)) (sum-of-squares x z))
        ((and (>= y x) (>= z x)) (sum-of-squares y z))))
```

