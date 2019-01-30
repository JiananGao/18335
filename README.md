#  18.335J/6.337J: Introduction to Numerical Methods

This is the repository of course materials for the 18.335J/6.337J course at MIT, taught by Prof. [Steven G. Johnson](http://math.mit.edu/~stevenj/), in Spring 2015.

Syllabus
--------

**Lectures**: Monday/Wednesday/Friday 3–4pm (4-163). **Office Hours:** Thursday 4–5pm (E17-416).

**Topics**: Advanced introduction to numerical linear algebra and related numerical methods. Topics include direct and iterative methods for linear systems, eigenvalue decompositions and QR/SVD factorizations, stability and accuracy of numerical algorithms, the IEEE floating-point standard, sparse and structured matrices, and linear algebra software. Other topics may include memory hierarchies and the impact of caches on algorithms, nonlinear optimization, numerical integration, FFTs, and sensitivity analysis. Problem sets will involve use of [Julia](http://julialang.org/), a Matlab-like environment (little or no prior experience required; you will learn as you go).

**Prerequisites**: Understanding of linear algebra ([18.06](http://web.mit.edu/18.06/www/), [18.700](http://ocw.mit.edu/OcwWeb/Mathematics/18-700Fall-2005/CourseHome/), or equivalents). Ordinary differential equations ([18.03](http://math.mit.edu/18.03/) or 18.034) is another listed prerequisite (not so much as specific material, but more as experience with post-freshman calculus).

**Textbook**: The primary textbook for the course is [_Numerical Linear Algebra_ by Trefethen and Bau](http://www.amazon.com/Numerical-Linear-Algebra-Lloyd-Trefethen/dp/0898713617). ([Readable online](http://owens.mit.edu:8888/sfx_local?bookid=9436&rft.genre=book&sid=Barton:Books24x7) with MIT certificates.)

**Other Reading**: Previous terms can be found in [branches of the 18335 git repository](https://github.com/mitmath/18335/branches). The [course notes from 18.335 in much earlier terms](https://ocw.mit.edu/courses/mathematics/18-335j-introduction-to-numerical-methods-fall-2010/) can be found on OpenCourseWare. For a review of iterative methods, the online books [Templates for the Solution of Linear Systems](http://www.netlib.org/linalg/html_templates/Templates.html) (Barrett et al.) and [Templates for the Solution of Algebraic Eigenvalue Problems](http://www.cs.utk.edu/~dongarra/etemplates/book.html) are useful surveys.

**Grading**: 33% problem sets (about six, ~biweekly). 33% **mid-term exam** (Monday **Apr. 6 from 2-4pm or from 3-5pm, room 50-340**), 34% **final project** (one-page proposal due Friday, March 20, project due Wed., **May 13**).

**TA:** Adrian Vladu (avladu at math.mit) and Aden Forrow (aforrow at mit). Submit your psets electronically to 18335sp15 at gmail.

**Collaboration policy**: Talk to anyone you want to and read anything you want to, with three exceptions: First, you **may not refer to homework solutions from the previous terms** in which I taught 18.335. Second, make a solid effort to solve a problem on your own before discussing it with classmates or googling. Third, no matter whom you talk to or what you read, write up the solution on your own, without having their answer in front of you.

**Final Projects**: The final project will be a 8–15 page paper (single-column, single-spaced, ideally using the style template from the [_SIAM Journal on Numerical Analysis_](http://www.siam.org/journals/auth-info.php)), reviewing some interesting numerical algorithm not covered in the course. \[Since this is not a numerical PDE course, the algorithm should _not_ be an algorithm for turning PDEs into finite/discretized systems; however, your project _may_ take a PDE discretization as a given "black box" and look at some other aspect of the problem, e.g. iterative solvers.\] Your paper should be written for an audience of your peers in the class, and should include example numerical results (by you) from application to a realistic problem (small-scale is fine), discussion of accuracy and performance characteristics (both theoretical and experimental), and a fair comparison to at **least one competing algorithm** for the same problem. Like any review paper, you should _thoroughly reference_ the published literature (citing both original articles and authoritative reviews/books where appropriate \[rarely web pages\]), tracing the historical development of the ideas and giving the reader pointers on where to go for more information and related work and later refinements, with references cited throughout the text (enough to make it clear what references go with what results). (**Note:** you may re-use diagrams from other sources, but all such usage must be _explicitly credited_; not doing so is [plagiarism](http://writing.mit.edu/wcc/avoidingplagiarism).) Model your paper on academic review articles (e.g. read _SIAM Review_ and similar journals for examples).

Frequently asked questions about the final project:

1.  _Does it have to be about numerical linear algebra?_ No. It can be any numerical topic (basically, anything where you are computing a conceptually real result, not integer computations), excluding algorithms for discretizing PDEs.
2.  _Can I use a matrix from a discretized PDE?_ Yes. You can take a matrix from the PDE as input and then talk about iterative methods to solve it, etcetera. I just don't want the paper to be about the PDE discretization technique itself.
3.  _How formal is the proposal?_ Very informal—one page describing what you plan to do, with a couple of references that you are using as starting points. Basically, the proposal is just so that I can verify that what you are planning is reasonable and to give you some early feedback.
4.  _How much code do I need to write?_ A typical project (there may be exceptions) will include a working proof-of-concept implementation, e.g. in Julia or Python or Matlab, that you wrote to demonstrate that you understand how the algorithm works. Your code does _not_ have to be competitive with "serious" implementations, and I encourage you to download and try out existing "serious" implementations (where available) for any large-scale testing and comparisons.
5.  _How should I do performance comparisons?_ Be very cautious about timing measurements: unless you are measuring highly optimized code or only care about orders of magnitude, timing measurements are more about implementation quality than algorithms. Better to measure something implementation independent (like flop counts, or matrix-vector multiplies for iterative algorithms, or function evaluations for integrators/optimizers), although such measures have their own weaknesses.

* * *

Lecture Summaries and Handouts
------------------------------

### Lecture 1 (Feb 4)

**Handouts:** a printout of this webpage (i.e., the syllabus). [Newton's method for square roots](newton-sqrt.pdf) and accompanying [notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Newton-Square-Roots.ipynb)

Brief overview of the huge field of numerical methods, and outline of the small portion that this course will cover. Key new concerns in numerical analysis, which don't appear in more abstract mathematics, are (i) performance (traditionally, arithmetic counts, but now memory access often dominates) and (ii) accuracy (both floating-point roundoff errors and also convergence of intrinsic approximations in the algorithms).

As a starting example, considered the convergence of Newton's method (as applied to square roots); see the handout and Julia notebook above.

**Further reading:** Googling "Newton's method" will find lots of references; as usual, the [Wikipedia article on Newton's method](https://en.wikipedia.org/wiki/Newton's_method) is a reasonable starting point. Beware that the terminology for the [convergence order](https://en.wikipedia.org/wiki/Rate_of_convergence) (linear, quadratic, etc.) is somewhat different in this context from the terminology for discretization schemes (first-order, second-order, etc.); see e.g. the linked Wikipedia article. Homer Reid's [notes on machine arithmetic](http://homerreid.dyndns.org/teaching/18.330/Notes/RootFinding.pdf) for [18.330](http://homerreid.dyndns.org/teaching/18.330/) are an excellent introduction that covers several applications and algorithms for root-finding. For numerical computation in 18.335, we will be using the Julia language: see this [information on Julia at MIT](https://github.com/stevengj/julia-mit).

### Lecture 2 (Feb 6)

**Handouts:** [notes on floating-point](http://persson.berkeley.edu/18.335/lec8handout6pp.pdf) (18.335 Fall 2007; [slides](http://persson.berkeley.edu/18.335/lec8.pdf)); Julia [floating-point notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Floating-Point-Intro.ipynb), some [floating-point myths](fp-myths.pdf); [pset 1](pset1-s15.pdf) and accompanying [notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/pset1-template-s15.ipynb) (due Feb 17 — TUESDAY = MIT Monday)

New topic: **Floating-point arithmetic**

The basic issue is that, for computer arithmetic to be fast, it has to be done in hardware, operating on numbers stored in a fixed, finite number of digits (bits). As a consequence, only a _finite subset_ of the real numbers can be represented, and the question becomes _which subset_ to store, how arithmetic on this subset is defined, and how to analyze the errors compared to theoretical exact arithmetic on real numbers.

In **floating-point** arithmetic, we store both an integer coefficient and an exponent in some base: essentially, scientific notation. This allows large dynamic range and fixed _relative_ accuracy: if fl(x) is the closest floating-point number to any real x, then |fl(x)-x| < ε|x| where ε is the _machine precision_. This makes error analysis much easier and makes algorithms mostly insensitive to overall scaling or units, but has the disadvantage that it requires specialized floating-point hardware to be fast. Nowadays, all general-purpose computers, and even many little computers like your cell phones, have floating-point units.

Went through some simple examples in Julia (see notebook above), illustrating basic syntax and a few interesting tidbits, in particular on the accuracy of summation algorithms, that we will investigate in more detail later.

Overview of **floating-point** representations, focusing on the IEEE 754 standard (see also handout from previous lecture). The key point is that the nearest floating-point number to _x_, denoted fl(_x_), has the property of _uniform relative precision_ (for |_x_| and 1/|_x_| < than some _range_, ≈10308 for double precision) that |fl(_x_)−_x_| ≤ εmachine|_x_|, where εmachine is the relative "machine precision" (about 10−16 for double precision). There are also a few special values: ±Inf (e.g. for [overflow](https://en.wikipedia.org/wiki/Arithmetic_overflow)), [NaN](https://en.wikipedia.org/wiki/NaN), and ±0 (e.g. for [underflow](https://en.wikipedia.org/wiki/Arithmetic_underflow)).

**Further reading:** [What Every Computer Scientist Should Know About Floating Point Arithmetic](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.22.6768) (David Goldberg, ACM 1991). William Kahan, [How Java's floating-point hurts everyone everywhere](http://www.cs.berkeley.edu/~wkahan/JAVAhurt.pdf) (2004): contains a nice discussion of floating-point myths and misconceptions. Trefethen, lecture 13. Homer Reid's [notes on machine arithmetic](http://homerreid.dyndns.org/teaching/18.330/Notes/MachineArithmetic.pdf) for [18.330](http://homerreid.dyndns.org/teaching/18.330/) are an excellent introduction to this material.

### Lecture 3 (Feb 1)

**Handout:** [notes on backwards stability of summation](summation-stability.pdf)

**Stability:** Gave the obvious definition of **accuracy**, or more technically stability: "forwards stability" = almost the right answer for the right input. Showed that this is often too strong; e.g. adding a sequence of numbers is not forwards stable. (Basically because the denominator in the relative forwards error, which is the exact sum, can be made arbitrarily small via cancellations.)

Define asymptotic notation O(ε): f(ε) is O(g(ε)) if there exist some constants C, δ > 0 such that |f(ε)| < C|g(ε)| for all |ε|<δ. That is, g(ε) is an asymptotic _upper bound_ for f(ε) as ε goes to zero, ignoring constant factors C. (A similar notation is used in computational complexity theory, but in the limit of _large_ ε.) In the definitions of stability, we technically require [uniform convergence](https://en.wikipedia.org/wiki/Uniform_convergence): we must have O(ε) errors with the same constants C and δ independent of the inputs x.

More generally, we apply a weaker condition: "stability" = almost the right answer for almost the right input. (Gave the technical version of this, from the book.) Forwards stability implies stability but not the converse.

Often, it is sufficient to prove "backwards stability" = right answer for almost the right input. Showed that, in our example of adding a sequence of numbers, backwards stability seems to work where forwards stability failed. Then more rigorously proved that floating-point summation of _n_ numbers is backwards stable. Began discussing a more formal proof of stability of summation (handout).

**Further reading**: See the further reading from the previous lecture. Trefethen, lectures 14, 15, and 3. See also the Wikipedia article on [asymptotic ("big O") notation](https://en.wikipedia.org/wiki/Big_O_notation); note that for expressions like O(ε) we are looking in the limit of _small_ arguments rather than of large arguments (as in complexity theory), but otherwise the ideas are the same.

### Julia tutorial (Feb 11: 4:30pm in 1-190) — optional

**Handout:** [Julia cheat-sheet](https://github.com/mitmath/julia-mit/blob/master/Julia-cheatsheet.pdf)

On Monday, 9 Wednesday 11 February (I hope), at 4:30pm in 1-190, I will give an (attendance-optional!) Julia tutorial, introducing the [Julia programming language and environment](http://julialang.org/) that we will use this term. Please see the [tutorial notes online](https://github.com/mitmath/julia-mit/blob/master/README.md).

Please **bring your laptops**, and try to install Julia and the IJulia interface first via the abovementioned tutorial notes. Several people will be at the tutorial session to help answer installation questions. Alternatively, you can use Julia online at [JuliaBox](https://juliabox.org/) without installing anything (although running things on your own machine is usually faster).

### Lecture 4 (Feb 13)

Finish proof of backwards-stability of recursive summation, from last lecture.

When quantifying errors, a central concept is a norm, and we saw in our proof of backwards stability of summation that the choice of norm seems important. Defined norms (as in lecture 3 of Trefethen), gave examples of norms of column vectors: _Lp_ norms (usually _p_ = 1, 2, or ∞) and weighted L2 norms.

Started discussing matrix norms. The most important matrix norms are those that are related to matrix operations. Started with the Frobenius norm. Related the Frobenius norm |A|F to the square root of the sum of eigenvalues of A\*A, which are called the _singular values_ σ2; we will do much more on singular values later, but for now noted that they equal the squared eigenvalues of A if A\*\=A (Hermitian). Also defined

**Further reading:** Trefethen, lecture 3. If you don't immediately recognize that A\*A has nonnegative real eigenvalues (it is positive semidefinite), now is a good time to review your linear algebra.

### Lecture 5 (Feb 17 — note that TUESDAY is an "MIT Monday")

**Handout:** [notes on the equivalence of norms](norm-equivalence.pdf)

Equivalence of norms. Described fact that any two norms are equivalent up to a constant bound, and showed that this means that **stability in one norm implies stability in all norms.** Sketched proof (_only skimmed this_): (i) show we can reduce the problem to proving any norm is equivalent to _L_1 on (ii) the unit circle; (iii) show any norm is continuous; and (ii) use a result from real analysis: a continuous function on a closed/bounded (compact) set achieves its maximum and minimum, the [extreme value theorem](http://en.wikipedia.org/wiki/Extreme_value_theorem). See notes handout.

Relate backwards error to forwards error, and backwards stability to forwards error (or "accuracy" as the book calls it). Show that, in the limit of high precision, the forwards error can be bounded by the backwards error multiplied by a quantity κ, the **relative condition number**. The nice thing about κ is that it involves only exact linear algebra and calculus, and is completely separate from considerations of floating-point roundoff. Showed that, for differentiable functions, κ can be written in terms of the induced norm of the Jacobian matrix.

**Further reading:** Trefethen, lectures 12, 14, 15, 24.

### Lecture 6 (Feb 18)

**Handout:** [pset 1 solutions](pset1sol-s15.pdf) and [Julia notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/pset1sol-s15.ipynb); [pset 2](pset2-s15.pdf) (due Fri 2/27).

Calculated condition number for square root, summation, and matrix-vector multiplication, as well as solving Ax=b, similar to the book. Defined the condition number of a matrix.

Related matrix _L_2 norm to eigenvalues of _B_\=_A_\*_A_. _B_ is obviously Hermitian (_B_\*\=_B_), and with a little more work showed that it is positive semidefinite: _x_\*_B__x_≥0 for any _x_. Reviewed and re-derived properties of eigenvalues and eigenvectors of Hermitian and positive-semidefinite matrices. Hermitian means that the eigenvalues are real, the eigenvectors are orthogonal (or can be chosen orthogonal). Also, a Hermitian matrix must be diagonalizable (I skipped the proof for this; we will prove it later in a more general setting). Positive semidefinite means that the eigenvalues are nonnegative.

Proved that, for a Hermitian matrix B, the **Rayleigh quotient** R(x)=x\*Bx/x\*x is bounded above and below by the largest and smallest eigenvalues of B (the "min–max theorem"). Hence showed that the L2 induced norm of A is the square root of the largest eigenvalue of _B_\=_A_\*_A_. Similarly, showed that the L2 induced norm of A\-1, or more generally the infimum of |x|/|Ax|, is equal to the square root of the inverse of the smallest eigenvalue of _A_\*._A_

Understanding norms and condition numbers of matrices therefore reduces to understanding the eigenvalues of _A_\*_A_ (or _A__A_\*). However, looking at it this way is unsatisfactory for several reasons. First, we would like to solve one eigenproblem, not two. Second, working with things like _A_\*_A_ explicitly is often bad numerically, because it squares the condition number \[showed that κ(_A_\*_A_)=κ(_A_)2\] and hence exacerbates roundoff errors. Third, we would really like to get some better understanding of _A_ itself. All of these concerns are addressed by the **singular value decomposition** or **SVD**, which we will derive next time.

**Further reading:** Trefethen, lectures 12, 14, 15, 24. See any linear-algebra textbook for a review of eigenvalue problems, especially Hermitian/real-symmetric ones.

### Lecture 7 (Feb 20)

Explicitly constructed SVD in terms of eigenvectors/eigenvalues of _A_\*_A_ and _A__A_\*. Recall from last time that we related the singular values to induced L2 norm and condition number.

Talked a little about the SVD and low-rank approximations (more on this in homework). Talked about [principal component analysis](http://en.wikipedia.org/wiki/Principal_component_analysis) (PCA), and gave ["eigenwalker"](http://www.biomotionlab.ca/Demos/BMLwalker.html) demo. Also gave an [SVD image-compression](https://inst.eecs.berkeley.edu/~ee127a/book/login/l_svd_apps_image.html) example, which illustrates how good the biggest singular values are at picking up the "important" information in a matrix (or image), although this is not a practical compression scheme compared to e.g. [JPEG](http://en.wikipedia.org/wiki/JPEG).

**Further reading:** Trefethen, lectures 4, 5, 11.

### Lecture 8 (Feb 23)

**Handouts:** [least-squares IJulia notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Least-squares.ipynb)

Introduced least-squares problems, gave example of polynomial fitting, gave normal equations, and derived them from the condition that the L2 error be minimized.

Discussed solution of normal equations. Discussed condition number of solving normal equations directly, and noted that it squares the condition number—not a good idea if we can avoid it.

Introduced the alternative of QR factorization (finding an orthonormal basis for the column space of the matrix). Explained why, if we can do it accurately, this will give a good way to solve least-squares problems.

**Further reading:** Trefethen, lectures 7, 8, 18, 19

### Lecture 9 (Feb 25)

**Handouts:** [Gram-Schmidt IJulia notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Gram-Schmidt.ipynb)

Gave the simple, but unstable, construction of the Gram-Schmidt algorithm, to find a QR factorization.

Discussed loss of orthogonality in classical Gram-Schmidt, using a simple example, especially in the case where the matrix has nearly dependent columns to begin with. Showed modified Gram-Schmidt and argued how it (mostly) fixes the problem. Numerical examples (see notebook).

Re-interpret Gram-Schmidt in matrix form as Q = AR1R2..., i.e. as multiplying A on the right by a sequence of upper-triangular matrices to get Q. The problem is that these matrices R may be very badly conditioned, leading to an inaccurate Q and loss of orthogonality. Instead of multiplying A on the right by R's to get Q, however, we can instead multiply A on the left by Q's to get R. This leads us to the Householder QR algorithm.

**Further reading:** Trefethen, lectures 7, 8, 18, 19. Per Persson's [2004 18.335 Gram-Schmidt notes](http://persson.berkeley.edu/18.335/lec5.pdf) are also helpful, as is the [Wikipedia Gram-Schmidt article](https://en.wikipedia.org/wiki/Gram%E2%80%93Schmidt_process). It turns out that modified GS is backwards stable in the sense that the product QR is close to A, i.e. the function f(A) = Q\*R is backwards stable in MGS; this is why solving systems with Q,R (appropriately used as discussed in Trefethen lecture 19) is an accurate approximation to solving them with A. For a review of the literature on backwards-stability proofs of MGS, see e.g. [this 2006 paper by Paige et al.](http://www.cs.cas.cz/miro/prs05.pdf) \[_SIAM J. Matrix Anal. Appl._ **28**, pp. 264-284\].

### Lecture 10 (Feb 27)

**Handouts:** [pset 2 solutions](pset2sol-s15.pdf)

Introduced Householder QR, emphasized the inherent stability properties of multiplying by a sequence of unitary matrices (as shown in pset 2). Show how we can convert a matrix to upper-triangular form (superficially similar to Gaussian elimination) via unitary Householder reflectors.

Finished Householder QR derivation, including the detail that one has a choice of Householder reflectors...we choose the sign to avoid taking differences of nearly-equal vectors. Gave flop count, showed that we don't need to explicitly compute Q if we store the Householder reflector vectors.

Operation count for Gram-Schmidt (2mn2) and Householder (2mn2 - 2n3/3), using the simple "graphical" estimation method from Trefethen. Evidently, Householder is at least as accurate as modified GS while being slightly faster. But does fewer operations really mean it is faster?

**Further reading:** Trefethen, lectures 7, 8, 10, 16.

### Lecture 11 (Mar 2)

**Handouts:** performance experiments with matrix multiplication ([one-page](matmuls-handout.pdf) or [full-size](matmuls.pdf) versions); [ideal-cache terminology](ideal-cache.pdf); [IJulia matrix-multiplication notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Matrix-multiplication-experiments.ipynb)

Counting arithmetic operation counts is no longer enough. Illustrate this with some performance experiments on a much simpler problem, matrix multiplication (see handouts). This leads us to analyze memory-access efficiency and caches and points the way to restructuring many algorithms.

Outline of the memory hierarchy: CPU, registers, L1/L2 cache, main memory, and presented simple 2-level ideal-cache model that we can analyze to get the basic ideas.

Analyzed cache complexity of simple row-column matrix multiply, showed that it asymptotically gets no benefit from the cache. Presented blocked algorithm, and showed that it achieves optimal Θ(_n_3/√_Z_) cache complexity.

Discussed some practical difficulties of the blocked matrix multiplication: algorithm depends on cache-size _Z_, and multi-level memories require multi-level blocking. Discussed how these ideas are applied to the design of modern linear-algebra libraries (LAPACK) by building them out of block operations (performed by an optimized BLAS).

**Further reading:** Wikipedia has a reasonable [introduction to memory locality](http://en.wikipedia.org/wiki/Locality_of_reference) that you might find useful. The optimized matrix multiplication shown on the handouts is called ATLAS, and you can find out more about it on the [ATLAS web page](http://math-atlas.sourceforge.net/). [Cache-oblivious algorithms](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.34.7911), describing ideal cache model and analysis for various algorithms, by Frigo, Leiserson, Prokop, and Ramachandran (1999). [Notes on the switch from LINPACK to LAPACK/BLAS in Matlab](http://www.mathworks.com/company/newsletters/news_notes/clevescorner/winter2000.cleve.html). The MIT course [6.172](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-172-performance-engineering-of-software-systems-fall-2010/index.htm) has two lecture videos ([first](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-172-performance-engineering-of-software-systems-fall-2010/video-lectures/lecture-8-cache-efficient-algorithms) and [second](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-172-performance-engineering-of-software-systems-fall-2010/video-lectures/lecture-9-cache-efficient-algorithms-ii)) on cache-efficient algorithms, including a discussion of matrix multiplication.

### Lecture 12 (Mar 4)

**Handouts:** experiments with cache-oblivious matrix-multiplication ([handout](oblivious-matmul-handout.pdf) or [full-size slides](oblivious-matmul.pdf)); see also notebook from previous lecture; [pset 3](pset3-s15.pdf) and [notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/pset3-s15.ipynb) (due Friday Mar 13).

Introduced the concept of optimal cache-oblivious algorithms. Discussed cache-oblivious matrix multiplication in theory and in practice (see handout and Frigo et. al paper above).

Discussion of spatial locality and cache lines, with examples of dot products and matrix additions (both of which are "level 1 BLAS" operations with no temporal locality); you'll do more on this in pset 3.

Review of **Gaussian elimination**. Reviewed the fact that this givs an A=LU factorization, and that we then solve Ax=b by solving Ly=b (doing the same steps to b that we did to A during elimination to get y) and then solving Ux=y (backsubstitution). Emphasized that you should _almost never compute A\-1_ explicitly. It is just as cheap to keep L and U around, since triangular solves are essentially the same cost as a matrix-vector multiplication. Computing A\-1 is usually a mistake: you can't do anything with A\-1 that you couldn't do with L and U, and you are wasting both computations and accuracy in computing A\-1. A\-1 is useful in abstract manipulations, but whenever you see "x=A\-1b" you should interpret it for computational purposes as solving Ax=b by LU or some other method.

**Further reading:** Frigo et al. paper from previous lecture. ATLAS web page above. See [Register Allocation in Kernel Generators](http://cscads.rice.edu/workshops/july2007/autotune-slides-07/Frigo.pdf) (talk by M. Frigo, 2007) on the difficulty of optimizing for the last level of cache (the registers) in matrix multiplication (compared to FFTs), and why a simple cache-oblivious algorithm is no longer enough. See e.g. the Wikipedia article on [row-major and column-major order](http://en.wikipedia.org/wiki/Row-major_order). Trefethen, lectures 20, 21, 22, 23.

### Lecture 13 (Mar 6)

Introduced partial pivoting, and pointed out (omitting bookkeeping details) that this can be expressed as a PA=LU factorization where P is a permutation. Began to discuss backwards stability of LU, and mentioned example where U matrix grows exponentially fast with _m_ to point out that the backwards stability result is practically useless here, and that the (indisputable) practicality of Gaussian elimination is more a result of the types of matrices that arise in practice.

Briefly discussed Cholesky factorization, which is Gaussian elimation for the special case of Hermitian positive-definite matrices, where we can save a factor of two in time and memory. More generally, if the matrix A has a special form, one can sometimes take advantage of this to have a more efficient Ax=b solver, for example: Hermitian positive-definite (Cholesky), tridiagonal or banded (linear-time solvers), lower/upper triangular (forward/backsubstitution), sparse (mostly zero—sparse-direct and iterative solvers, to be discussed later; typically only worthwhile when the matrix is much bigger than 1000×1000).

New topic: **eigenproblems**. Reviewed the usual formulation of eigenproblems and the characteristic polynomial, mentioned extensions to generalized eigenproblems and SVDs. Discussed diagonalization, defective matrices, and the generalization ot the Schur factorization.

**Further reading:** Trefethen, lectures 20, 21, 22, 23. See all of the [special cases of LAPACK's linear-equation solvers](http://www.netlib.org/lapack/lug/node38.html).

### Lecture 14 (Mar 9)

Discussed diagonalization, defective matrices, and the generalization ot the Schur factorization. Proved (by induction) that every (square) matrix has a Schur factorization, and that for Hermitian matrices the Schur form is real and diagonal.

Pointed out that an "LU-like" algorithm for eigenproblems, which computes the exact eigenvalues/eigenvectors (in exact arithmetic, neglecting roundoff) in a finite number of steps involving addition, subtraction, multiplication, division, and roots, is impossible. The reason is that no such algorithm exists (or can _ever_ exist) to find roots of polynomials with degree greater than 4, thanks to a theorem by Abel, Galois and others in the 19th century. Used the [companion matrix](http://en.wikipedia.org/wiki/Companion_matrix) to show that polynomial root finding is equivalent to the problem of finding eigenvalues. Mentioned the connection to other classic problems of antiquity (squaring the circle, trisecting an angle, doubling the cube), which were also proved impossible in the 19th century.

As a result, all eigenproblem methods must be _iterative_: they must consist of improving an initial guess, in successive steps, so that it converges towards the exact result to _any desired accuracy_, but never actually reaches the exact answer in general. A simple example of such a method is Newton's method, which can be applied to iteratively approximate a root of any nonlinear function to any desired accuracy, given a sufficiently good initial guess.

However, finding roots of the characteristic polynomial is generally a terrible way to find eigenvalues. Actually computing the characteristic polynomial coefficients and then finding the roots somehow (Newton's method?) is a disaster, incredibly ill-conditioned: gave the example of [Wilkinson's polynomial](http://en.wikipedia.org/wiki/Wilkinson%27s_polynomial). If we can compute the characteristic polynomial values implicitly somehow, directly from the determinant, then it is not too bad (if you are looking only for eigenvalues in some known interval, for example), but we haven't learned an efficient way to do that yet. The way LAPACK and Matlab actually compute eigenvalues, the QR method and its descendants, wasn't discovered until 1960.

**Further reading:** Trefethen, lecture 24, 25. See [this Wilkinson polynomial Julia notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Wilkinson-Polynomial.ipynb) for some experiments with polynomial roots in Julia.

### Lecture 15 (Mar 11)

**Handouts:** [notes on Hessenberg factorization](http://persson.berkeley.edu/18.335/lec14handout6pp.pdf)

The key to making most of the eigensolver algorithms efficient is reducing A to **Hessenberg form**: A=QHQ\* where H is upper triangular plus one nonzero value below each diagonal. Unlike Schur form, Hessenberg factorization _can_ be done exactly in a finite number \[Θ(m3)\] of steps (in exact arithmetic). H and A are similar: they have the same eigenvalues, and the eigenvector are related by Q. And once we reduce to Hessenberg form, all the subsequent operations we might want to do (determinants, LU or QR factorization, etcetera), will be fast. In the case of Hermitian A, showed that H is tridiagonal; in this case, most subsequent operations (even LU and QR factorization) will be Θ(m) (you will show this in HW)!

For example we can actually evaluate det(A-λI)=det(H-λI) in O(m2) time for each value of λ, or O(m) time if A is Hermitian, making e.g. Newton's method on det(H-λI) much more practical. It will also accelerate lots of other methods to find eigenvalues.

Introduced basic idea of Hessenberg factorization by relating it to Householder QR, and in particular showed that Householder reflectors will do the job as long as we allow one nonzero element below the diagonal (see handout).

Discussed power method for biggest-|λ| eigenvector/eigenvalue, and (re-)introduced the Rayleigh quotient to estimate the eigenenvalue. Discussed the convergence rate, and how for Hermitian matrix the eigenvalue estimate has a much smaller error than the eigenvector (the error is squared) due to the fact that the eigenvalue is an extremum.

Discussed how to use the power method to get multiple eigenvalues/vectors of Hermitian matrices by "deflation" (using orthogonality of eigenvectors). Discussed how, in principle, QR factorization of _An_ for large _n_ will give the eigenvectors and eigenvalues in descending order of magnitude, but how this is killed by roundoff errors.

**Further reading:** See Trefethen, lecture 27, and these [2007 notes](http://persson.berkeley.edu/18.335/lec15handout6pp.pdf) on power/inverse/Rayleigh iteration.

### Lecture 16 (Mar 13)

**Handouts:** [pset 3 solutions](pset3sol-s15.pdf) and [notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/pset3sol-s15.ipynb)

Unshifted QR method: proved that repeatedly forming A=QR, then replacing A with RQ (as in pset 3) is equivalent to QR factorizing _An_. But since we do this while only multiplying repeatedly by unitary matrices, it is well conditioned and we get the eigenvalues accurately.

To make the QR method faster, we first reduce to Hessenberg form; you will show in pset 4 that this is especially fast when A is Hermitian and the Hessenberg form is tridiagonal. Second, we use shifts.

In particular, the worst case for the QR method, just as for the power method, is when eigenvalues are nearly equal. We can fix this by shifting.

Discussed inverse iteration and shifted-inverse iteration. Discussed Rayleigh-quotient iteration (shifted-inverse iteration with the Rayleigh-quotient eigenvalue estimate as the shift) and its convergence rate in the Hermitian case.

Briefly mentioned the Wilkinson shift to break ties, rather than just using a shift based on the minimum |λ| estimate.

There are a number of additional tricks to further improve things, the most important of which is probably the Wilkinson shift: estimating μ from a little 2×2 problem from the last _two_ columns to avoid problems in cases e.g. where there are two equal and opposite eigenvalues. Some of these tricks (e.g. the Wilkinson shift) are described in the book, and some are only in specialized publications. If you want the eigenvectors as well as eigenvalues, it turns out to be more efficient to use a more recent "divide and conquer" algorithm, summarized in the book, but where the details are especially tricky and important. However, at this point I don't want to cover more gory details in 18.335. Although it is good to know the general structure of modern algorithms, especially the fact that they look nothing like the characteristic-polynomial algorithm you learn as an undergraduate, as a practical matter you are always just going to call LAPACK if the problem is small enough to solve directly. Matters are different for much larger problems, where the algorithms are not so bulletproof and one might need to get into the guts of the algorithms; this will lead us into the next topic of the course, iterative algorithms for large systems, in subsequent lectures.

Briefly discussed Golub–Kahn bidiagonalization method for SVD, just to get the general flavor. At this point, however, we are mostly through with details of dense linear-algebra techniques: the important thing is to grasp the fundamental ideas rather than zillions of little details, since in practice you're just going to use LAPACK anyway.

**Further reading:** See Trefethen, lectures 27–30, and Per Persson's [2007 notes](http://persson.berkeley.edu/18.335/lec15handout6pp.pdf) on power/inverse/Rayleigh iteration and on QR ([part 1](http://persson.berkeley.edu/18.335/lec15handout6pp.pdf) and [part 2](http://persson.berkeley.edu/18.335/lec16handout6pp.pdf)).

### Lecture 17 (Mar 16)

Started discussing (at a very general level) a new topic: **iterative algorithms**, usually for sparse matrices, and in general for matrices where you have a fast way to compute _Ax_ matrix-vector products but cannot (practically) mess around with the specific entries of _A_.

Emphasized that there are many iterative methods, and that there is no clear "winner" or single bulletproof library that you can use without much thought (unlike LAPACK for dense direct solvers). It is problem-dependent and often requires some trial and error. Then there is the whole topic of preconditioning, which we will discuss more later, which is even more problem-dependent. Briefly listed several common techniques for linear systems (Ax=b) and eigenproblems (Ax=λx or Ax=λBx).

Gave simple example of power method, which we already learned. This, however, only keeps the most recent vector Anv and throws away the previous ones. Introduced Krylov subspaces, and the idea of Krylov subspace methods: find the best solution in the whole subspace spanned by v,Av,...,An-1v.

Derive the Arnoldi algorithm. Unlike the book, I _start_ the derivation by considering it to be modified Gram-Schmidt on (q1,Aq1,Aq2,Aq3,...). In the next lecture, we will re-interpret this as a partial Hessenberg factorization.

Discussed what it means to stop Arnoldi after n<m iterations: finding the "best" solution in the Krylov subspace Kn. Discussed the general principle of Rayleigh-Ritz methods for approximately solving the eigenproblem in a subspace: finding the Ritz vectors/values (= eigenvector/value approximations) with a residual perpendicular to the subspace (a special case of a Galerkin method).

Also showed that the max/min Ritz values are the maximum/minimum of the Rayleigh quotient in the subspace.

**Further reading:** Trefethen, lecture 31, 32, 33, 34. The online books, [Templates for the Solution of Linear Systems](http://www.netlib.org/linalg/html_templates/Templates.html) (Barrett et al.) and [Templates for the Solution of Algebraic Eigenvalue Problems](http://www.cs.utk.edu/~dongarra/etemplates/book.html), are useful surveys of iterative methods.

### Lecture 18 (Mar 18)

**Handouts**: [Arnoldi-iteration experiments](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Arnoldi.ipynb), [pset 4](pset4-s15.pdf) (due Monday March 30).

Showed that the Ritz (Galerkin) matrix of the Arnoldi process is actually an upper-Hessenberg matrix H whose entries are generated during the Arnoldi algorithm itself.

Lanczos: Arnoldi for Hermitian matrices, in which case H is real-symmetric tridiagonal. Showed that in this case we get a three-term recurrence for the tridiagonal reduction of A. (Derivation somewhat different than in the book. By using A=A\* and the construction of the q vectors, showed explicitly that qj\*v=qj\*Aqn\=0 for j<n-1, and that for j=n gives |v|=βn from the n-th step. Hence Arnoldi reduces to a three-term recurrence, and the Ritz matrix is tridiagonal.)

Noted that Arnoldi requires Θ(mn2) operations and Θ(mn) storage. If we only care about the eigenvalues and not the eigenvectors, Lanczos requires Θ(mn) operations and Θ(m+n) storage. However, this is complicated by rounding problems.

Discussed how rounding problems cause a loss of orthogonality in Lanczos, leading to "ghost" eigenvalues where extremal eigenvalues re-appear. In Arnoldi, we explicitly store and orthogonalize against all qj vectors, but then another problem arises: this becomes more and more expensive as n increases. The solution to this is restarting, discussed in the next lecture.

**Further reading:** Trefethen, lectures 33, 36.

### Lecture 19 (Mar 20)

A solution to the loss of orthogonality in Lanczos and the growing computational effort in Arnoldi is restarting schemes, where we go for n steps and then restart with the k "best" eigenvectors. For k=1 this is easy, but explained why it is nontrivial for k>1: we need to restart in such a way that maintains the Lanczos (or Arnoldi) property that the residual AQn - QnHn is nonzero only in the n-th column (and that column is orthogonal to Qn).

Discussed the implicitly restarted Lanczos method, which does n−k steps of shifted QR to reduce the problem from n to k dimensions. The key thing is that, because the Q matrices in QR on tridiagonal matrices are upper Hessenberg, their product can be shown to preserve the Lanczos property of the residual for the first k columns.

Introduced the **GMRES** algorithm: compute Q as in Arnoldi, but then minimize the residual |Ax-b| in the Krylov subspace using this basis. Briefly discussed a variant of GMRES, the full orthogonalization method (FOM), which solves for **x** in the Krylov space such that the residual **b**−A**x** is orthogonal to the Krylov space (instead of minimizing its norm as in GMRES), in the spirit of Rayleigh-Ritz and Galerkin methods. Discussed theorem (Cullum and A. Greenbaum, 1996) that shows FOM and GMRES to have the same convergence rates until the convergence of GMRES stalls, at which point the FOM residual norm may increase.

**Further reading:** See the section on [implicitly restarted Lanczos](http://www.cs.utk.edu/~dongarra/etemplates/node117.html) in [Templates for the Solution of Algebraic Eigenvalue Problems](http://www.cs.utk.edu/~dongarra/etemplates/book.html). [Cullum (1996)](http://link.springer.com/article/10.1007%2FBF02127693) reviews the relationship between GMRES and FOM and two other iterative schemes. Trefethen, lectures 34, 35, 40. The

### Lecture 20 (Mar 30)

**Handouts:** [pset 4 solutions](pset4sol-s15.pdf)

Discussed the convergence rate of GMRES and Arnoldi in terms of polynomial approximations. Following the book closely, showed that the relative errors (the residual norm for GMRES) can be bounded by minimizing the value p(λ) of a polynomial p(z) evaluated at the eigenvalues, where p(0)=1 and p has degree _n_ after the _n_\-th iteration. (There is also a factor of the condition number of the eigenvector matrix in GMRES, so it is favorable for the eigenvectors to be near-orthogonal, i.e for the matrix to be near-[normal](http://en.wikipedia.org/wiki/Normal_matrix).)

Using this, we can see that the most favorable situation occurs when the eigenvalues are grouped into a small cluster, or perhaps a few small clusters, since we can then make p(λ) small with a low-degree polynomial that concentrates a few roots in each cluster. This meanst that GMRES will achieve small errors in only a few iterations. Morever we can see that a _few_ outlying eigenvalues aren't a problem, since p(z) will quickly attain roots there and effectively eliminate those eigenvalues from the error—this quantifies the intuition that Krylov methods "improve the condition number" of the matrix as the iteration proceeds, which is why the condition-number bounds on the error are often pessimistic. Conversely, the worst case will be when the eigenvalues are all spread out uniformly in some sense. Following examples 35.1 and 35.2 in the book, you can actually have two matrices with very similar small condition numbers but very different GMRES convergence rates, if in one case the eigenvalues are clustered and in the other case the eigenvalues are spread out in a circle around the origin (i.e. with clustered magnitudes |λ| but different phase angles).

Contrasted convergence with Arnoldi/Lanczos. As in the book, showed that Arnoldi also minimizes a polynomial on the eigenvalues, except that in this case the coefficient of the _highest_ degree term is constrained to be 1. (We proceeded somewhat backwards from the book: the book started with polynomial minimization and derived the Rayleigh-Ritz eigenproblem, whereas we went in the reverse direction.) Showed that this set of polynomials is shift-invariant, which explains why (as we saw experimentally) Arnoldi convergence is identical for A and A+μI. This is _not_ true for GMRES, and hence GMRES convergence is not shift-invariant—this is not suprising, since solving Ax=b and (A+μI)x=b can be very different problems.

Like Arnoldi/Lanczos, if GMRES does not converge quickly we must generally **restart** it, usually with a subspace of dimension 1; restarting GMRES repeatedly after k steps is called **GMRES(k)**. Unfortunately, unlike Arnoldi, restarted GMRES is _not guaranteed to converge_. If it doesn't converge, we must do something to speed up convergence:

In many practical cases, unfortunately, the eigenvalues of A are _not_ mostly clustered, so convergence of GMRES may be slow (and restarted GMRES may not converge at all). The solution to this problem is **preconditioning**: finding an easy-to-invert M such that M\-1A has clustered eigenvalues (and is not too far from normal).

**Further reading:** [Cullum (1996)](http://link.springer.com/article/10.1007%2FBF02127693) reviews the relationship between GMRES and FOM and two other iterative schemes. Trefethen, lectures 34, 35, 40. The convergence of GMRES for very non-normal matrices is a complicated subject; see e.g. [this paper on GMRES for defective matrices](http://citeseer.ist.psu.edu/viewdoc/summary?doi=10.1.1.48.1733) or [this paper surveying different convergence estimates](http://eprints.maths.ox.ac.uk/1290/). Regarding convergence problems with GMRES, see this 2002 presentation by Mark Embree on [Restarted GMRES dynamics](http://www.caam.rice.edu/~embree/householder.pdf). [Templates for the Solution of Linear Systems](http://www.netlib.org/linalg/html_templates/Templates.html), chapter on [preconditioners](http://www.netlib.org/linalg/html_templates/node51.html), and e.g. _[Matrix Preconditioning Techniques and Applications](http://books.google.com/books?id=d9UdanCqJ1QC)_ by Ke Chen (Cambridge Univ. Press, 2005).

### Lecture 21 (Apr 1)

Continued to discuss preconditioning: finding an M such that MA (left preconditioning) or AM (right preconditioning) has clustered eigenvalues (solving MAx=Mb or AMy=b with x=My, respectively). Essentially, one can think of M as a crude approximation for A–1, or rather the inverse of a crude approximation of A that is easy to invert. Brief summary of some preconditioning ideas: multigrid, incomplete LU/Cholesky, Jacobi/block-Jacobi. (Since Jacobi preconditioners only have short-range interactions, they tend not to work well for matrices that come from finite-difference/finite-element discretizations on grids, but they can work well for diagonally dominant matrices that arise in spectral and integral-equation methods.)

**Conjugate-gradient (CG) methods:**

Began discussing gradient-based iterative solvers for Ax=b linear systems, starting with the case where A is Hermitian positive-definite. Our goal is the conjugate-gradient method, but we start with a simpler technique. First, we cast this as a minimization problem for f(x)=x\*Ax-x\*b-b\*x. Then, we perform 1d line minimizations of f(x+αd) for some direction d. If we choose the directions d to be the steepest-descent directions b-Ax, this gives the steepest-descent method. Discussed successive line minimization of f(x), and in particular the steepest-descent choice of d=b-Ax at each step. Explained how this leads to "zig-zag" convergence by a simple two-dimensional example, and in fact the number of steps is proportional to κ(A). We want to improve this by deriving a Krylov-subspace method that minimizes f(x) over _all_ previous search directions simultaneously.

Derived the conjugate-gradient method, by explicitly requiring that the n-th step minimize over the whole Krylov subspace (the span of the previous search directions). This gives rise to an orthogonality ("conjugacy", orthogonality through A) condition on the search directions, and can be enforced with Gram-Schmidt on the gradient directions. Then we will show that a Lanczos-like miracle occurs: most of the Gram-Schmidt inner products are zero, and we only need to keep the previous search direction.

**Further reading:** On MINRES and SYMMLQ: [Differences in the effects of rounding errors in Krylov solvers for symmetric indefinite linear systems](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.31.3064) by Sleijpen (2000); see also van der Vorst notes from Lecture 22 and the _Templates_ book. Trefethen, lecture 38 on CG. See also the useful notes, [An introduction to the conjugate gradient method without the agonizing pain](http://www.cs.cmu.edu/~quake-papers/painless-conjugate-gradient.pdf) by J. R. Shewchuk.

### Lecture 22 (Apr 3)

Finished derivation of conjugate gradient, by showing that it reduces to a three-term recurrence.

Discussed convergence of conjugate gradient: useless results like "exact" convergence in m steps (not including roundoff), pessimistic bounds saying that the number of steps goes like the square root of the condition number, and the possibility of superlinear convergence for clustered eigenvalues.

Via a simple analysis of the discretized Poisson's equation in 1d (which easily generalizes to any discretized grid/mesh with nearest-neighbor interactions), argued that the number of steps in unpreconditioned GMRES (and other Krylov methods) is (at least) proportional to the diameter of the grid for sparse matrices of this type, and that this exactly corresponds to the square root of the condition number in the Poisson case. Hence, an ideal preconditioner for this type of matrix really needs some kind of long-range interaction.

### Midterm (Apr 6)

Midterm [exam](midterm-s15.pdf) and [solutions](midtermsol-s15.pdf).

### Lecture 23 (Apr 8)

CG easily generalizes to a simple nonlinear optimization algorithm to (locally) minimize arbitrary twice-differentiable f(x): successive line minimization (for unconstrained local optimization with continuous design parameters), which leads us directly to nonlinear steepest-descent and thence to nonlinear conjugate-gradient algorithms. The key point being that, near a local minimum of a smooth function, the objective is typically roughly quadratic (via Taylor expansion), and when that happens CG greatly accelerates convergence. (Mentioned Polak–Ribiere heuristic to help "reset" the search direction to the gradient if we are far from the minimum and convergence has stalled; see the Hager survey below for many more.)

Outlined application of nonlinear CG to Hermitian eigenproblems by minimizing the Rayleigh quotient (this is convex, and furthermore we can use the Ritz vectors to shortcut both the conjugacy and the line minimization steps). The generalization of this is the [LOBPCG](http://en.wikipedia.org/wiki/LOBPCG) algorithm; discussed some pros and cons compared to Lanczos (basically, LOBPCG is often advantageous if you need several of the smallest eigenvalues, because it avoids ghosts without restarting, and especially if you have a good preconditioner).

### Lecture 24 (Apr 10)

**Handouts:** [summary of options for solving linear systems](solver-options.pdf)

Discussed the polynomial viewpoint in the textbook, which views conjugate gradient (and other algorithms) as trying to find a polynomial that is as small as possible at the eigenvalues. This gives a nice way to think about how fast iterative methods converge and the impact of the eigenvalue spectrum. As with GMRES, the most favorable situation occurs when the eigenvalues are grouped into a small cluster, or perhaps a few small clusters, since we can then make p(λ) small with a low-degree polynomial that concentrates a few roots in each cluster.

Derived the preconditioned conjugate gradient method (showing how the apparent non-Hermitian-ness of M\-1A is not actually a problem as long as M is Hermitian positive-definite). Mentioned the connection to approximate Newton methods (which is easy to see if we consider preconditioned steepest-descent with M approximately A\-1).

**Further reading:** See the textbook, lecture 38, for the polynomial viewpoint, and lecture 40 on preconditioning.

**Biconjugate gradient:** As an alternative to GMRES for non-Hermitian problems, considered the biCG algorithm. Derived it as in the van der Vorst notes below: as PCG on the Hermitian-indefinite matrix B=\[0,A;A\*,0\] with the "preconditioner" \[0,I;I,0\] (in the unpreconditioned case). Because this is Hermitian, there is still a conjugacy condition and it is still a Krylov method. Because it is indefinite, we are finding a saddle point and not a minimum of a quadratic, and _breakdown_ can occur if one of the denominators (e.g. d\*Bd) becomes zero. (This is the same as algorithm 39.1 in Trefethen, but derived very differently.) Because of this, you should almost never use the plain biCG algorithm. However, the biCG idea was the starting point for several "stabilized" refinements, culminating in biCGSTAB(L) that try to avoid breakdown by combining biCG with elements of GMRES. Another algorithm worth trying is the QMR algorithm.

Concluded with some rules of thumb (see handout) about which type of solvers to use: LAPACK for small matrices (< 1000×1000), sparse-direct for intermediate-size sparse cases, and iterative methods for the largest problems or problems with a fast matrix\*vector but no sparsity. One important point is that sparse-direct algorithms scale much better for sparse matrices that come from discretization of 2d PDEs than 3d PDEs. In general, some experimentation is required to find the best technique for a given problem, so software like Matlab or the Petsc library is extremely helpful in providing a quick way to explore many algorithms.

**Further reading:** [Templates for the Solution of Linear Systems](http://www.netlib.org/linalg/html_templates/Templates.html). A very nice overview of iterative methods for non-Hermitian problems can be found in these 2002 [Lecture Notes on Iterative Methods](http://www.math.uu.nl/people/vorst/lecture.html) by Henk van der Vorst (second section, starting with GMRES).

### Lecture 25 (Apr 13)

**Handouts:** [notes on sparse-direct solvers](http://persson.berkeley.edu/18.335/lec20handout6pp.pdf) from Fall 2007; [IJulia notebook on sparse-direct solvers](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Nested-Dissection.ipynb)

**Sparse-direct solvers:** For many problems, there is an intermediate between the dense Θ(m3) solvers of LAPACK and iterative algorithms: for a sparse matrix A, we can sometimes perform an LU or Cholesky factorization while maintaining sparsity, storing and computing only nonzero entries for vast savings in storage and work. In particular, did a Matlab demo, a few experiments with a simple test case: the "discrete Laplacian" center-difference matrix on uniform grids that we've played with previously in 18.335. In 1d, this matrix is tridiagonal and LU/Cholesky factorization produces a bidiagonal matrix: Θ(m) storage and work! For a 2d grid, there are 4 off-diagonal elements, and showed how elimination introduces Θ(√m) nonzero entries in each column, or Θ(m3/2) nonzero entries in total. This is still not too bad, but we can do better. First, showed that this "fill-in" of the sparsity depends strongly on the ordering of the degrees of freedom: as an experiment, tried a _random_ reordering, and found that we obtain Θ(m2) nonzero entries (~10% nonzero). Alternatively, one can find re-orderings that greatly reduce the fill-in. One key observation is that the fill-in only depends on the pattern of the matrix, which can be interpreted as a [graph](http://en.wikipedia.org/wiki/Graph_%28mathematics%29): m vertices, and edges for the nonzero entries of A (an [adjacency matrix](http://en.wikipedia.org/wiki/Adjacency_matrix) of the graph), and sparse-direct algorithms are closely related to graph-theory problems. For our simple 2d Laplacian, the graph is just the picture of the grid connecting the points. One simple algorithm is the [nested dissection algorithm](http://en.wikipedia.org/wiki/Nested_dissection): recursively find a separator of the graph, then re-order the vertices to put the separator last. This reorders the matrix into a mostly block-diagonal form, with large blocks of zeros that are preserved by elimination, and if we do this recursively we greatly reduce the fill-in. Did a crude analysis of the the fill-in structure, resulting in the time/space complexity on the last page of the handoutw, for our 2d grid where separators are obvious; for more general matrices finding separators is a hard and important problem in graph theory.

**Further reading:** A [survey of nested-dissection algorithms](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.58.9722) (Khaira, 1992). List of [sparse-direct solver software](http://www.cs.utk.edu/~dongarra/etemplates/node388.html) by Dongarra and [another list by Davis](http://www.cise.ufl.edu/research/sparse/codes/). [Notes on multifrontal sparse-direct methods](http://www.cse.illinois.edu/courses/cs598mh/gupta.ps) by M. Gupta (UIUC, 1999). The book _[Direct Methods for Sparse Linear Systems](http://books.google.com/books?id=TvwiyF8vy3EC&lpg=PR1&ots=odauEC2c4k&dq=direct%20methods%20for%20sparse%20davis&pg=PR1#v=onepage&q&f=false)_ by Davis is a useful reference. Outside of Matlab, a popular library to help you solve spare problems is [PETSc](http://www.mcs.anl.gov/petsc/petsc-as/).

### Lecture 26 (Apr 15)

**Handouts:** [overview of optimization](optimization-handout.pdf) ([full-page slides](optimization.pdf))

Several of the iterative algorithms so far have worked, conceptually at least, by turning the original linear-algebra problem into a minimization problem. It is natural to ask, then, whether we can use similar ideas to solve more general **optimization problems**, which will be the next major topic in 18.335.

Broad overview of optimization problems (see handout). The most general formulation is actually quite difficult to solve, so most algorithms (especially the most efficient algorithms) solve various special cases, and it is important to know what the key factors are that distinguish a particular problem. There is also something of an art to the problem formulation itself, e.g. a nondifferentiable minimax problem can be reformulated as a nicer differentiable problem with differentiable constraints.

### Lecture 27 (Apr 17)

**Handouts:** [notes on adjoint methods](http://math.mit.edu/~stevenj/18.336/adjoint.pdf) to compute gradients; [notes on adjoint methods for recurrence relations](http://math.mit.edu/~stevenj/18.336/recurrence2.pdf); [adjoint example notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/Adjoint-method.ipynb)

Introduction to **adjoint** methods and the remarkable fact that one can compute the gradient of a complicated function with about the same number of additional operations as computing the function _once_.

### Lecture 28 (Apr 22)

**Handouts:** [notes on adjoint methods for recurrence relations](http://math.mit.edu/~stevenj/18.336/recurrence2.pdf); see pages 1–10 of [Svanberg (2002) paper on CCSA algorithms](
http://dx.doi.org/10.1137/S1052623499362822)

Adjoint methods for recurrence relations, following notes.

Discussed some general concepts in local optimization. **Global convergence** means convergence to a _local_ optimum from any _feasible_ starting point; explained why finding the feasible region from an _infeasible_ starting point is in general as hard as global optimization. A typical **trust region** approach is to _locally approximate_ the objective and constraint functions by some _simple functions_ that are easy to optimize, optimize them within some localized trust region around a current point **x** to obtain a candidate step **y**, and then either take the step (e.g. if **y** is an improvement) and/or update the approximations and trust region (e.g. if **y** was not an improvement or the approximation and exact functions differed greatly). There are many, many algorithms that follow this general outline, but they differ greatly in what approximations they use (e.g. linear, quadratic, ...), what trust region they use, and what methods they use to update the trust region and to evaluate candidate steps. Often, the approximate functions are _convex_ so that convex-optimization methods can be used to solve the _trust-region subproblems_.

Start discussing a particular example of a nonlinear optimization scheme, solving the full inequality-constrained nonlinear-programming problem: the CCSA and MMA algorithms, as refined by Svanberg (2002). This is a surprisingly simple algorithm (the [NLopt](http://ab-initio.mit.edu/nlopt) implementation is only 300 lines of C code), but is robust and provably convergent, and illustrates a number of important ideas in optimization: optimizing an approximation to update the parameters **x**, guarding the approximation with trust regions and penalty terms, and optimizing via the dual function (Lagrange multipliers). Like many optimization algorithms, the general ideas are very straightforward, but getting the details right can be delicate!

Outlined the inner/outer iteration structure of CCSA, and the interesting property that it produces a sequence of feasible iterates from a feasible starting point, which means that you can stop it early and still have a feasible solution (which is very useful for many applications where 99% of optimal is fine, but feasibility is essential).

### Lecture 29 (Apr 24)

Started by reviewing the basic idea of Lagrange multipliers to find an extremum of one function f0(x) and one equality constraint h1(x)=0. We instead find an extremum of L(x,ν1)=f0(x)+ν1h1(x) over x and the _Lagrange multiplier_ ν1. The ν1 partial derivative of L ensures h1(x)=0, in which case L=f0 and the remaining derivatives extremize f0 along the constraint surface. Noted that ∇L=0 then enforces ∇f0\=0 in the direction parallel to the constraint, whereas perpendicular to the constraint ν1 represents a "force" that prevents x from leaving the h1(x)=0 constraint surface.

Generalized to the Lagrangian L(x,λ,ν) of the general optimization problem (the "primal" problem) with both inequality and equality constraints, following chapter 5 of the Boyd and Vandenberghe book (see below) (section 5.1.1).

Described the KKT conditions for a (local) optimum/extremum (Boyd, section 5.5.3). These are true in problems with strong duality, as pointed out by Boyd, but they are actually true in much more general conditions. For example, they hold under the "LICQ" condition in which the gradients of all the active constraints are linearly independents. Gave a simple graphical example to illustrate why violating LICQ requires a fairly weird optimum, at a cusp of two constraints.

**Further reading:** _[Convex Optimization](http://www.stanford.edu/~boyd/cvxbook/)_ by Boyd and Vandenberghe (free book online), chapter 5. There are many sources on [Lagrange multipliers](http://en.wikipedia.org/wiki/Lagrange_multipliers) (the special case of equality constraints) online that can be found by googling.

### Lecture 30 (Apr 27)

Defined the Lagrange dual function g(λ,ν) (Boyd, section 5.1.2) and proved weak duality of the dual problem (sections 5.1.3, 5.2, 5.2.2). Commented on strong duality (5.2.3), which is mostly true/useful in convex problems (Slater's condition). Defined the notation x\* etcetera for the optimum, as in Boyd.

Explained how to solve the convex subproblem from the CCSA (Svanberg, 2001) method (see lecture 29) using duality. We reduce it to a dual problem with only bound constraints on the dual variables, and then do CCSA recursively to obtain a dual problem with no variables at all (trivially solvable).

CCSA uses only the function value and gradient information from the current step, discarding the gradients from the previous steps; in that sense, it is similar in spirit to steepest-descent algorithms or successive LP approximations. More sophisticated algorithms, converging faster near the minimum, will also use (implicit or explicit) second-derivative information. This leads us to Newton and quasi-Newton methods.

Began discussing quasi-Newton methods in general, and the BFGS algorithm in particular. Motivated the problem: we want to construct a sequence of quadratic approximations for our objective function, and optimize these to obtain Newton steps in our parameters. Discussed backtracking line searches to ensure that the Newton step is a sufficient improvement. Discussed difficulty of using exact quadratic model (exact Hessian matrix) in general.

Discussed how quasi-Newton methods are used: they are used to generate not really a step (since the Newton step may be way off if the function is not near the minimum) but rather a direction for a line search.

### Lecture 31 (Apr 29)

**Handouts:** [pset 5](pset5-s15.pdf) (due Mon May 11).

Outlined four desirable properties of approximate Hessian matrix: positive definiteness, convergence to exact Hessian for quadratic objectives, multiplying it by the change in _x_ should give the change in the gradient for the most recent step (the "secant condition"), and it should have as much "memory" as possible (minimizing the change to the Hessian or its inverse in some norm).

Following Greenstadt (1970), outlined how minimizing the change in the inverse Hessian, in a weighted Frobenius norm, subject to the secant condition and a symmetry constraint, is a QP that can be explicitly solved via the dual problem. This leads to a nice formula involving two rank-1 updates, which is especially nice if a convenient weight is chosen. You will derive this in homework.

Gave BFGS update formula, and explained how the update for the approximate inverse Hessian can be transformed into a similar update for the Hessian, using the [Sherman-Morrison](https://en.wikipedia.org/wiki/Sherman%E2%80%93Morrison_formula) formula for rank-1 updates. Briefly derived this formula.

From the BFGS update formula, and showed that it satisfies at least positivity. With the help of the [Cauchy-Schwarz inequality](https://en.wikipedia.org/wiki/Cauchy%E2%80%93Schwarz_inequality), reduced the problem of proving positive-definiteness to showing that the dot product γTδ of the change in gradient (γ) with the change in _x_ (δ) must be positive.

Discussed exact vs. approximate line searches (ala Nocedal, 1980). Explained why an exact line search leads to positive γTδ and hence positive-definite approximate Hessians, and why an approximate line-search can usually be defined to enforce this (cf. [Wolfe conditions](http://en.wikipedia.org/wiki/Wolfe_conditions))...and what to do when this doesn't happen.

Briefly discussed the limited-memory BFGS algorithm, and applications to sequential quadratic programming (SQP).

**Further reading:** Wikipedia's articles on [quasi-Newton methods](http://en.wikipedia.org/wiki/Quasi-Newton_methods) and the [BFGS method](http://en.wikipedia.org/wiki/BFGS_method) have some useful links and summaries. Helpful derivations of many of the properties of BFGS updates, and many references, can be found in [this 1980 technical report by Dennis and Schnabel](http://www.cs.colorado.edu/department/publications/reports/docs/CU-CS-185-80.pdf) and for a generalization in [this 1994 paper by O'Leary and Yeremin](http://www.cs.umd.edu/~oleary/reprints/j39.pdf), for example. A nice derivation of the minimum-norm change property (or rather, a derivation of the BFGS update formula from this property), can be found in Greenstadt, _Math. Comp._ **24**, pp. 1–22 (1970).

### Lecture 32 (May 1)

Introduced derivative-free optimization algorithms, for the common case where you don't have too many parameters (tens or hundreds) and computing the gradient is inconvenient (complicated programming, even if adjoint methods are theoretically applicable) or impossible (non-differentiable objectives). Started by discussing methods based on linear interpolation of simplices, such as the COBYLA algorithm of Powell.

Discussed derivative-free optimization based on quadratic approximation by symmetric Broyden updates (as in BOBYQA/NEWUOA algorithm of Powell, for example). Updating the Hessian turns into a quadratic programming (QP) problem, and discussed solution of QPs by construction of the dual, turning it into either an unconstrained QP (and hence a linear system) for equality constrained problems, or a bound-constrained QP for inequality-constrained QPs.

Briefly discussed global optimization (GO). For general objectives, there are no "good" GO algorithms; it is easy to devise an objective for which GO is arbitrarily hard (the problem is NP-hard in general). Many (but not all) GO algorithms have a proof (often trivial) that they converge to the global optimum asymptotically, but little can be said about how _fast_ they converge, and in general there is no way to know when the global optimum has been found—stopping criteria for global optimization tend to be "stop when the design is good enough" or "stop when you run out of patience". In high dimensions, GO is often hopeless unless you have a function that is very "nice" (has only a few local optima). There are a few categories of GO algorithms, depending on how they perform the _global_ and _local_ portions of their search.

_Stochastic global & local search:_ Algorithms like genetic algorithms, simulated annealing, and so on, typically rely on randomized algorithms for both exploring the global search space and for refining local optimum. These algorithms are easy to implement, assume little or nothing about the objective, are easy to parallelize, and have evocative natural analogies. As a result, they perhaps have a disproportionate mind share: they should often be treated as **methods of last resort**, because they don't exploit any mathematical structure of the objective (e.g. smoothness or even continuity).*   _Stochastic global & deterministic local search:_ The typical algorithm in this category is a "multistart" algorithm: perform repeated local optimizations from randomized starting points. This sort of algorithm can take advantage of very efficient local optimizers, especially if you have a differentiable function and the gradient is available. On the other hand, effective use often requires some tweaking to choose the stopping criteria of the local search, and the algorithms will often search the same local optimum many times. One attempt to deal with the latter problem is the MLSL algorithm, which is a multistart algorithm with a "filter" to prevent repeated searches of the same optimum (the filtering rule for starting points is not perfect, but it provably leads to each optimum being searched a finite number of times asymptotically).
*   _Deterministic global & local search:_ These are typically "branch-and-bound" algorithms that systematically divide up the search domain and search the whole thing. For a black-box objective, one must asymptotically search the entire domain, but heuristics can be used to identify which subregions to search first, and a typical algorithm of this sort is DIRECT. Given more knowledge of the objective function, one can ideally devise a method to compute a _lower bound_ of the objective in each subregion, and in this way subregions can be eliminated from the search if their lower bound is above the best value found so far. A typical tool to construct such bounds is Taylor arithmetic, e.g. via the COSY INFINITY software. A typical example of branch-and-bound GO software based on analytical lower bounds is the BARON program.

**Further reading:** The book [Introduction to Derivative-Free Optimization](http://books.google.com/books?id=7c7X6tlcaHEC&lpg=PP1&ots=ljSCrl3WuI&dq=derivative%20free%20optimization%20conn&pg=PP1#v=onepage&q&f=false) by Andrew Conn et al is a reasonable starting point. See also the [derivative-free algorithms in NLopt](http://ab-initio.mit.edu/wiki/index.php/NLopt_Algorithms) and the references thereof.

### Lecture 33 (May 4)

**Handout:** [Notes](http://math.mit.edu/~stevenj/trap-iap-2011.pdf) on error analysis of the trapezoidal rule and Clenshaw-Curtis quadrature in terms of Fourier cosine series, and a [quick review of cosine series](http://math.mit.edu/~stevenj/cosines.pdf).

New topic: **numerical integration** (numerical quadrature). Began by basic definition of the problem (in 1d) and differences from general ODE problems. Then gave trapezoidal quadrature rule, and simple argument why the error generally decreases with the square of the number of function evaluations.

Showed numerical experiment (see handout) demonstrating that sometimes the trapezoidal rule can do much better than this: it can even have exponential convergence with the number of points! To understand this at a deeper level, I analyze the problem using Fourier cosine series (see handout), and show that the error in the trapezoidal rule is directly related to the convergence rate of the Fourier series. Claimed that this convergence rate is related to the smoothness of the periodic extension of the function, and in fact an analytic periodic function has Fourier coefficients that vanish exponentially fast, and thus the trapezoidal rule converges exponentially in that case. Proved by integration by parts of the Fourier series. In fact, we find that only the _odd_\-order derivatives at the endpoints need to be periodic to get accelerated convergence.

### Lecture 34 (May 6)

**Handout:** [Clenshaw–Curtis quadrature](http://en.wikipedia.org/wiki/Clenshaw%E2%80%93Curtis_quadrature) from Wikipedia (mostly written by SGJ as of May 2015, so I can vouch for its accuracy \[or I am responsible for its inaccuracy\]).

Explained the idea of Clenshaw–Curtis quadrature as a change of variables + a cosine series to turn the integral of _any_ function into the integral of periodic functions. This way, functions only need to be analytic on the interior of the integration interval in order to get exponential convergence. (See Wikipedia handout.)

Also explained (as in the handout) how to precompute the weights in terms of a discrete cosine transform, rather than cosine-transforming the function values every time one needs an integral, via a simple transposition trick.

Discussed the importance of nested quadrature rules for _a posteriori_ error estimation and adaptive quadrature. Discussed p-adaptive vs. h-adaptive adaptive schemes.

**Further reading**: Lloyd N. Trefethen, "[Is Gauss quadrature better than Clenshaw-Curtis?](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.157.4174)," _SIAM Review_ **50** (1), 67-87 (2008). Pedro Gonnet, [A review of error estimation in adaptive quadrature](http://dl.acm.org/citation.cfm?id=2333117), _ACM Computing Surveys_ **44**, article 22 (2012).

### Lecture 35 (May 8)

Explained connection of Clenshaw-Curtis quadrature and cosine series to Chebyshev polynomials. This leads into the general topic of Chebyshev approximation, and how we can approximate any smooth function on a finite interval by a polynomial with exponential accuracy (in the degree of the polynomial) as long as we interpolate via Chebyshev points.

Using Chebyshev approximation, explained how lots of problems can be solved by first approximating a nasty function via a polynomial, at which point one can just use easy methods for polynomials. Showed examples of root finding, minimization, integration, and solving ODEs via the [ApproxFun](https://github.com/ApproxFun/ApproxFun.jl) package for Julia, which implements these ideas (following in the tracks of the pioneering [chebfun](http://www.chebfun.org/) package for Matlab).

**Further reading**: [Chebyshev polynomials on Wikipedia](http://en.wikipedia.org/wiki/Chebyshev_polynomials), free book online [Chebyshev and Fourier Spectral Methods](http://www-personal.umich.edu/~jpboyd/BOOK_Spectral2000.html) by John P. Boyd, the [chebfun package](http://www2.maths.ox.ac.uk/chebfun/) for Matlab by Trefethen et al.,

### Lecture 36 (May 11)

**Handout:** [notes on FFTs](fft-iap3.pdf), [pset 5 solutions](pset5sol-s15.pdf) and [notebook](http://nbviewer.ipython.org/url/math.mit.edu/~stevenj/18.335/pset5sol-s15.ipynb)

Overview of fast Fourier transform (FFT) algorithms, and in particular derived the Cooley-Tukey algorithm and analyzed its complexity. Briefly commented on the existence of O(N log N) FFT algorithms for prime sizes and gave the example of [Rader's algorithm](https://en.wikipedia.org/wiki/Rader%27s_FFT_algorithm).

**Further reading:** [notes on FFTs](fft-iap3.pdf) and references therein. The Wikipedia page on [fast Fourier transforms](https://en.wikipedia.org/wiki/Fast_Fourier_transform) is reasonably accurate and links to descriptions of many algorithms (largely written by SGJ).

### Lecture 37 (May 13)

**Handout:** [slides on FFTs and FFTW](FFTW-Alan-2008.pdf)