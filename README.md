# Traversal with Prolog


### Quick start
1) Download [GNU Prolog](http://www.gprolog.org/#download)
2) Download/Clone this repository.
3) Consult the 'transversal.pl' file.
4) Enter:

```prolog
path_to_phone(1,16).
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

## room(X)
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

## path_to_phone(Start, End)
```prolog
%---Given start and destination---%
path_to_phone(Start, End):-nonvar(Start), nonvar(End),
	phoneRinging(End),
	get_paths(Start, End),
	fail.


%---Given start only---%
path_to_phone(Start, End):-nonvar(Start), var(End),
	forall(phoneRinging(E), (get_paths(Start, E))),
	fail.


%---Given destination only---%
path_to_phone(Start,End):-var(Start), nonvar(End),
	phoneRinging(End),
	forall(room(E), (get_paths(E, End))),
	fail.


%---Given nothing---%
path_to_phone(Start, End):-var(Start), var(End),
	forall(phoneRinging(PH), forall(room(Room), (get_paths(Room, PH)))),
	fail.
```
```prolog
path_to_phone(1, 16). % Both
path_to_phone(1, End). % Start only
path_to_phone(Start, 16). % End only
path_to_phone(Start, End). % Nothing
```
#### path_to_phone has four procedures, one where the start and end are given, one where only the start is given, one where 
#### only the end is given, and one where nothing is given.
___

## get_paths(Start, End)
```prolog
get_paths(Start, End):-nonvar(Start), nonvar(End),
	forall(find_path(Start, End, R), nl).
```
#### get_paths uses find_path to find all the paths available from the Start to the End.
___

## find_path(Start, End, T)
```prolog
find_path(Start, Dest, T):-nonvar(Start), nonvar(Dest), var(T),
	T = [],
	move_forward(Start, Dest, T, R),
	move_backward(R, Route, []),
	write(Route).
```
#### find_path uses move_forward and move_backward to find a path.
___

## move_forward(Start, End, T, R)
```prolog
% Used when Starting room and ending room are the same
move_forward(Start,Start,T,[Start|T]). 	

move_forward(Start,End,T,R):-
   next_to(Start,Next),
	\+(member(Next,T)), 
	move_forward(Next,End,[Start|T],R).
```
#### move_forward will move forward if there is a room next_to it that can be moved to.
___


## move_backward([H|T],Z,Acc)
```prolog
move_backward([],Z,Z).
move_backward([H|T],Z,Acc) :-move_backward(T,Z,[H|Acc]).
```
#### move_backward will reverse backwards a room.
___

#### License
Auburn University
___

## Author
Jacob Rozell
