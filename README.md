# MIT Course 18.06, Fall 2022

This is a repository for the course [18.06: Linear Algebra](http://web.mit.edu/18.06) at MIT in Fall 2022.   See [other branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/viewing-branches-in-your-repository) of this repository for previous semesters.

**Instructor**: [Prof. Steven G. Johnson](http://math.mit.edu/~stevenj).  Course administrator: [Sergei Korotkikh](https://math.mit.edu/directory/profile.php?pid=2113).

**Lectures**: MWF11 in 26-100.  [Handwritten notes](https://www.dropbox.com/s/a1xy4oh6wb2i5ub/18.06%20Fall%202022.pdf?dl=0) are posted online, along with video recordings (linked below) and other materials (slides, further reading) in the lecture summaries below.

**Exams**: 11am in 26-100, on 10/7, 11/14, & 12/9.  Final exam: date TBA.

**Recitations**:

 * R01,R02 — [Chirag Falor](https://web.mit.edu/directory/?id=cfalor&d=mit.edu): T9 in 2-143, T10 in 2-146 (office hours Mon 3pm [via Zoom](https://mit.zoom.us/j/96071172098), Wed 3pm in 2-449).
 * R03,R05 — [Melissa Sherman-Bennett](https://sites.google.com/view/mshermanbennett): T11 in 2-147, T12 in 2-147 (office hours Wed 10am [via Zoom](https://mit.zoom.us/j/96071172098), Thurs 10am in 2-136).
 * R04 — [Sergei Korotkikh](https://math.mit.edu/directory/profile.php?pid=2113): T11 in 2-146 (office hours Tues 6pm [via Zoom](https://mit.zoom.us/j/96071172098), Thurs 6pm in 2-242).
 * R06,R09 — [Victor Rong](https://web.mit.edu/directory/?id=vrong&d=mit.edu): T12 in 2-146, T1 in 2-146 (office hours Mon 8pm [via Zoom](https://mit.zoom.us/j/96071172098), Tues 2pm in 2-361).
 * R07,R08 — [Mitchell Harris](https://math.mit.edu/directory/profile.php?pid=2180): T12 in 2-361, T1 in 2-142 (office hours Mon 2pm [via Zoom](https://mit.zoom.us/j/96071172098), Fri 2pm in 32-D707).
 * R10,R11 — [Ishan Levy](https://math.mit.edu/directory/profile.php?pid=2185): T1 in 2-136, T2 in 2-142 (office hours Thurs 10:30am [via Zoom](https://mit.zoom.us/j/96071172098), Wed 2pm in 2-390).
 * R12,R13 — [Gefei Dang](https://math.mit.edu/directory/profile.php?pid=2178): T2 in 2-146, T3 in 2-142 (office hours Thurs 4pm [via Zoom](https://mit.zoom.us/j/96071172098), Wed 11am in 2-239).

**Undergraduate Assistants**: Raza Abbas, Alvin Chen, Christina Mirro, and Daniel Villagran.   Email them at **1806fall22_ua ατ mit.edu** for 1-on-1 technical help with Julia or other questions that don't work well over Piazza etc.

**Resources**: [Piazza discussion forum](https://piazza.com/class/l7g5ixuivav3rm), [math learning center](https://math.mit.edu/learningcenter/), [TSR^2 study/resource room](https://ome.mit.edu/programs/talented-scholars-resource-room-tsr2), [pset partners](https://psetpartners.mit.edu/).

This document is a *brief* summary of what was covered in each 18.06
lecture, along with links and suggestions for further reading.  It is
*not* a good substitute for attending lecture, but may provide a
useful study guide.  (You can also look at the analogous summaries from [Spring 2022](https://github.com/stevengj/1806/blob/spring22/README.md).)

## Lecture 1 (Sep 7)

* [course overview/syllabus](https://docs.google.com/presentation/d/1ivbV1nr67XfasBdXezZF9UWILzDoQtQev8vSqRKBfu0/edit?usp=sharing)
* [pset 1](psets/pset1.ipynb): due **Friday Sep 16 at 11am** (submit your solutions on Gradescope).
* [video](https://mit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=19855fd0-d2be-4252-aa41-af0900816383)

Slides giving the syllabus and the "big picture" of what 18.06 is about.  Introduction to thinking about matrices as linear operations, not just as "bags of numbers".

**Further reading**: Strang, chapter 1, and section 8.1 on linear transformations.  3blue1brown has a nice video on [matrix multiplication as composition of linear transformations](https://youtu.be/XkY2DOUCWMU).  If you've forgotten the basics of how to multiply matrices by vectors or matrices by matrices, google for some tutorial material online (e.g. [Khan academy](https://www.khanacademy.org/math/precalculus/x9e81a4f98389efdf:matrices/x9e81a4f98389efdf:multiplying-matrices-by-matrices/a/multiplying-matrices)) and do a quick brush-up.

## Lecture 2 (Sep 9)

* handwritten notes: see link above (at beginning)
* [video](https://mit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b9662b0d-6280-448a-b745-af090062417b)

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

We're not done: it turns out to be even more fruitful to *reverse* the process, and write A = LU: L represents the operations required to turn the matrix U back into A, and turns out toe be a **lower**-triangular matrix whose entries are just a record of the elimination steps.  This **LU factorization** is extremely useful and important because it allows us to replace a *complicated* matrix A with two *much simpler* (triangular) ones.  For example, solving Ax=b turns into LUx=b, and we can do this just by two "triangular" solves.  More on this next time.

**Further reading:** Textbook sections 2.1, 2.2, 2.3.  Strang [lecture 2 video](https://www.youtube.com/watch?v=QVKj3LADCnA&list=PLE7DDD91010BC51F8&index=3).   And there is a Gaussian-elimination [Julia notebook](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Gaussian-elimination.ipynb) that covers the same steps in Julia form.
See also "The key reason why A = LU" in section 2.6 of the textbook.

## Lecture 3 (Feb 4): recorded

* video (only): see the [spring 2022 recording](https://mit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=885fb286-4dab-4aa6-9ef0-ae2e00f05ceb), lecture 3
* handwritten notes
* [Matrix inverse and LU notebook](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Inverses-LU-intro.ipynb)

(Prof. Johnson is sick and so we will use the recorded lecture from spring.)

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

## *Optional* Julia Tutorial: recorded

* [video recording](https://mit.zoom.us/rec/share/w7o2TQjDOnHsaRlJvbS1iysu5Sh23gGVFt3nX_VShRoRBr5UCsPlMhEu1EeyQrk.Vq1WOfArkC3v-Lma?startTime=1643839179000)

(No live tutorial since Prof. Johnson is sick.)

A basic overview of the Julia programming environment for numerical computations that we will use in 18.06 for simple computational exploration.   This (Zoom-based) tutorial will cover what Julia is and the basics of interaction, scalar/vector/matrix arithmetic, and plotting — we'll be using it as just a "fancy calculator" and no "real programming" will be required.

* [Tutorial materials](https://github.com/mitmath/julia-mit) (and links to other resources)

If possible, try to install Julia on your laptop beforehand using the instructions at the above link.  Failing that, you can run Julia in the cloud (see instructions above).

## Lecture 4 (Sep 14)

* [video recording](https://mit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=faf2a3ef-fcc2-4ff4-a928-af0900628908)
* [Matrix inverse and Gauss–Jordan](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Gauss-Jordan.ipynb)

Reviewed matrix inverses and key properties thereof.

Went through how to explicitly compute A⁻¹ by solving AA⁻¹ = I.   Essentially, this is just solving Ax=b multiple times, where b is each column of I. A common way to organize this for *hand* calculation (ugh) is the Gauss–Jordan algorithm (on a 3×3 example that can also be found in the textbook): If we do row operations on A to get I, then the *same* row operations on I give A⁻¹!  To carry this out by hand, we augment (A|I), do ordinary Gaussian elimination to get (U|C), and then do elimination "upwards" to get (I|A⁻¹).

Matrix inverses are mainly a *conceptual* tool that we use to move matrices around *symbolically* in equations.   Once you are through with your algebraic manipulations, you might end up with an expression like A⁻¹b — but when it comes time to actually *compute* the answer, you should **read "A⁻¹b" as "solve Ax=b for x by the best available method"**.

**Further reading:** Textbook sections 2.5, 2.6.  Strang [video lecture 3](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-3-multiplication-and-inverse-matrices/).


## Lecture 5 (Sep 16)

* [Video recording](https://mit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=32b37815-81a0-42aa-a2a5-af0c00d75c55)
* [pset 1 solutions](psets/pset1sol.ipynb)
* [pset 2](psets/pset2.ipynb): due **Mon** Sep 26 (Friday is a holiday).
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

## Lecture 6 (Sep 19)

* video: Panopto Video link on Canvas
* handwritten notes
* [Computational complexity](https://nbviewer.org/github/mitmath/1806/blob/master/notes/Complexity.ipynb)

Complexity of matrix operations: why matrix × vector or backsubstitution scale like n² for n×n matrices, while matrix × matrix or Gaussian elimination (LU factorization) scale like n³.   Matrices much bigger than a few thousand square quickly become impractical, and really large problems are only tractable because they have special structure like [sparsity](https://en.wikipedia.org/wiki/Sparse_matrix).

The next few weeks will be devoted to problems arising from **singular** and **non-square** matrices.   A "singular" square matrix is one for which we "run out of pivots" when doing elimination (we hit zeros on the diagonal we can't remove with row swaps).   Non-square matrices are either "tall" (arising in **overdetermined** systems with more equations than unknowns, leading to **fitting** problems and *approximate* solutions) or "wide" (arising in **underdetermined** systems with more unknowns than equations, leading to *freedom* in the choice of solution and *regularization* techniques to impose "priors" on this choice).   A key technique that will help us understand these equations is to **break vectors into simpler/smaller vectors**.   To do this we must first broaden our concept of a "vector".

Introduced **vector spaces** (informally, a set V of anything you can add x±y and multiply by scalars αx) and **subspaces** (a subset of V such that vector operations *stay in the subspace*).  Examples of vector spaces include real n-component vectors (ℝⁿ, or ℂⁿ for complex numbers), real m×n matrices, functions f(x) (ℝ↦ℝ, real numbers to real numbers).  Examples of subspaces includes planes or lines through the origin in ℝ³, or the origin itself.   The goal of this is to break vector spaces into smaller pieces that we can still do linear algebra on (hence the need for a subspace, not just any arbitrary subset).  Subspaces are especially important to help us understand the solutions (if any) of Ax=b for **non-square** matrices A.

**Further reading:** Textbook sections 2.6 ("The cost of elimination") and 11.1.   Section 3.1 and 3.2 on vector spaces and subspaces.

## Lecture 7 (Sep 21)

* video: Panopto Video link on Canvas
* Handwritten notes

Reviewed **vector spaces** (informally, a set V of anything you can add x±y and multiply by scalars αx) and introduced **subspaces** (a subset of V such that vector operations *stay in the subspace*).  Examples of vector spaces include real n-component vectors (ℝⁿ, or ℂⁿ for complex numbers), real m×n matrices, functions f(x) (ℝ↦ℝ, real numbers to real numbers).  Examples of subspaces includes planes or lines through the origin in ℝ³, or the origin itself.   The goal of this is to break vector spaces into smaller pieces that we can still do linear algebra on (hence the need for a subspace, not just any arbitrary subset).  Subspaces are especially important to help us understand the solutions (if any) of Ax=b for **non-square** matrices A.

For an m×n matrix A, introduced two important subspaces.

* First, the **column space C(A)**: the set {Ax for all x ∈ ℝⁿ}.  This is the set of *right-hand sides* b such that Ax=b is *solvable*, and is a subspace of the "output space" ℝᵐ (not ℝⁿ unless m=n!).  Equivalently, C(A) is all linear combinations of the *columns* of A, which we call the **span** of the columns.

* Second, the **null space N(A)** (also called the "kernel"): the set {x such that Ax=0} ⊆ ℝⁿ (i.e., a subspace of the "input space" ℝⁿ).  Given any solution x to Ax=b, then x+z is also a solution if z ∈ N(A) (i.e. Az=0 ⟹ A(x+z)=Ax+Az=Ax=b).

These are very important subspaces because they tell us a lot about the matrix A and solutions to Ax=b.  As a trivial example, if A is an n×n *invertible* matrix, C(A)=ℝⁿ and N(A)={0}.  Conversely, if A is an m×n matrix of zeros, then C(A)={0} and N(A)=ℝⁿ.

Defined a **basis** for a vector space as a *minimal* set of vectors (we will later say that they have to be *linearly independent*) whose
**span** (all linear combinations) produces everything in the space.  The number of vectors in any basis is the **dimension** of the vector space.

Showed that the **nullspace is preserved by elimination (row) operations**, but that the column space is not.   So, to find N(A), we can instead do elimination and find N(U)=N(A) for the upper-triangular form U.   We now want to find *all* possible solutions to Ax=0.

**Further reading:** Textbook, sections 3.1—3.3; Strang [video lecture 6](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-6-column-space-and-nullspace/) and [lecture 7](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/lecture-7-solving-ax-0-pivot-variables-special-solutions/).   Note that Strang's lectures and book emphasize the "reduced row echelon" ("rref") form, which is essentially a bookkeeping trick (similar to Gauss–Jordan for inverses) to do the back-solves for the special solutions all at once.  I will *not* emphasize rref form this semester, but you can use it if you want.  (In practical applications, rref form is virtually never used, and for that matter one doesn't actually use elimination at all to find null spaces; instead, one uses something called the [SVD](https://en.wikipedia.org/wiki/Singular_value_decomposition) that we will cover later.)
