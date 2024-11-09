### Detailed Notes on Matrix Chain Multiplication (MCM) with Dynamic Programming

- Reference: [youtube](https://youtu.be/prx1psByp7U?si=qlhrkFD0ikqceJXv)
---

#### Overview of Matrix Chain Multiplication Problem:
1. **Matrix Multiplication Basics**:
   - Given two matrices A (m × n) and B (n × p), they can be multiplied if the number of columns in A equals the number of rows in B.
   - The resulting matrix C has dimensions (m × p).
   - **Cost of Multiplication**: The cost (number of scalar multiplications) to compute C = AB is `m * n * p`.

2. **Matrix Chain Multiplication Problem**:
   - When multiplying more than two matrices, the order in which the matrices are multiplied affects the computation cost.
   - **Objective**: Determine the optimal parenthesis order for multiplication that minimizes the total number of scalar multiplications.

3. **Example Problem**:
   - Suppose we have matrices with dimensions:
     - A1 (5 × 4), A2 (4 × 6), A3 (6 × 2), and A4 (2 × 7).
   - Multiplying them in various orders leads to different computation costs.
   - **Goal**: Find the parenthesis pattern that yields the minimum multiplication cost.

---

#### Solution Approach Using Dynamic Programming (DP):
1. **Dynamic Programming (DP) Approach**:
   - Uses a table to store results of subproblems and solve the main problem by combining these results.
   - Follows a **bottom-up approach** by first solving smaller subproblems and building up to the main problem.

2. **Table Setup**:
   - Use two tables:
     - **M Table**: Stores the minimum multiplication costs for subproblems.
     - **S Table**: Stores split points to record where the optimal split occurs for each subproblem.
   - Dimensions of these tables are based on the number of matrices.

3. **Base Case**:
   - Single matrices have no multiplication cost, so the diagonal of the M table is filled with 0.

4. **Recursive Formula for Filling the Table**:
   - For each subproblem `M[i][j]` (minimum cost to multiply matrices from A_i to A_j):
     \[
     M[i][j] = \min_{i \leq k < j} \{ M[i][k] + M[k+1][j] + d_{i-1} \cdot d_k \cdot d_j \}
     \]
   - Here, \( d_{i-1} \cdot d_k \cdot d_j \) is the cost of multiplying the resulting matrices from partitions i to k and k+1 to j.

5. **Procedure**:
   - Compute costs for chains of increasing lengths.
   - Use results from previously computed subchains to find optimal costs for longer chains.
   - Store the minimum values in the M table and the corresponding split points in the S table.

---

#### Detailed Example with Dynamic Programming Table:
1. **Table Filling**:
   - Start with pairs of matrices, compute costs, and store in M table.
   - Progressively compute costs for three matrices, then four, and so on.
   - Example:
     - `M[1][2]`: Cost to multiply A1 and A2.
     - `M[2][3]`: Cost to multiply A2 and A3.
     - Continue until the entire range is covered.

2. **Optimal Parenthesization**:
   - Using the S table, reconstruct the optimal multiplication order from the computed split points.

3. **Final Result**:
   - The minimum cost for the complete multiplication (A1 × A2 × A3 × A4) is found at `M[1][n]`, where n is the total number of matrices.

---

#### Complexity Analysis:
1. **Time Complexity**:
   - Filling the DP table requires O(n³) time, where n is the number of matrices, due to nested loops and checking all possible splits for each subproblem.
2. **Space Complexity**:
   - Requires O(n²) space to store the M and S tables.

---

#### Steps to Implement the DP Solution:
1. Define dimensions of matrices as an array, e.g., `dimensions = [5, 4, 6, 2, 7]`.
2. Initialize M and S tables with dimensions based on the number of matrices.
3. Use the recursive formula to populate the M and S tables.
4. Retrieve the minimum multiplication cost from `M[1][n]`.
5. Use the S table to find the optimal multiplication order.

---

#### Conclusion:
- Matrix Chain Multiplication optimally minimizes the cost of scalar multiplications through dynamic programming.
- **Applications**: Useful in fields requiring heavy matrix computations like computer graphics, scientific computing, and machine learning.