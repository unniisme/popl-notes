
# Simply typed Lambda calculus
<pre>
types:
    t = bool 
    | t1 -> t2

terms:
    term = x        (VAR)
    |   e1 e2       (APP)
    |   λx:t.e      (ABS)
        # problem here is e might not be well typed
</pre>

<pre>
Judgements:
e:t => e is well typed and has type t

Γ ⊢ e:t  (e has type t in contex of Γ)
Γ = { x1:t1, x2:t2 ... xn:tn}

⊢ e:t is same as ϕ ⊢ e:t

some notations
1. x:t' ∉ Γ
2. Γ, x:t = Γ ∪ {x.t}

Inference:
J1
J2
J3
----
J


Inference ruls:
VAR:

----
{x:t} ⊢ x:t


APP:
Γ ⊢ e1:t' -> t
Γ ⊢ e2:t'
----
Γ ⊢ e1 e2 : t


ABS:
Γ, {x:t1} ⊢ e:t2
----
Γ ⊢ λx:t1.e : t1->t2


Weakening:
Γ ⊢ e:t
----
Γ,x.t ⊢ e:t

Contraction:
Γ ∪ {x:t1} ∪ {x:t1} ⊢ e:t
----
Γ ∪ {x:t1} ⊢ e:t
</pre>

Expession is **closed** if it has no free variables \
A **proof** is a finite sequence of judgements

<pre>
Eg:
Q. type of λ(x:bool).x
1) {x:bool} ⊢ x:bool (VAR)
2) ⊢ λ(x:bool).x : bool -> bool   (ABS)


Eg:
Q. type of λ(x:bool)(y:int).x
1) {x:bool} ⊢ x:bool (VAR)
2) {x:bool},{y:int} ⊢ x:bool  (Weakening)
3) {x:bool} ⊢ λy:int.x : int -> bool
4) ⊢ λ(x:bool)(y:int).x : bool -> int -> bool
</pre>

We say e is **well typed** in context of Γ if Γ ⊢ e:t can be proven for some type t. \
For a closed term e we say e is well typed if ⊢ e.t can be proven.\


----
### STLC problems:
1. Type checking problem \
Given a context Γ, an expression e and a type t, check if Γ ⊢ e:t can  be derived using inference rules.
2. Type inference problem \
Given a context Γ, and an expression e, find a type t (if possible) such that Γ ⊢ e:t is derivable.
----

### Extended STLC:
<pre>
types
    t = Basic Types
    | t1 -> t2
    | t1*t2

e   = x             (VAR)
    | e1 e2         (APP)
    | λx:t.e        (ABS)
    | pair (e1,e2)  (PAIR)
    | fst e         (INDEX 1)
    | lst e         (INDEX 2)
</pre>

Added Inference rules:
<pre>
PAIR
Γ ⊢ e1 : t1
Γ ⊢ e2 : t2
----
Γ ⊢ pair (e1,e2) : t1*t2

INDEX 1
Γ ⊢ e : t1*t2
----
Γ ⊢ fst e : t1

INDEX 2
Γ ⊢ e : t1*t2
----
Γ ⊢ lst e : t2
</pre>
