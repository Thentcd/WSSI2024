Zadanie 1:

% A x i y są rodzeństwem
% B x i y są kuzynami
% C x i y są swatami
% D x jest przybranym dzieckiem y, y jest macochą/ojczymem x
% E x i y są przybranym rodzeństwem
% F X jest szwagrem/bratową y
% G

Zadnie 2:

% 1. kobieta(X) - X jest kobietą, jeśli X jest osobą i nie jest mężczyzną
kobieta(X) :- osoba(X), \+ mezczyzna(X).

% 2. ojciec(X, Y) - X jest ojcem Y, jeśli X jest rodzicem Y i X jest mężczyzną
ojciec(X, Y) :- rodzic(X, Y), mezczyzna(X).

% 3. matka(X, Y) - X jest matką Y, jeśli X jest rodzicem Y i X jest kobietą
matka(X, Y) :- rodzic(X, Y), kobieta(X).

% 4. corka(X, Y) - X jest córką Y, jeśli X jest dzieckiem Y i X jest kobietą
corka(X, Y) :- rodzic(Y, X), kobieta(X).

% 5. brat_rodzony(X, Y) - X jest rodzeństwem Y i X jest mężczyzną, oraz mają tych samych rodziców
brat_rodzony(X, Y) :-
mezczyzna(X),
rodzic(Z, X), rodzic(Z, Y),
X \= Y.

% 6. brat_przyrodni(X, Y) - X jest przyrodnim bratem Y, jeśli X jest mężczyzną i mają wspólnego tylko jednego rodzica
brat_przyrodni(X, Y) :-
mezczyzna(X),
rodzic(A, X), rodzic(A, Y),
\+ ( rodzic(B, X), rodzic(B, Y), A \= B),
X \= Y.

% 7. kuzyn(X, Y) - X jest kuzynem Y, jeśli ich rodzice są rodzeństwem
kuzyn(X, Y) :-
rodzic(A, X), rodzic(B, Y),
brat_rodzony(A, B);
rodzic(A, X), rodzic(B, Y),
brat_przyrodni(A, B).

% 8. dziadek_od_strony_ojca(X, Y) - X jest dziadkiem od strony ojca dla Y, jeśli X jest ojcem ojca Y
dziadek_od_strony_ojca(X, Y) :-
ojciec(X, Z), ojciec(Z, Y).

% 9. dziadek_od_strony_matki(X, Y) - X jest dziadkiem od strony matki dla Y, jeśli X jest ojcem matki Y
dziadek_od_strony_matki(X, Y) :-
ojciec(X, Z), matka(Z, Y).

% 10. dziadek(X, Y) - X jest dziadkiem Y, jeśli X jest ojcem któregoś z rodziców Y
dziadek(X, Y) :- dziadek_od_strony_ojca(X, Y);
dziadek_od_strony_matki(X, Y).

% 11. babcia(X, Y) - X jest babcią Y, jeśli X jest matką któregoś z rodziców Y
babcia(X, Y) :-
matka(X, Z), rodzic(Z, Y).

% 12. wnuczka(X, Y) - Y jest wnuczką X, jeśli Y jest córką dziecka X
wnuczka(X, Y) :-
rodzic(X, Z), corka(Y, Z).

% 13. przodek_do2pokolenia_wstecz(X, Y) - X jest przodkiem Y do drugiego pokolenia wstecz
przodek_do2pokolenia_wstecz(X, Y) :- rodzic(X, Y);
rodzic(X, Z), rodzic(Z, Y).

% 14. przodek_do3pokolenia_wstecz(X, Y) - X jest przodkiem Y do trzeciego pokolenia wstecz
przodek_do3pokolenia_wstecz(X, Y) :- przodek_do2pokolenia_wstecz(X, Y);
rodzic(X, Z), przodek_do2pokolenia_wstecz(Z, Y).
