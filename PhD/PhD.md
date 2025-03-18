# PhD

*The thesis is titled Application of variational algorithms in quantum computation. It will be publicly accessible from UCL, and is available as a PDF file [here](./Thesis%20Hongxiang%20Chen.pdf).*

Since joining the quantum computation group at UCL, I have worked independently to develop algorithms targeting the near-term applications of quantum computers. I developed variational (quantum) algorithms for error correction and for computing Green’s function.

#### Background

The initial interest in using quantum mechanics for computation stems from the desire to model the complex dynamics of quantum mechanical systems. The idea is to simulate the ultimate physical laws exactly, without approximations as on classical computers, and efficiently, without for example the exponential space cost as would also be required on classical computers.

​Recently, significant interest has been drawn to quantum computation due to a few algorithms promising exponential advantages over the best classical alternatives. For example, *Shor’s algorithm* factors larger numbers in polynomial time while the best classical counterpart factors in sub-exponential time. As the security of modern communication technology relies on the exponential difficulty of the classical algorithm, Shor’s algorithm can be used to break modern encryption algorithms. It has pushed the leading encryption algorithm to look for quantum-proof algorithms that would not rely on the difficulty of large number factorisation.

​Recent interest in quantum computation has been focused on *error-resiliency*. This is driven by the errors appearing significantly more frequently on quantum computers than on classical computers. Taking information storage as an example, on classical computers the chance of a memory error is probably much less than $10^{-18}$ (see e.g. a [2009 study](http://10.1145/2492101.1555372) by Google), while that of the best quantum computers today is of order $10^{-4}$ or worse, significantly more than the classical case! The larger error rate makes practical quantum computation impossible. Currently, only extremely short operations (about ten to a hundred in my experience) can be reliably executed on quantum computers from major providers.

​For the so-called near-term era, we anticipate that only quantum computers of a moderate size and of a noisy nature can be available. In this era, *variational quantum algorithms (VQAs)* have been most successful. Variational quantum algorithms transform the problem such that its solution can be obtained by minimising an energy function. Additionally, such problems are not extremely sensitive to the quality of the solution. The archetypical example is the variational quantum eigensolver (VQE), which transforms the ground-state problem (finding the smallest eigenvalue of a matrix) into the minimisation of energy computed on a trial vector.

#### My Projects

**Computing Green’s function.** In this project, we extended the variational quantum eigensolver to compute Green’s function. As Green’s function requires information from excited states (i.e., from eigenvalues of higher values than the ground-state value), we extended VQE to cover such states. This has been achieved in two major approaches: one through a modified Hamiltonian and obtains the information of higher eigenvalues one-by-one, the other through a variational linear algebra solver which can scan the real numbers for certain “signatures” of the information from excited states.

<details>
<summary>What is a Green’s function?</summary>

Green’s functions are analytical tools used to characterise the response of the system to an external point-like disturbance. The mathematical Green’s function was named after the British mathematical physicist George Green and used for solving partial differential equations (PDEs): it is the solution of an inhomogeneous PDE where the inhomogeneous term is replaced by a Dirac delta function. The many-body Green’s function, which is discussed in the main text, grows out of the application of the mathematical one to quantum many-body theory (see a concrete example in the introduction of [this paper](https://arxiv.org/abs/2406.03204)). While the definition of many-body Green’s function is different from the mathematical one, under a so-called linear response theory, the many-body one would describe the response of a many-body system to an instantaneous disturbance, sharing the same intuition with the mathematical one.
</details>

​Further, we have actually implemented one of the quantum algorithms for Green’s function on a quantum computer, thus proving its noise-resilience on a concrete example. Through these projects, we have tested and tailored the software and algorithm design to the needs of the quantum hardware available, and shed light on the potential use of such methods for the analysis and design of new materials.

**Logical gate generation in error correction.** In another project, we applied the idea behind VQAs to quantum error correction. We try to tackle the problem of generating logical gates within an error-correcting code. Instead of mathematically analysing the structure of the given code, which is the traditional method and which requires significant mathematical knowledge, we aim to generate the logical gates by variational methods.

<details>
<summary>What is quantum error correction?</summary>

Quantum error correction is a way of dealing with the error-prone nature of quantum computers by actively encoding and manipulating information stored in protected subspaces in quantum computers. Specifically, the information is encoded using the error-correcting codes, and thus protected from the disturbance from error. Such encoded information is manipulated using logical gates within the encoded subspace.
</details>

​This aim is achieved as we look at the problem from the bottom up. First, a logical gate is a transformation between the encoded information, or mathematically the unitary transformation between the encoded basis (“code words”). This transformation can be parametrised in terms of single-qubit rotation gates, or the so-called *ansatzes*, using the same approach common in the VQE. We then restrict the transformation to be local, which is ideal for resilience against noise. Finally, we make it compatible with the error-correcting code by appending the so-called minimum weight perfect matching corrections after every computation.

​The result is an automated procedure for generating logical gates given error-correcting codes. Notably, we have generated a few logical gates which haven’t been discovered by the inventors of the codes. We were credited [here](https://errorcorrectionzoo.org/c/stab_8_3_2) for the discovery of the CZ gate for the [[8,3,2]] code.
