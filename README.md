# bool-notes
> 
> - `&` will stand for `AND`
> - `|` will stand for `OR`
> - `!` will stand for `NOT`
>
> ### DNF Example
> `(A & B) | (C & D & E) | F`
>
> ### CNF Example
>`(A | B) & (C | D | E) & F`
>
>
> A solution will stand for any subsitution of variables (to 1s or 0s) that results in the general equation being a tautology
>

## CNF to DNF
Converting `(A | B) & (C | D | E) & F` to DNF
Concept1: split up and foil, then repeat

1. Split up : `((A | B) & (C | D | E)) & F`
2. Foil : `(((A | B) & C) | ((A | B) & D) | ((A | B) & E))) & F`
2. Foil : `((A & C) | (B & C) | (A & D) | (B & D) | (A & E) | (B & E)) | F`
4. Foil : `(A & C & F) | (B & C & F) | (A & D & F) | (B & D & F) | (A & E & F) | (B & E & F)`

Vice versa works with DNF to CNF.

## DNF note

DNF form is a concise representation of every single possible "solution" to a boolean equation.

## DNF atoms

Ways of operating on DNFs, while keeping them as DNFs

1. `DNF1` => stays DNF
2. `DNF1 | DNF2` => stays DNF
3. `DNF1 & DNF2` => foil
> ```
> DNF1 = (A & B) | (A & C & D)
> DNF2 = (E & F) | (G & H & I) | K
> [(A & B) | (A & C & D)]
> == (A & B & [(E & F) | (G & H & I) | K]) | (A & C & D & [(E & F) | (G & H & I) | K])
> == (A & B & E & F) | (A & B & G & H & I) | (A & B & K) | (A & C & D & E & F) | (A & C & D & G & H & I) | (A & C & D & K)
> Resulting DNF
> (A & B & E & F) | (A & B & G & H & I) | (A & B & K) | (A & C & D & E & F) | (A & C & D & G & H & I) | (A & C & D & K)
> ```
4. `!DNF1` => de morgans then foil (CNF to DNF)
> ```
> DNF1 = (A & B) | (A & C & D)
> ![(A & B) | (A & C & D)]
> == (!A | !B) & (!A | !C | !D) ;; Demorgans
> ==    .   .   .
> == (!A & !A) | (!A & !C)| (!A & !D) | (!B & !A) | (!B & !C) | (!B & !D)
> Resulting DNF
> (!A & !A) | (!A & !C)| (!A & !D) | (!B & !A) | (!B & !C)| (!B & !D)
> ```


`&` and `!` take polynomial time, while `|` takes O(1)

To get all possible solutions, this may be the fastest we can get. Sometimes not every solution is required
<!--
## Suggested "Hollow DNF" (hDNF) form

Instead of storing all the conjuctions (bound together by disjunctions) in DNF form, another approach may be to only store the first value of each conjuction, along with all the elements of the first conjuction. With only this information stored, every solution to a boolean equation will not be calculatable, although it will be a lot easier to find one sole solution.

> ### DNF vs hDNF Example
> DNF : (E & F) | (G & H & I) | K
> hDNF : {(E & F), G, K}

## hDNF atoms

Ways of operating on hDNFs, while keeping them as hDNFs

1. `hDNF1` => stays hDNF
2. `hDNF1 | hDNF2` => concat fronts
> ```
> hDNF1 = {(A & B), A}
> hDNF2 = {(E & F), G, K}
> Resulting hDNF
>   {(A & B), A, E, G, K}
3. `hDNF1 & hDNF2` => combine top, concat fronts
> ```
> hDNF1 = {(A & B), A}
> hDNF2 = {(E & F), G, K}
> Resulting hDNF
>   {(A & B & E & F), A, G, K}
> ```
4. `!DNF1` => de morgans then foil (CNF to DNF)
> ```
> DNF1 = (A & B) | (A & C & D)
> ![(A & B) | (A & C & D)]
> == (!A | !B) & (!A | !C | !D) ;; Demorgans
> ==    .   .   .
> == (!A & !A) | (!A & !C)| (!A & !D) | (!B & !A) | (!B & !C) | (!B & !D)
> Resulting DNF
> (!A & !A) | (!A & !C)| (!A & !D) | (!B & !A) | (!B & !C)| (!B & !D)
> ```

-->
