# Question 1: Mutations

In a genetic algorithm with 10 chromosomes, each 20 genes long, and a mutation rate of 0.01 (per gene), how many gene mutations are expected per generation?

---

$$
\begin{aligned}
\mathbb{E}(\text{mutations}) &= \text{number of chromosomes} \times \text{genes per chromosome} \times \text{mutation rate} \\
&= 10 \times 20 \times 0.01 = 2
\end{aligned}
$$

# Question 2: Offspring fitness

Suppose a genetic algorithm encodes solutions as 4-bit chromosomes, and the fitness function is

\[
f(b_1 b_2 b_3 b_4) = b_1 + 2 b_2 + 4 b_3 + 8 b_4 \quad (b_i \in {0,1})
\]

Given parent chromosomes

* (A = 1100)
* (B = 0011)

After single-point crossover between the second and third bits, what is the fitness of the offspring?

---
Children after crossover:
- Child 1: 11|11 = 1111
- Child 2: 00|00 = 0000

Fitness of Child 1:
\[
f(1111) = 1 + 2 + 4 + 8 = 15
\]
Fitness of Child 2:
\[
f(0000) = 0 + 0 + 0 + 0 = 0
\]

# Question 3: Tabu search

Given a small optimisation problem:

\[
\text{Minimise } f(x) = x^2 - 4x + 4
\]

where (x) can take integer values between −10 and 10.

Perform one iteration of the Tabu Search algorithm starting from (x = 0).

Assume two neighbours, consisting of (x = -1) and (x = 1).

What is the new value of (x) after the first iteration?

---

Tabu list: initially empty.
Neighbours of (x = 0):
- (x = -1): f(-1) = (-1)^2 - 4(-1) + 4 = 9
- (x = 1): f(1) = (1)^2 - 4(1) + 4 = 1
- Choose (x = 1) as it has the lowest value.
- Update Tabu list: add (x = 0) to the Tabu list.
- New value of after the first iteration: (x = 1)

下面是题目 **完整转换为 Markdown 格式**：

---

# Question 4: Genetic operators

Consider two chromosomes in a genetic algorithm where symbol “(|)” marks the crossover point.
The fitness function is defined as the number of ‘1’ in a chromosome.

* Chromosome 1: **1100 | 1010**
* Chromosome 2: **1010 | 1011**

---

## Questions:

* What are the fitness values of the original chromosomes?

* What would be the two offspring or children after the crossover?

* What are the fitness scores of both offspring?

* Perform bit flip mutations at positions **2** and **5** on both offspring
  (0-based index from left to right).
  What are the new offspring?

* An offspring is considered fit if its fitness score > 5.
  How many of the offspring after mutation are fit?
---
- Fitness of Chromosome 1: 4 (four '1's). Fitness of Chromosome 2: 5 (five '1's).
- Offspring after crossover:
  - Child 1: 1100 | 1011 = 11001011
  - Child 2: 1010 | 1010 = 10101010
- Fitness of Child 1: 5 (five '1's). Fitness of Child 2: 4 (four '1's).
- After bit flip mutations:
  - Child 1: 11101111 (flip at positions 2 and 5)
  - Child 2: 10001110 (flip at positions 2 and 5)
- Child 1 fitness: 7 (fit). Child 2 fitness: 4 (not fit). 1 offspring is fit.
---

# **Question 5: Genetic algorithm**

A genetic algorithm is applied to optimise a binary chromosome problem.
The initial population consists of the following chromosomes:

* **Parent 1:** `1101001011`
* **Parent 2:** `1010110101`

The algorithm proceeds with the following steps in sequence:

---

### **1. Perform single-point crossover**

Perform single-point crossover at the **4th position** (zero-based indexing)
between Parent 1 and Parent 2.

---
Offspring 1: `1101|110101` = `1101110101`
Offspring 2: `1010|001011` = `1010001011`


### **2. Apply mutation**

Apply mutation to **Offspring 1** by flipping the bits at positions **2**, **6**, and **9** (zero-based indexing).
---
Mutated Offspring 1:
- Original: `1101110101`
- After flipping position 2 and 6 and 9: `1111111100`

### **3. Compute the fitness function for Offspring 1 after mutation**

The fitness function is defined as:

\[
\text{Fitness} = \sum_{i=0}^{n-1} b_i \cdot 2^{,n-1-i}
\]

Where:

* ( $b_i$ ) is the bit value (0 or 1) at position ( i )
* ( $n$ ) is the total number of bits in the chromosome

---

### **Question**

After performing these operations, what is the **fitness value of the final mutated chromosome**?


