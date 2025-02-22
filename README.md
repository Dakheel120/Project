import streamlit as st
import math

def generate_pascals_triangle(rows):
    """Generate Pascal's Triangle up to a given number of rows."""
    triangle = [[1] * (i + 1) for i in range(rows)]
    for i in range(2, rows):
        for j in range(1, i):
            triangle[i][j] = triangle[i - 1][j - 1] + triangle[i - 1][j]
    return triangle

def combination(n, r):
    """Calculate nCr (Combinations) using factorials."""
    return math.comb(n, r) if r <= n else 0

def binomial_expansion(n):
    """Generate the binomial expansion coefficients using Pascal's Triangle."""
    return [combination(n, r) for r in range(n + 1)]

def main():
    st.title("🔢 Pascal's Triangle & Binomial Expansion Game")
    
    st.header("📌 Pascal's Triangle Generator")
    rows = st.number_input("Enter number of rows for Pascal's Triangle:", min_value=1, max_value=20, value=5)
    triangle = generate_pascals_triangle(rows)
    
    for row in triangle:
        st.write(" ".join(map(str, row)))
    
    st.header("📌 Combinatorial Calculator (nCr)")
    n = st.number_input("Enter n (total items):", min_value=0, max_value=100, value=5)
    r = st.number_input("Enter r (chosen items):", min_value=0, max_value=100, value=2)
    st.write(f"nCr ({n} choose {r}): {combination(n, r)}")
    
    st.header("📌 Binomial Expansion Calculator")
    exp_n = st.number_input("Enter exponent (n) for (a+b)^n:", min_value=0, max_value=20, value=5)
    coefficients = binomial_expansion(exp_n)
    expansion = " + ".join([f"{coeff}a^{exp_n-i}b^{i}" for i, coeff in enumerate(coefficients)])
    st.write(f"(a + b)^{exp_n} = {expansion}")
    
if __name__ == "__main__":
    main()
