# Scheme - Lee County Funfair


### Quick start
1) Download [GNU Prolog](http://www.gprolog.org/#download)
2) Download/Clone this repository.
3) Consult the 'transversal.pl' file.

# Table of Contents
* [Summary](#summary)
* [API](#API)

___

#### Summary
For this programming assignment, we will be writing a program in Prolog that will tell us how to get from one
room of a one-story building, to any other room in that building (if it’s possible), by telling us all of the rooms we
must go through to get to the destination room. In addition to the previous statement, there will be phones ringing in
one or more of the rooms. Our prolog program should ONLY tell us how to get to those rooms. If we attempt to go
to a room that does not have a ringing phone, the program should not produce any output.
___

### API

## ball-val
```racket
(define (ball-val color)
  (let ((ball color))
    (cond ((equal? 'W ball) 1)
          ((equal? 'R ball) 10)
          ((equal? 'G ball) 15)
          ((equal? 'B ball) 20))))
```
```scheme
(ball-val 'R)
```
#### The procedure ball-val takes a color as an argument and returns how many points that color is worth.
___

## count-balls
```racket
(define (count-balls color bucket)
  (count
   (keep (lambda (c) (equal? color c)) bucket)))
```
```scheme
(count-balls 'R '(R B G R R R B W R W))
```
#### The procedure count-balls takes a color and a bucket as an argument and returns the number of balls in the bucket with the given color.
___

## color-counts
```racket
(define (color-counts bucket)
  (let ([R (count-balls 'R bucket)]
        [G (count-balls 'G bucket)]
        [B (count-balls 'B bucket)]
        [W (count-balls 'W bucket)])
    (display (list R G W B))))
```
```scheme
(color-counts '(R B G R R R B W R W))
```
#### The procedure color-counts takes a bucket as an argument and returns a
#### sentence containing the number of reds, the number of green, the number of blues, and
#### the number of whites in the bucket.
___

## bucket-val
```
(define (bucket-val bucket)
  (let ((score 0))
    (apply + (map (lambda (c) (+ score (ball-val c))) bucket))))
```
```scheme
(bucket-val '(R B G R R R B W R W))
```
#### The procedure bucket-val takes a bucket as an argument and returns the total
#### number of points that the bucket is worth.
___

## judge
```racket
(define (judge bucket_1 bucket_2)
  (let ((score1 (bucket-val bucket_1) ))
    (let ((score2 (bucket-val bucket_2) ))
      (cond ((> score1 score2) "Bucket 1, won!")
            ((> score2 score1) "Bucket 2, won!")
            ((equal? score1 score2) "It's a tie!")))))
```
```scheme
(judge '(R B G R R R B W R W) '(W R R R R G B B G W))
```
#### The procedure judge takes two arguments bucket_1 and bucket_2 and returns
#### which player won the game.
___

#### License
Auburn University
___

## Author
Jacob Rozell
