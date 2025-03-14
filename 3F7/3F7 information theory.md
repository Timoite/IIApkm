# ==Probability review== 
### random variable (rv) X
### Discrete Random Variables
### Jointly distributed discrete rvs X, Y :
		Product rule
		Sum rule (marginalisation)
### Independence
### Entropy
#### Binary Entropy Function
#### Properties of Entropy
	1. H(X) ≥ 0. 
	2. If we denote the alphabet size |X | by M, then H(X) ≤                      log M 
	3. Among all random variables taking values in X , the                        equiprobable distribution ( 1 M , . . . , 1 M ) has                       the maximum entropy, equal to log M.
#### Proofs of the properties
#### Joint and Conditional Entropy
#### Joint Entropy of Multiple RVs
	Chain Rule of Joint Entropy:
		
# ==*Information theory fundamentals*== 
Markov’s Inequality
Proof of Markov’s Inequality
Chebyshev’s inequality
Weak Law of Large Numbers (WLLN)
Typicality
Typical sequences
Asymptotic Equipartition Property (AEP)
Properties of the Typical Set
Compression
	A Na¨ıve Compression Code
	Compression via the Typical Set
Fundamental Limit of Compression
# ==Lossless data compression (source coding):== 
Prefix-free codes
Extension Codes and Unique Decodability
Prefix code lengths
Kraft Inequality to prove (L ≥ H(X).)
Coding theorem for a random variable
Coding theorem for blocks of source symbols
	E[ℓ(X N )]/ N ≥ H(X)
## Practical compression algorithms 
Shannon-Fano Coding
Huffman Coding
Properties of the Huffman Code
	For a given set of probabilities, there is no prefix-free code that has smaller expected length than the Huffman code.
Interval coding
	In interval coding, the length of the binary codeword for a symbol with probability p is either l log2 1 p m or l log2 1 p m + 1 bits.
Arithmetic Coding
Expected Code Length
![[1737546596841.png]]
Arithmetic coding for non-iid sources
Finite precision issues
## Hypothesis testing, Relative entropy & Mutual information 
Relative entropy
	Relative Entropy is always non-negative
Redundancy in Source Coding
Hypothesis Testing
	Type I error: This occurs when H0 is true, but the decision rule chooses H1. 
	Type II error: This occurs when H1 is true, but the decision rule chooses H0.
Mutual Information
	I(X; Y ) = H(X) + H(Y ) − H(X, Y ) = H(Y ) − H(Y |X)
	I(X; Y ) = D (PXY ∥PX PY )
	I(X; Y ) ≥ 0
Conditional Mutual Information and Chain Rule
	I(X; Y |Z) := H(X|Z) − H(X|Y , Z).
	I(X1, X2, . . . , Xn; Y ) = Xn i=1 I(Xi ; Y |Xi−1, Xi−2, . . . , X1 )

# ==Data transmission (channel coding):== 
Data Transmission
Coding and Modulation
Binary Channel
Binary Symmetric Channel (BSC)
Discrete Memoryless Channel
## Channel capacity; 
The channel capacity of a discrete memoryless channel is defined as C = max PX I(X; Y )
Noiseless Binary Channel
BSC
Noisy Keyboard Channel
Binary Erasure Channel
## the coding theorem for noisy channels Practical channel coding techniques 
The idea for a general DMC
Joint Typical Set
The Joint AEP
The Probability of Error of a Code
Theorem 
	“For a DMC with capacity C, all rates less than C are achievable.” 
	Specifically, 
	1. Fix R < C and pick any ϵ > 0. Then, for all sufficiently large n there exists a length-n code of rate R with maximal probability of error less than ϵ.
	 2. Conversely, any sequence of length-n codes of rate R with average/maximal probability of error P (n) e → 0 as n → ∞ must have R ≤ C.
Encoding
Joint Typicality Decoder
Analysing the probability of error
Error Analysis
The Final Code
## Data Processing and Mutual Information
Fano’s inequality
1 + Pe log |X | ≥ H(X|Xˆ) ≥ H(X|Y )
	1. H(E|X, Xˆ) = 0. (because E is a function of (X, Xˆ)) 
	2. H(E|Xˆ) ≤ H(E) = H2 (Pe ). (conditioning can only reduce H) 
	3. H(X|Xˆ, E) ≤ Pe log|X | because H(X|Xˆ, E) = Pr(E = 0)H(X|Xˆ, E = 0) + Pr(E = 1)H(X|Xˆ, E = 1) ≤ (1 − Pe ) 0 + Pe log|X
A Little Lemma
	Let Y n be the result of passing a sequence X n through a DMC of channel capacity C. Then I(X n ; Y n ) ≤ nC regardless of the distribution of X n
C is a sharp threshold: ▶ For all rates R < C, there exists a sequence of (2nR, n) codes whose Pe → 0. ▶ For R > C, you cannot find a sequence of (2nR, n) codes whose Pe → 0


# ==Other applications of information theory + Review==
The Additive White Gaussian Noise (AWGN) Channel
Information Theory for Continuous Alphabets
Differential Entropy of Multiple RVs
Capacity of the discrete-time AWGN Channel
Computing the AWGN Capacity
	Among all random variables Y with EY 2 ≤ (P + σ 2 ), the maximum differential entropy is achieved when Y is Gaussian N (0, P + σ 2 )
Capacity of the AWGN Channel
	![[1737553112899.png]]
### Binary Linear Block Codes
Block Code
Minimum distance of a code
Optimal Decoding of a Block Code
	Decode cˆ = arg maxc∈{c1 ,...,cM } Pr(y | c)
Optimal decoding on the BSC(p)
	We can successfully correct any pattern of t errors if t ≤ ⌊ dmin−1 2 ⌋ 9 / 2
Linear Block Codes
Systematic Generator Matrices
Converting to Systematic Form
LBCs as Subspaces
The Parity Check Matrix
Minimum Distance of an LBC
	Let C be an linear block code with parity check matrix H. The minimum distance of C is the smallest number of columns of H that sum to 0.
Performance of Block Codes over a BSC(p)
A caveat about minimum-distance
### Low Density Parity Check (LDPC) Codes for the Binary Erasure Channel
Linear Codes for the BEC
Iterative Decoding
Low-Density Parity Check (LDPC) Matrix
Regular LDPC codes
Factor graph of a linear code
Iterative Decoding as Message Passing
Message passing for the Hamming code
### Designing good LDPC codes
Degree distributions
Density Evolution
Irregular Codes
### Low Density Parity Check (LDPC) codes for general binary input channels
The Set-up
Optimal decoding: block-wise vs. bit-wise
Why optimal decoding is hard
Message Passing Decoding
Variable-to-check messages
Check-to-variable messages
Computing P(cj | yj )
Log-domain message passing
Algorithm termination
Complexity of decoding
Constructing good LDPC codes