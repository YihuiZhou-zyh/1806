# MIT Course 18.06, Spring 2022

This is a repository for the course [18.06: Linear Algebra](http://web.mit.edu/18.06) at MIT in Spring 2022.   See [other branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/viewing-branches-in-your-repository) of this repository for previous semesters.

**Instructor**: [Prof. Steven G. Johnson](http://math.mit.edu/~stevenj).

**Lectures**: MWF11 in 10-250.  See [recordings](https://mit.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx?folderID=68796547-c661-4d78-a50e-ae2e00efcbba) and [handwritten notes](https://www.dropbox.com/s/q6ff0kfu7jyjiuz/18.06%20Spring%202022.pdf?dl=0) posted online, along with other materials (slides, further reading) posted below.

**Exams**: 11am in 10-250, on Fridays **2/25**, **4/1**, and **5/6**.  Final exam: 9–12 in 10–250 on Wednesday **5/18**.

**Recitations**:
 * [Gary Choi](https://math.mit.edu/~ptchoi/): T2 in 2-136, T3 in 2-136 (office hours W10 [virtual](https://mit.zoom.us/j/99599310644), R11 in-person 2-246C)
 * [Haushuo Fu](https://math.mit.edu/directory/profile.php?pid=2229): T11 in 2-136, T12 in 2-136 (office hours M4 [virtual](https://mit.zoom.us/j/99599310644), W1 in-person 2-238)
 * [Sergei Korotkikh](https://math.mit.edu/directory/profile.php?pid=2113): T11 in 2-131, T1 in 2-136 (office hours W6 [virtual](https://mit.zoom.us/j/99599310644), R6 in-person 2-231D)
 * [Yair Shenfeld](https://www.yairshenfeld.com/): T9 in 2-132, T10 in 2-132 (office hours T4 [virtual](https://mit.zoom.us/j/99599310644), R5 in-person 2-231)

**Undergraduate Assistants**: [Subha Pushpita](https://snpushpi.mit.edu/), Isaac M Lopez, and Gaurav Arya.   Email them at **1806sp22_ua ατ mit.edu** for 1-on-1 technical help with Julia or other questions that don't work well over Piazza etc.   [Virtual](https://mit.zoom.us/j/99599310644) office hours: M7, T5:30, F1–3.

**Resources**: [Piazza discussion forum](https://piazza.com/mit/spring2022/1806), [math learning center](https://math.mit.edu/learningcenter/), [TSR^2 study/resource room](https://ome.mit.edu/programs/talented-scholars-resource-room-tsr2), [pset partners](https://psetpartners.mit.edu/).

This document is a *brief* summary of what was covered in each 18.06
lecture, along with links and suggestions for further reading.  It is
*not* a good substitute for attending lecture, but may provide a
useful study guide.  (You can also look at the analogous summaries from [Fall 2018](https://github.com/stevengj/1806/blob/fall18/summaries.md).)

## Lecture 1 (Jan 31)

* [course overview/syllabus](https://docs.google.com/presentation/d/1ivbV1nr67XfasBdXezZF9UWILzDoQtQev8vSqRKBfu0/edit?usp=sharing)
* [pset 0](psets/pset0.ipynb): due **Friday Feb 4 at 11am** (submit your solutions on Canvas).
* video: see *recordings* link above.

Slides giving the syllabus and the "big picture" of what 18.06 is about.  Introduction to thinking about matrices as linear operations, not just as "bags of numbers".

**Further reading**: Strang, chapter 1, and section 8.1 on linear transformations.  3blue1brown has a nice video on [matrix multiplication as composition of linear transformations](https://youtu.be/XkY2DOUCWMU).  If you've forgotten the basics of how to multiply matrices by vectors or matrices by matrices, google for some tutorial material online (e.g. [Khan academy](https://www.khanacademy.org/math/precalculus/x9e81a4f98389efdf:matrices/x9e81a4f98389efdf:multiplying-matrices-by-matrices/a/multiplying-matrices)) and do a quick brush-up.

## Lecture 2 (Feb 2)

* handwritten notes: see link above (at beginning)
* Gaussian-elimination [Julia notebook](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Gaussian-elimination.ipynb)

(Started with quick review of matrix–matrix multiplication from the end of lecture 1.)

[Gaussian
elimination](https://en.wikipedia.org/wiki/Gaussian_elimination) for **Ax=b**:  I
started with the grade-school/high-school viewpoint of writing out three equations
in three unknowns, adding/subtracting multiples of equations until we
were left with one equation in one unknown.  Then, I wrote the
same equations in matrix form, and renamed this process "Gaussian
elimination": we add/subtract multiples of matrix rows to introduce
zeros below the diagonal, i.e. to make the matrix [upper
triangular](https://en.wikipedia.org/wiki/Triangular_matrix) **U**.  We then do the same row operations to the right hand side **b** to get a new vector **c**.  Finally, we solve **Ux=c** for x by working from bottom (1 equation in 1 variable) to top, a process called "backsubstitution".

To do the same operations to both **A** and **b**, a useful trick for hand calculations is to [augment](https://en.wikipedia.org/wiki/Augmented_matrix) the matrix with a new column representing the right-hand side, forming **[A b]** before starting Gaussian elimination.

What comes next?  The problem with expressing Gaussian elimination this way, as operations on individual numbers in the matrix, is that it is impossible to follow the process in detail for anything except a very tiny matrix.   We need a higher-level "algebraic" way to express the process, both to help us understand it and also to help us to *use* it (e.g. to perform additional algebraic transformations afterwards).   To do this, we want to express the process, not as operations on individual numbers, but as matrix operations.

Rewrote Gaussian elimination in matrix form: we multiply a matrix A on the *left* by a sequence of **lower**-triangular "elimination matrices" Eₙ to arrive at an **upper**-triangular matrix U = EA.  To solve Ax=b, we can think of the earlier process as multiplying *both sides* on the *left* by **E**, the linear operator representing the composition (product) of all of the elimination steps, yielding Ux=EAx on the left and c=Eb on the right.

**Further reading:** Textbook sections 2.1, 2.2, 2.3.  Strang [lecture 2 video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=3).

## *Optional* Julia Tutorial (Feb 2 @ 5pm): [Zoom](https://mit.zoom.us/j/92693276240?pwd=TmhwQmRWcmJWVm51eTQ4Szg4cWI4dz09)

* [video recording](https://mit.zoom.us/rec/share/w7o2TQjDOnHsaRlJvbS1iysu5Sh23gGVFt3nX_VShRoRBr5UCsPlMhEu1EeyQrk.Vq1WOfArkC3v-Lma?startTime=1643839179000)

A basic overview of the Julia programming environment for numerical computations that we will use in 18.06 for simple computational exploration.   This (Zoom-based) tutorial will cover what Julia is and the basics of interaction, scalar/vector/matrix arithmetic, and plotting — we'll be using it as just a "fancy calculator" and no "real programming" will be required.

* [Tutorial materials](https://github.com/mitmath/julia-mit) (and links to other resources)

If possible, try to install Julia on your laptop beforehand using the instructions at the above link.  Failing that, you can run Julia in the cloud (see instructions above).

## Lecture 3 (Feb 4)

* handwritten notes
* [Matrix inverse and LU notebook](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Inverses-LU-intro.ipynb)
* [pset 0 solutions](psets/pset0sol.ipynb)
* [pset 1](psets/pset1.ipynb) (due Feb 11)

Showed that Gaussian elimination can be viewed as **LU factorization**:

* Gaussian elimination A ⟿ U=EA (without row swaps) can be thought of as A=LU: factorizing A into a **product of two simpler (triangular) matrices** (L=lower, U=upper).  U is the matrix that you normally get when you do elimination by hand, and L (the inverse of the elimination steps L=E⁻¹, a lower-triangular matrix with 1's on the diagonal) is essentially a *"record" of the elimination steps*.

L is the matrix that "reverses" Gaussian elimination: it tells you how to get A back from L.   Despite this, I showed in lecture that L is actually *easier* to get than E: all you do is make a diagonal matrix of 1's, and then fill in the *multipliers* from the elimination steps (flipping subtraction to addition) below the diagonal.  So, L just requires bookkeeping, and *no* computation.

Computing U is hard (elimination is a lot of work, even for a computer), but once you have U and L then many things that you might want to do with A become easy.

* For example, suppose you want to solve Ax=b, given A=LU.  Write LUx=b=L(Ux), and let y=Ux.  Then Ly=b, and we can solve for y by forward-substitution.  Given y, we can then solve Ux=y by back-substitution.  Both of these steps are easy because the systems are triangular.
  - Moreover, solving Ly=b turns out to *exactly* correspond to applying the elimination steps from A ⟿ U to b.   (The 1's on L's diagonal mean that there are no divisions required, either.)
* This means that we can re-use L and U to solve Ax=b for *many right-hand sides*.   In contrast, if you "augment" A with b and then do elimination (A|b)⟶(U|y), you get the *same* new right-hand side y but you haven't kept a record of the elimination steps, so if you have a new right-hand side you might naively repeat the whole elimination process (hard!) rather than solving Ly=b (easy!).
* More generally, whenever you have A as a product of "simpler" matrices (e.g. triangular, diagonal, …), you can solve Ax=b by a sequence of "simpler" solves.

Introduction to the concept of a matrix inverse more generally as the matrix that reverses the action of a linear operator.  Key ideas from the notebook:

* A⁻¹ is the matrix that does the "reverse" of A:  A⁻¹(Ax)=x for any x.   It also follows that A is the reverse of A⁻¹: A(A⁻¹x)=x for any x, i.e. (A⁻¹)⁻¹=A.
   -  That is, if Ax=b, then A⁻¹b=x (for any x).  (Equivalently, it gives the solution to Ax=b.)
   - It only exists for **square, nonsingular** matrices A.  (i.e. an m×m matrix A must give m nonzero pivots when you do elimination.)
* Equivalently, A⁻¹ is the matrix for which A⁻¹A = A⁻¹A = I (the m×m identity matrix).
  - I is an identity matrix, the matrix that gives Ix=x for any x or IA=A and AI=A for any A.  There are m×m identity matrices for all m, and when we write "I" we usually infer from context how big an I we mean.

In the next lecture (which will start with the end of this notebook), we will look at calculating inverses more generally (although it turns out that this is something that you should almost never do explicitly, even on a computer!).

**Further reading:** Textbook sections 2.5, 2.6.  Strang [lecture 4 video](https://www.youtube.com/watch?v=5hO3MrzPa0A) and [lecture 3 video](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-3-multiplication-and-inverse-matrices/).  See also "The key reason why A = LU" in section 2.6 of the textbook.


## Lecture 4 (Feb 7)

* handwritten notes
* [Matrix inverse and Gauss–Jordan](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Gauss-Jordan.ipynb)

Reviewed matrix inverses and key properties thereof.

Went through how to explicitly compute A⁻¹ by solving AA⁻¹ = I.   Essentially, this is just solving Ax=b multiple times, where b is each column of I. A common way to organize this for *hand* calculation (ugh) is the Gauss–Jordan algorithm (on a 3×3 example that can also be found in the textbook): If we do row operations on A to get I, then the *same* row operations on I give A⁻¹!  To carry this out by hand, we augment (A|I), do ordinary Gaussian elimination to get (U|C), and then do elimination "upwards" to get (I|A⁻¹).

Matrix inverses are mainly a *conceptual* tool that we use to move matrices around *symbolically* in equations.   Once you are through with your algebraic manipulations, you might end up with an expression like A⁻¹b — but when it comes time to actually *compute* the answer, you should **read "A⁻¹b" as "solve Ax=b for x by the best available method"**.

**Further reading:** Textbook sections 2.5, 2.6.  Strang [video lecture 3](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-3-multiplication-and-inverse-matrices/).

## Lecture 5 (Feb 9)

* Handwritten notes
* [LU factorization for real](https://nbviewer.org/github/mitmath/1806/blob/master/notes/LU-for-real.ipynb)

Brief review of previous topics in LU factorization with some more examples in the notebook:

* How the L matrix entries are just the multipliers from Gaussian elimination.  No extra work is required!
* How in practice, one rarely "augments" the matrix with the right-hand side.  Instead, you compute A=LU, substitute this into Ax=b=LUx, let c=Ux, solve Lc=b, then solve Ux=c.  In particular, solving Lc=b is *exactly* the same as performing the Gaussian-elimination steps on c.  (The "augmented" method is a little easier for human bookkeeping, but has essentially no advantage for the computer.)

Some new information about LU to complete the story:

* Given A=LU, you can efficiently solve multiple right-hand sides, or equivalently the **matrix equation** AX=B.
* How row swaps lead to the factorization PA=LU: in practice, the computer *almost always* does row swaps, and *always* gives you a permutation matrix P (or its equivalent).

We apply PA=LU to Ax=b in much the same way as for LU; the only difference is that we have to first apply the permutation P to b.

Permutation matrices P are a great example of a linear operator that is often easier to understand (and more efficient) if you *don't* write it as a matrix, but instead write it as a "vector" `p` of the permuted indices 1…n in the new order.  Then Px is just `x[p]` in Julia (and very similarly in Matlab and Numpy): just make a new vector by extracting the components p₁,p₂,… of x.

**Further reading:** Textbook sections 2.7 (on permutations; we will talk about transposes soon), and 11.1.  Strang [video lecture 4](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-4-factorization-into-a-lu/) and [video lecture 5](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-5-transposes-permutations-spaces-r-n/).   For 18.06, I *don't expect you to know* the details of how the permutation P in PA=LU is constructed even though you don't know the permutation in advance … you only need to know how to *use* PA=LU if it (or something similar) is *given* to you … but if you are interested this "partial pivoting" algorithm is described in lecture 21 of *Numerical Linear Algebra* by Trefethen and Bau, or in many other textbooks on numerical linear algebra.


## Lecture 6 (Feb 11)

* handwritten notes
* [Computational complexity](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Complexity.ipynb)
* [Singular matrices and rank](http://nbviewer.jupyter.org/github/stevengj/1806/blob/fall18/lectures/Singular.ipynb)
* [pset 1 solutions](https://github.com/mitmath/1806/blob/master/psets/pset1sol.ipynb)
* [pset 2](psets/pset2.ipynb)

Complexity of matrix operations: why matrix × vector or backsubstitution scale like n² for n×n matrices, while matrix × matrix or Gaussian elimination (LU factorization) scale like n³.   Matrices much bigger than a few thousand square quickly become impractical, and really large problems are only tractable because they have special structure like [sparsity](https://en.wikipedia.org/wiki/Sparse_matrix).

Began talking about singular matrices.  With a relatively simple example, showed that singular matrices (matrices with not enough pivots) A can still have solutions to Ax=b, but only for certain right hand sides.  And when they do have solutions, they have *infinitely many* solutions.
As a measure of *how* singular a matrix is, we talk about its **rank r**, equal to the number of pivots that we have after elimination.   It will turn out that this number **r** is closely related to the *geometry* of solutions to singular (and non-square) matrix problems.   The solvable right-hand sides live in "**r** dimensions", a *subspace* of all possible right-hand sides — in our example, we had r=2 for a 3×3 matrix, so the allowed right-hand sides lived in a 2d *plane*.   And if the solutions exist to an n×n system with rank r, then we will see that the solutions "live" in n–r dimensions, e.g. a 1d line in our example.

To make this precise, we first have to go back and generalize our notion of a "vector" to a more abstract notion called a "vector space", and from this we can define "subspaces", and see how certain key subspaces related to a matrix A tell us the geometry of its solutions.

**Further reading:** Textbook sections 2.6 ("The cost of elimination") and 11.1.   For next time, textbook sections 3.1 and 3.2.

## Lecture 7 (Feb 14)

* Handwritten notes

Introduced **vector spaces** (informally, a set V of anything you can add x±y and multiply by scalars αx) and **subspaces** (a subset of V such that vector operations *stay in the subspace*).  Examples of vector spaces include real n-component vectors (ℝⁿ, or ℂⁿ for complex numbers), real m×n matrices, functions f(x) (ℝ↦ℝ, real numbers to real numbers).  Examples of subspaces includes planes or lines through the origin in ℝ³, or the origin itself.   The goal of this is to break vector spaces into smaller pieces that we can still do linear algebra on (hence the need for a subspace, not just any arbitrary subset).  Subspaces are especially important to help us understand the solutions (if any) of Ax=b for **non-square** matrices A.

For an m×n matrix A, introduced two important subspaces.

* First, the **column space C(A)**: the set {Ax for all x ∈ ℝⁿ}.  This is the set of *right-hand sides* b such that Ax=b is *solvable*, and is a subspace of the "output space" ℝᵐ (not ℝⁿ unless m=n!).  Equivalently, C(A) is all linear combinations of the *columns* of A, which we call the **span** of the columns.

* Second, the **null space N(A)** (also called the "kernel"): the set {x such that Ax=0} ⊆ ℝⁿ (i.e., a subspace of the "input space" ℝⁿ).  Given any solution x to Ax=b, then x+z is also a solution if z ∈ N(A) (i.e. Az=0 ⟹ A(x+z)=Ax+Az=Ax=b).

These are very important subspaces because they tell us a lot about the matrix A and solutions to Ax=b.  As a trivial example, if A is an n×n *invertible* matrix, C(A)=ℝⁿ and N(A)={0}.  Conversely, if A is an m×n matrix of zeros, then C(A)={0} and N(A)=ℝⁿ.

Defined a **basis** for a vector space as a *minimal* set of vectors (we will later say that they have to be *linearly independent*) whose
**span** (all linear combinations) produces everything in the space.

We can solve Ux=0 by breaking up x=(p,f) into the pivot variables p and the free variables f, and solve for p from f, and in fact this is an upper-triangular solve that we can do by backsubstitution.  This means that we can choose *any f we want* and *p is determined*.   If we choose the usual basis (1,0,0,…), (0,1,0,…) for f∈ℝⁿ⁻ʳ and solve for p, this gives us the **special solutions**, a basis for N(A).

Showed that the **nullspace is preserved by elimination (row) operations**, but that the column space is not.   So, to find N(A), we can instead do elimination and find N(U)=N(A) for the upper-triangular form U.   Defined the **rank** as the number of (nonzero) pivots, the pivot columns, and the free columns.  We now want to find *all* possible solutions to Ax=0.

**Further reading:** Textbook, sections 3.1—3.3; Strang [video lecture 6](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-6-column-space-and-nullspace/) and [lecture 7](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-7-solving-ax-0-pivot-variables-special-solutions/).   Note that Strang's lectures and book emphasize the "reduced row echelon" ("rref") form, which is essentially a bookkeeping trick (similar to Gauss–Jordan for inverses) to do the back-solves for the special solutions all at once.  I will *not* emphasize rref form this semester, but you can use it if you want.  (In practical applications, rref form is virtually never used, and for that matter one doesn't actually use elimination at all to find null spaces; instead, one uses something called the [SVD](https://en.wikipedia.org/wiki/Singular_value_decomposition) that we will cover later.)

## Lecture 8 (Feb 16)

* handwritten notes

Went through two examples of finding the special solutions as a basis for the nullspace.  They key point is always this: given the free variables, we can easily solve for the corresponding pivot variables.

We can now find the **complete solution** (i.e., all solutions) to a non-square linear system Ax=b.  Elimination turns this into Ux=C. We look for solutions in the form xₚ + xₙ: a **particular solution** xₚ plus any vector xₙ in N(A) (specified explicitly from the basis).  The particular solution xₚ can be *any* solution to Ax=b, but the simplest one to find is usually to *set the free variables* to zero.  That is, we write the solution xₚ=(p; 0) where p is the unknown values in the pivot rows, setting the other (free) rows to zero, then plug into Uxₚ=d to get p.  Since this extracts the part of U that is upper triangular, we can easily solve it.   Then we add in anything in N(A).

I used a 3×4 example matrix A (similar in spirit to one in the textbook, section 3.3) that was **rank deficient**: after elimination, we only had two pivots (rank r=2) in the first two rows, and a whole row of zeros.   Furthermore, its pivot columns were the first and *third* columns, with the second and fourth columns being free — this is possible (albeit unusual)!   Showed that we could still get the special solutions by solving for the pivot variables in terms of the free variables = (1,0,…) etcetera, and we still got dimension n-r (= 2) for the null space.   When solving Ax=b by elimination into Ux=c, however, we *only got a solution x if c was zero in the same rows as U*.  If the zero third row of U was matched by a zero third row of c, then we got a particular solution as before by setting the free variables to zero.  If the zero third row of U was *not* matched by a zero third row of c, then there is *no* solution: b was *not in the column space* C(A).  This gives an easy way to check whether the right-hand-side is in the column space.   We went through two example right-hand-sides: one with no solutions, and one with infinitely many solutions.

**Further reading:** Textbook sections 3.3–3.4, [lecture 8](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-8-solving-ax-b-row-reduced-form-r/).  As noted in lecture 7, I'm not emphasizing the trick of "rref" form (used extensively by Strang's book and lectures) which makes hand calculation *slightly* easier, but might push students towards memorizing formulas (which are useless in the long run).

## Lecture 9 (Feb 18)

* handwritten notes
* pset 2 solutions: coming soon
* *short* [pset 3](psets/pset3.ipynb) (due **Wed** Feb 23)

### Linear independence and C(A)

Bases, dimension, and independence.   Earlier, I defined a basis as a minimal set of vectors whose span gives an entire vector space, and the dimension of the space as the size of the basis.  Now, we want to think more carefully about the term "minimal".   If we have too many vectors in our basis, the problem is that some of the vectors might be redundant (you can get them from the other basis vectors).  We now rephrase this as saying that such vectors are *linearly dependent*: some linear combination (with nonzero multipliers) of them gives the zero vector, and we want every basis to be **linearly independent**.    The **dimension** of a subspace is still the number of basis vectors.

What does it mean to be linearly independent?  Given a set of n vectors {x₁, ⋯, xₙ}, if we matrix a matrix X whose columns
are x₁⋯xₙ, then C(X) is precisely the span of x₁⋯xₙ.   To check whether
the x₁⋯xₙ form a *basis* for C(X), we need to check whether they
are *linearly independent*.  There are three equivalent ways to think about
this:

1. We want to make sure that none of x₁⋯xₙ are "redundant": make sure
   that no xⱼ can be made from a linear combination of the other xᵢ's.

2. Equivalently, we don't want any linear combination of x₁⋯xₙ to give
   zero unless all the coefficients are zero.

3. Equivalently, we want N(X) = {0}.

In this way, we reduced the concept of independence to thinking about the
null space.   Since the nullspace is preserved by elimination, it follows
that *columns of A are dependent/independent if and
only if the corresponding columns of R are dependent/independent*.
By looking at R, we can see by inspection that the *pivot columns* form
a maximal set of independent vectors, and hence are a basis for C(R).
Hence, the *pivot columns of A* (i.e. the columns of A corresponding to
the columns of R or U where the pivots appear) are a basis for C(A).

It follows that the dimension of C(A) is exactly rank(A).

### Four important cases for Ax=b

Went through four important cases for an m×n matrix A of rank r.  (Note that we must have r ≤ m and n: you can't have more pivots than there are rows or columns.)

1. If r=n, then A has **full column rank**.  We must have m ≥ n (it is a "tall" matrix), and N(A)={0} (there are no free columns).  Hence, any solution to Ax=b (if it exists at all) must be *unique*.  (If m > n, the problem is "overdetermined": more equations than unknowns.)

2. If r=m, then A has **full row rank**.  We must have n ≥ m (it is a "wide" matrix), and C(A)=ℝᵐ.  Ax=b is *always solvable* (but the solution will not be unique unless m=n).  (If m < n the problem is "underdetermined": more unknowns than equations.)

3. If r=m=n, then A is a square **invertible** matrix.  Ax=b is always solvable and the solution x=A⁻¹b is unique.

4. If r < m and r < n, then A is **rank deficient**.  Solutions to Ax=b may not exist and will not be unique if they do exist.

Cases (1)-(3) are called **full rank**: the rank is as big as possible given the shape of A.  In practice, most matrices that one encounters are full rank (this is essentially always true for *random* matrices).  If the matrix is rank deficient, it usually arises from some special structure of the problem (i.e. you usually want to look at where A came from to help you figure out why it is rank deficient, rather than computing the rank etcetera by mindless calculation).   (A separate problem is that of matrices that are *nearly* rank deficient because the pivots are very small, but the right tools to analyze this case won't come up until near the end of the course.)

**Further reading:** Textbook sections 3.3–3.4, [lecture 9](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-9-independence-basis-and-dimension/).

## Exam 1 (Feb 25, in class)

Exam 1 will cover the material through **lecture 9** and **pset 3**: matrix-vector operations, matrix multiplication interpretations, writing/working with equations in matrix form, solving systems of equations with one or more right-hand side, Gaussian elimination, back/forward-substitution and triangular matrices, LU factorization and PA=LU, permutation matrices, matrix inverses and Gauss–Jordan, singular matrices, computational costs (which operations are ~ m² or ~ m³ and arranging calculations efficiently), rank of a matrix (= numbrer of pivots), vector space & subspaces, null space & special solutions, pivot/free columns column spaces, bases and dimensions of vector spaces, checking whether Ax=b is solvabe, complete solutions to Ax=b.

Practice questions: coming soon.