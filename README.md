# A Traveling Salesman Problem solved with Simplex method

This is an assignment for a Operations Research class at Federal University of Alagoas (UFAL) requested by professor Roberta Lopes and performed by the students: Vanessa Vieira, Rubem Ferreira and André Santana.

# The problem
Imagine a traveling salesman that needs to travel from one city to another in the quickest way possible. This is a graph with all the cities and the distances:

[![texto alt](http://www.phpsimplex.com/pt/img/problema6.png)](urldolink)

Imagine that he needs to go from A to G. What we need to do to solve this is determine the decision variables and express them algebraically. In this case:

Xij: action of moving from city i to city j (0 indicates that there is no displacement and 1 that there is displacement).

Determine the constraints and express them as equations or inequalities dependent on the decision variables. Such restrictions are deduced from the balance between the possible routes that depart from each city and the roads that reach it (ignoring the roads that return us to the point of departure and those that come from the destination):

- Balance of city roads for A: XAB + XAC = 1
- Balance of city roads for B: XBD + XBE - XAB - XDB - XEB = 0
- Balance of city roads for C: XCD + XCF - XAC - XDC - XFC = 0
- Balance of city roads for D: XDB + XDC + XDE - XBD - XCD - XED = 0
- Balance of city roads for E: XEB + XED + XEG - XBE - XDE = 0
- Balance of city roads for F: XFC + XFG - XCF = 0
- Balance of city roads for G: - XEG - XFG = -1

Express all the conditions implicitly established by the nature of the variables: that they can not be negative, that they are integers and that can only have certain values. In this case, the constraints are, that the variables must be Boolean (0 should not be taken the path, 1 use the path), and therefore can not be negative:

- Xij ≥ 0;
- Xij are booleans.

Determine the objective function:
- Minimize Z = 12 XAB + 4 XAC + 5 XBD + 3 XBE + 2 XCD + 10 XCF + 5 XDB + 2 XDC + 10 XDE + 3 XEB + 10 XED + 2 XEG + 10 XFC + 4 XFG

Given that:

- 1 X1 + 1 X2 + 0 X3 + 0 X4 + 0 X5 + 0 X6 + 0 X7 + 0 X8 + 0 X9 + 0 X10 + 0 X11 + 0 X12 + 0 X13 + 0 X14 = 1
- -1 X1 + 0 X2 + 1 X3 + 1 X4 -1 X5 -1 X6 + 0 X7 + 0 X8 + 0 X9 + 0 X10 + 0 X11 + 0 X12 + 0 X13 + 0 X14 = 0
- 0 X1 -1 X2 + 0 X3 + 0 X4 + 0 X5 + 0 X6 + 1 X7 + 1 X8 -1 X9 -1 X10 + 0 X11 + 0 X12 + 0 X13 + 0 X14 = 0
- 0 X1 + 0 X2 + 0 X3 -1 X4 + 1 X5 + 0 X6 -1 X7 + 0 X8 + 0 X9 + 1 X10 + 1 X11 -1 X12 + 0 X13 + 0 X14 = 0
- 0 X1 + 0 X2 -1 X3 + 0 X4 + 0 X5 + 1 X6 + 0 X7 + 0 X8 + 0 X9 + 0 X10 -1 X11 + 1 X12 + 1 X13 + 0 X14 = 0
- 0 X1 + 0 X2 + 0 X3 + 0 X4 + 0 X5 + 0 X6 + 0 X7 -1 X8 + 1 X9 + 0 X10 + 0 X11 + 0 X12 + 0 X13 + 1 X14 = 0
- 0 X1 + 0 X2 + 0 X3 + 0 X4 + 0 X5 + 0 X6 + 0 X7 + 0 X8 + 0 X9 + 0 X10 + 0 X11 + 0 X12 -1 X13 -1 X14 = -1

Make a change of variables with the following match:

| Roads | After Change |
---------|-------------|
|    XAB | X1          |
|    XAC | X2          |
|    XBE | X3          |
|    XBD | X4          |
|    XDB | X5          |
|    XEB | X6          |
|    XCD | X7          |
|    XCF | X8          |
|    XFC | X9          |
|    XDC | X10         |
|    XDE | X11         |
|    XED | X12         |
|    XEG | X13         |
|    XFG | X14         |


  After this, we apply the Simplex method using the SciPy Library and get the following results:
  ```sh
  Shortest path = 16
  ```
|  Roads | Used or not|
---------|------------
|    X1 | 0           |
|    X2 | 1           |
|    X3 | 1           |
|    X4 | 0           |
|    X5 | 1           |
|    X6 | 0           |
|    X7 | 1           |
|    X8 | 0           |
|    X9 | 0           |
|    X10 | 0          |
|    X11 | 0          |
|    X12 | 0          |
|    X13 | 1          |
|    X14 | 0          |

Output:
```sh
fun: 16.0
message: 'Optimization terminated successfully.'
nit: 10
slack: array([], dtype=float64)
status: 0
success: True
x: array([0., 1., 1., 0., 1., 0., 1., 0., 0., 0., 0., 0., 1., 0.])
```
