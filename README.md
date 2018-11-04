# Traversal with Prolog


### Quick start
1) Download [GNU Prolog](http://www.gprolog.org/#download)
2) Download/Clone this repository.
3) Consult the 'transversal.pl' file.
4) Enter:

```prolog
path_to_phone(1,16,My_Path).
```

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

![map](https://github.com/jacobrozell/PrologProject/blob/master/map.PNG)
___

### API

## room()
```prolog
room(1).
room(2).
room(3).
room(4).
room(5).
room(6).
room(7).
room(8).
room(9).
room(10).
room(11).
room(12).
room(13).
room(14).
room(15).
room(16).
```
#### This creates the 16 rooms in the prolog database.
___

## door(X,Y)
```prolog
door(1,2).
door(1,7).
door(2,8).
door(3,8).
door(4,8).
door(4,9).
door(5,6).
door(5,9).
door(6,9).
door(7,8).
door(7,9).
door(7,10).
door(7,11).
door(7,12).
door(7,13).
door(7,14).
door(14,15).
door(15,16).
```
```prolog
door(7,X).
```
#### This creates the doors in the prolog database. If called (like the example above) it show which rooms connect to room 7.
___

## phoneRinging(X)
```prolog
phoneRinging(5).
phoneRinging(9).
phoneRinging(16).
```
```prolog
phoneRinging(5). 
```
#### phoneRinging will return 'yes' if a phone is ringing in that room.
___

## next_to(Room1,Room2)
```prolog
next_to(Room1, Room2) :- (door(Room1, Room2); door(Room2, Room1)).
```
```prolog
next_to(5,7).
```
#### next_to will return 'yes' if the rooms are next to each other. It uses door(X,Y) to determine this.
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
