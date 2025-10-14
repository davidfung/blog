# pseudocode blog

## SICP Exercise 3.2

001-2025-08

**Structure and Interpretation of Computer Programs**

Exercise 3.2.  In software-testing applications, it is useful to be able to count the number of times a given procedure is called during the course of a computation. Write a procedure make-monitored that takes as input a procedure, f, that itself takes one input. The result returned by make-monitored is a third procedure, say mf, that keeps track of the number of times it has been called by maintaining an internal counter. If the input to mf is the special symbol how-many-calls?, then mf returns the value of the counter. If the input is the special symbol reset-count, then mf resets the counter to zero. For any other input, mf returns the result of calling f on that input and increments the counter. For instance, we could make a monitored version of the sqrt procedure:

    (define s (make-monitored sqrt))

    (s 100)
    10

    (s 'how-many-calls?)
    1

***Implementation***

    #lang racket

    (define (make-monitored f)
      (define count 0)
      (define (mf a)
        (cond [(eq? a 'how-many-calls?) count]
              [(eq? a 'reset-count) (set! count 0)]
              [else (set! count (+ count 1))
                    (f a)]
        )
      )
      mf
    )

***Test***

    (define s (make-monitored sqrt))
    (s 144)                 ; 12
    (s 121)                 ; 11
    (s 'how-many-calls?)    ; 2
    (s 'reset-count)        
    (s 9)                   ; 3
    (s 'how-many-calls?)    ; 1

***Epilogue***

This is my attempt on SICP Exercise 3.2 in the programming language Racket.  I am impressed that the Scheme code in the book still runs unchanged several decades later in Racket. 
