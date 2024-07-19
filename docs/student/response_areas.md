# Response Areas

## Numerical answers
![A numerical answer box](images/number_box.png)

This type of response area expects a numerical answer. Usually, a tolerance is allowed, so you will still be marked as correct
if your response differs from the answer by a small amount. 

![A numerical answer box, with units](images/number_units.png)

Some questions will also require you to enter the units of the answer. In this case, any form of the same unit, with any SI prefix,
should be accepted. For example, if the answer to a question is `10 MPa`, `0.01 GPa` and `10 MNm^-2` should both be marked correct. 


## Entering mathematical expressions
Entering mathematical expressions on Lambda is very similar to if you were doing it in Matlab, for example. 

### Examples
|              Expression              | Lambda Feedback input|
|--------------------------------------|----------------------|
|$x^2 - x - 2$                         |`x^2 - x - 2`         |
|$\sqrt{\sin(x) + \frac{\pi}{2}}$      |`sqrt(sin(x) + pi/2)` |
|$e^{\frac{\pi x}{2} + 1}              |`exp((pi*x)/2 + 1)`   |

### Reference
| Operator       | Symbol        | Lambda Feedback input |
|----------------|---------------|-----------------------|
| Addition       | $a + b$       | a+b                   |
| Subtraction    | $a - b$       | a-b                   |
| Multiplication | $a \times b$  | a*b                   |
| Division       | $\frac{a}{b}$ | a/b                   |
| Exponentiation | $a^b$         | a^b                   |
| Square root    | $\sqrt{a}$    | sqrt(a)               |
|                |               |                       |

Common elementary functions such as $\sin$, $\cos$, $\arcsin$, $\ln$ etc. are also supported.
