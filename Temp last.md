## Max sub array problem
Brute force: O(n^2)
Using divide and conquer:
O(n log n)

## Multiplication Algorithm
Grade school algo.
O(n^2)

Divide and Conquer:
O(n^2)

Karatsuba’s Multiplication Algorithm
O(n^1.54)
log of 3 to the base 2 = 1.54

## Solving Recurrences
Expansion method:
Master Method:
![[Screenshot (442).png]]

## Fast Fourier Transform
Naive: O(n^2)
Using divide and conquer: O(n log n)
Inverse Fourier Transform: O(n log n)
Applications:
1. Multiplying two polynomials: Naive O(n^2). Optimal O(n log n)
2. Data Analysis (Signal Processing): 

## Prefix Codes
After compression it was difficult to decompress it because the string could be decoded in multiple ways.

Prefix codes are used during decompression so that there is only one way to read back the characters.

No code word should be a proper prefix of another code word. Thus when decoding it, it will uniquely give us back the original string.

Prefix codes can be written as trees.
![[Screenshot (446).png]]

To calculate an optimal prefix tree:
We use Huffman codes.

## Huffman Codes
Obtained through greedy algorithm. 
![[Screenshot (447).png]]
![[Screenshot (448).png]]
![[Screenshot (452).png]]

## Decision Problems and Languages
Decision Problems are those whose answer is either yes or no.

Most problems have a nice decision version.
![[Screenshot (453).png]]

Why are decision problems nicer to study ?
- The size of the answer is just 1 bit.
- We can make a connection between problems and languages.
## Polynomial Time Problems
Problems which can be solved in polynomial time.

NP(Non deterministic polynomial): which cannot be solved in polynomial time. If the answer of these problems is found then it can be verified easily that is in polynomial time.

Every problem in polynomial time belongs in NP.

