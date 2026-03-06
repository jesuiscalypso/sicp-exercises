# Ejercicio 1.12
## Enunciado

El patrón de numeros que se ve a continuación recibe el nombre de pirámide de Pascal:

<pre>
          1
        1   1
     1    2    1
   1   3     3   1
 1   4    6    4   1
         ...
</pre>

Los números en la parte externa del triangulo es la suma de los dos numeros que se encuentran por encima. Escribe un procedimiento que computa los elementos del triangulo de pascal por medio de un acercamiento recursivo.

## Respuesta

```scheme
(define (pascal-elem layer elem)
  (cond ((or (= elem 1) (= elem layer)) 1)
        (else (+ (pascal-elem (- layer 1) (- elem 1)) (pascal-elem (- layer 1) elem)))))

(define (print-pascal-layer-elems layer start)
    (if (> start layer) 
      (newline)
      (begin 
        (display (pascal-elem layer start)) 
        (display " ") 
        (print-pascal-layer-elems layer (+ start 1)))))

(define (print-pascal-layer layer curr)
    (if (> curr layer) 
        (newline)
        (begin
            (print-pascal-layer-elems curr 1)
            (print-pascal-layer layer (+ curr 1)))))

(define (print-pascal layer) 
  (print-pascal-layer layer 1))
```
