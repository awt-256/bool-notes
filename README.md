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

## CNF to DNF
Converting `(A | B) & (C | D | E) & F` to DNF
Concept1: split up and foil, then repeat

1. Split up : `((A | B) & (C | D | E)) & F`
2. Foil : `(((A | B) & C) | ((A | B) & D) | ((A | B) & E))) & F`
2. Foil : `((A & C) | (B & C) | (A & D) | (B & D) | (A & E) | (B & E)) | F`
4. Foil : `(A & C & F) | (B & C & F) | (A & D & F) | (B & D & F) | (A & E & F) | (B & E & F)`

Vice versa works with DNF to CNF.

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
> == (!A & !A) | (!A & !C)| (!A & !D) | (!B & !A) | (!B & !C)| (!B & !D)
> Resulting DNF
> (!A & !A) | (!A & !C)| (!A & !D) | (!B & !A) | (!B & !C)| (!B & !D)
> ```


`&` and `!` take polynomial time, while `|` takes O(1)
