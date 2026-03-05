# Ejercicio 1.10

# Respuesta

```scheme
1 ]=> (A 1 10)

;Value: 1024

1 ]=> (A 2 4)

;Value: 65536

1 ]=> (A 3 3)

;Value: 65536
```

Por su parte, debido a la manera en que se comportan las funciones definidas, podemos sostener que matematicamente calculan los siguientes valores:

1. `(f n) = (A 0 n) = 2*n`
2. `(g n) = (A 1 n) = 2^n`
3. `(h n) = (A 2 n) = 2 si x = 1; 2 ^ Ack(2, x-1) en cualquier otro caso`
