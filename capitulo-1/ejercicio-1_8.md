# Ejercicio 1.8.

## Respuesta

```scheme
(define (improve guess x) 
  (/ 
    (+ (/ x (square guess)) (* 2 guess)) 
    3))

(define (good-enough? guess previous-guess) 
  (< (abs (- guess previous-guess)) 0.0000001))

(define (cubed-root guess x) 
  (if (good-enough? guess (improve guess x))
    guess
    (cubed-root (improve guess x) x)))

(define (cbrt x) (cubed-root 1.0 x))
```
