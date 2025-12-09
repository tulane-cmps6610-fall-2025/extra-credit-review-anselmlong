# CMPS 6610 Extra Credit Answers
  
In this extra credit assignment, we will test and review concepts you
   have learned since the midterm exam. Please add your written answers
   to `answers.md` which you can convert to a PDF using
   `convert.sh`. Alternatively, you may scan and upload written
   answers to a file named `answers.pdf`.



1. **Algorithmic Paradigms**

My favourite paradigm is Divide and Conquer because it breaks down a problem into smaller subproblems, solves each subproblem independently, and then combines the results to solve the original problem. This approach is efficient for many problems, such as sorting algorithms like Merge Sort and Quick Sort, as well as searching algorithms like Binary Search. The recursive nature of Divide and Conquer allows for elegant solutions and often leads to improved time complexity compared to iterative approaches.

2. **Divide and Conquer**

No. If we go into the definitions, we can see why not all divide and conquer algorithms have optimal substructure.
- **Divide and Conquer**: A problem-solving approach that breaks a problem into smaller subproblems, solves them recursively, and combines the results.
- **Optimal Substructure**: A problem has optimal substructure if an optimal solution to the problem contains optimal solutions to its subproblems.

However, one counterexample is Binary Search.

*Problem*: Find if a target element exists in a sorted array.

*Divide and Conquer Nature*: 
- Binary search divides the array in half
- Recursively searches the appropriate half  
Returns true if found, false otherwise

*Lacks Optimal Substructure*: 
- Binary search doesn't optimize anything - it's a decision problem (exists/doesn't exist)
- There's no notion of "optimal solution" to subproblems
- Each recursive call is a different problem (searching different subarrays), not a subproblem contributing to an overall optimization

Hence, while binary search is a divide and conquer algorithm, it does not exhibit optimal substructure.

3. **Randomization**

- 3a.

To find this probability, we apply Markov's inequality with:
- $X$ = number of comparisons made by Quicksort
- $E[X] = O(n \log n)$ (expected work)
- We want $P[X \geq cn^2]$ for some constant $c > 0$

Using Markov's inequality:
$$P[X \geq cn^2] \leq \frac{E[X]}{cn^2}$$

Since $E[X] = O(n \log n)$, we can write $E[X] \leq k \cdot n \log n$ for some constant $k$.

Therefore:
$$P[X \geq cn^2] \leq \frac{k \cdot n \log n}{cn^2} = \frac{k \log n}{cn}$$

For large n, specifically as $n \to \infty$, we have $\frac{\log n}{n} \to 0$.

The probability that Quicksort does $\Omega(n^2)$ comparisons is at most $O(\frac{\log n}{n})$, which approaches 0 as $n$ increases. This shows that the probability of worst-case behavior becomes negligible for large inputs.
Hence, Quicksort is efficient and used widely.

- 3b.
What is the probability that Quicksort does $10^c n \ln n$
comparisons, for a given $c>0$? What does this say about the
"concentration" of the expected work for Quicksort?
 
Using Markov's Inequality again, we set:
- $X$ = number of comparisons made by Quicksort
- $E[X] = O(n \log n)$ (expected work)
- We want $P[X \geq 10^c n \ln n]$

Then,
$$P[X \geq 10^c n \ln n] \leq \frac{E[X]}{10^c n \ln n}$$

If we assume $E[X] \leq k \cdot n \log n$ for some constant $k$, we have:
$$P[X \geq 10^c n \ln n] \leq \frac{k \cdot n \log n}{10^c n \ln n} = \frac{k}{10^c}$$
This means that as c increases, the probability that Quicksort exceeds $10^c n \ln n$ comparisons decreases exponentially. This indicates a strong concentration of the expected work around its mean, suggesting that Quicksort is very likely to perform close to its expected time complexity of $O(n \log n)$ for large inputs.

4. **Greedy Algorithms**

**Theorem**: Scheduling jobs in order of their processing times (shortest-job-first) minimizes the average waiting time.

Let's consider any optimal schedule $S^*$.

We have $n$ jobs $j_1, j_2, \cdots, j_n$ with processing times $p_1, p_2, \cdots, p_n$.

Let $W_i$ denote the waiting time of job $j_i$ in schedule $S$. Then, let's define total waiting time as $\sum_{i=1}^n W_i$ and average waiting time as $\frac{1}{n}\sum_{i=1}^n W_i$

For a job $j_i$ which is scheduled in schedule $S$, we can say that $W_i$ is the sum of all the processing times of the jobs before position k.

Suppose there exists an optimal schedule $S^*$ where some job $j_i$ with processing time $p_i$ appears before job $j_j$ with processing time $p_j$, where $p_i > p_j$. In other words, the longer processing time appears before a shorter one.

Consider swapping these two adjacent jobs to create schedule $S'$:
- Jobs before position of $j_i$: waiting times unchanged
- Job $j_j$ (now in earlier position): waiting time decreases by $p_i - p_j > 0$  
- Job $j_i$ (now in later position): waiting time increases by $p_j$
- Jobs after position of $j_j$: waiting times unchanged

**Net change in total waiting time**:
$$\Delta = (p_j) - (p_i - p_j) = 2p_j - p_i < 0$$

Since $p_i > p_j$, we have $\Delta < 0$, meaning the total waiting time decreases.

This contradicts the assumption that $S^*$ was optimal.

Hence, jobs must be ordered in non-decreasing order of processing times.

5. **Dynamic Programming**

For maximum span, the DAG is just one linear chain. An example is a DP problem with strict linear dependency, such as computing the nth Fibonacci number using the naive recursive approach. The recurrence relation is:
F(n) = F(n-1) + F(n-2)
Here, each computation depends on the previous two computations, leading to a linear chain of dependencies.

The smaller the longest path of the DAG is, the more parallelizable it is. A polylogarithmic span can be achieved for problems like binary tree computations, such as computing the height of a balanced binary tree. The recurrence relation is:
H(n) = 1 + max(H(left_subtree), H(right_subtree))
Here, the height of the tree can be computed in parallel for the left and right subtrees, leading to a span of O(log n) for a balanced binary tree.

6. **Graphs**

To prove that the heaviest edge in any cycle can't be in an MST.

Assume an MST contains the heaviest edge $e$ from some cycle. Since it's a cycle, there's another path connecting the same two vertices without using $e$. 

Then, we can remove $e$ and add any lighter edge from that alternative path. This gives us a new spanning tree with smaller total weight, which contradicts our assumption that the original was minimum.

Hence, the heaviest edge in any cycle can never be part of an MST - you can always do better by using a lighter alternative from the same cycle.
