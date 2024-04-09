[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```



Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Asymtotic Analysis
Runtime Recurrance Relation: T(n) = 3T(n/3) + n^5 + C
The mystery function calls itself three times with an input of n/3, so that contributes the 3T(n/3), the inner-most loop ierates n^2 times, in a loop iterating n times, in a loop iterating n^2 times; so that contribues (n^2)(n)(n^2) = n^5. Finally C accounts the the constant amount of work done in each iteration.

$T(n) = 1$    {where n $\le$ 1}

$T(n) = 3T(n/3) + n^5 + C$    {where n > 1}


$= 3(3T(\frac{n}{9}) + (\frac{n}{3})^5 + C) + n^5 + C$    {Substitute in T(n)}

$= 9T(\frac{n}{9}) + 3(\frac{n}{3})^5 + n^5 + 3C + C$

$= 3(9T(\frac{n}{27}) + 3(\frac{n}{9})^5 + (\frac{n}{3})^5 + 3C) + n^5 + C$    {Substitute in T(n) again}

$= 27T(\frac{n}{27}) + 9(\frac{n^5}{3}) + 3n^5 + 3n^5 + C$

$= 3^iT(\frac{n}{3^i}) +$ $$\sum_{n=1}^{10} n^2$$ $+$ $$\sum_{n=1}^{10} n^2$$    {where i = $\log(n)$}



$= nT(1) + n^5\log(n) = n + n^5\log(n)$

Thus the complexity is $O(n^5\log(n))$