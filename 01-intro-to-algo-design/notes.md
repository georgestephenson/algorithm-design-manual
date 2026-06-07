# Introduction to Algorithm Design

- First take-home lesson: algorithms produce correct results whereas heuristics are often do a decent job but have no guarantee of correctness
    - Algorithm can be correct but it could also be very slow. For a given problem there may be faster algorithms or there may not. For example an exhaustive search is usually correct but extremely slow
    - Heuristics can be easy to find but with very suboptimal solutions

Reasonable-looking algorithms can easily be incorrect. Algorithms require careful exposition to show correctness and *not incorrectness*.

## Proofs

1. Clear statement of what you're trying to prove
2. Set of assumptions that are taken to be true
3. Chain of reasoning taking you from the assumptions to the statement to be proven
4. Finishing with a tombstone symbol ∎ or QED at the bottom ("thus it is demonstrated")

## Problems and properties

- Need to be careful about specifying a problem that is not too open-ended or it's easy to find an algorithm that solves some interpretation of the problem

## Demonstrating incorrectness

- The best way to disprove the correctness of a heuristic is with a counterexample

## Induction and Recursion

- Recursion in programming is mathematical induction in action
- Proof by induction is usually the right way to verify recursive or incremental insertion algorithms are correct
- Proof by induction can be subtlety incorrect.
    - Boundary errors, if our base case is $y = 0$ and we have assumed the algorithm works correctly for $y = n - 1$, then the case $y = n$ must really work for every other $n$, including the boundaries such as $y = 1$, or else it's a special case and we need to define that case explicitly. 
    - Extension claims - adding one item to a set can change the optimal solution so that none of the items in the previous solution set are in the new solution.

## Modelling the Problem

There is an art to applying the right abstract data structures to your concrete problem

"Hitchhiker's Guide" in Part II defines many common problem sets and algorithms, we want to model problems using these as much as possible

## Recursive objects

Many of the combinatorial objects (permutations, graphs, trees, strings, polygons), are also recursive objects

Meaning they can be decomposed into smaller objects which are still the same type of object.



## Proof by contradiction

- Assume a hypothesis is false, then show that a consequence of this assumption is demonstrably false, so the hypothesis must be true
- Classic example is Euclid's proof that there are infinite primes.
    - Assume there are finite primes
    - Find the integer $N$ which is the product of all the primes
    - $N + 1$ is not divisibly by any of the primes, so itself must be prime
    - So primes cannot be finite