# Ejercicio 1.11

Una funcion `f` es es definida por la siguiente regla:

f(n) = n; si n < 3
Si no, f(n) = f(n-1) + 2f(n-2) + 3f(n-3)

Escriba dos procedimientos: Uno que calcule f de manera recursiva y otro que lo haga de manera iterativa

## Respuesta

```scheme
(define (f n)
    (cond ((< n 3) n)
          (else 
            (+ 
                (f (- n 1))  
                (* 2 (f (- n 2)))  
                (* 3 (f (- n 3)))))))
```

```scheme
(define (f n)
    (if (< n 3) 
        n 
        (f-iter n 2 2 1 0)))

(define (f-iter n count p1 p2 p3)
	( if ( = count n )
		p1
		(f-iter 
            n 
            (+ count 1)
			(+ p1 (* 2 p2) (* 3 p3))
			p1 
            p2)))
```



