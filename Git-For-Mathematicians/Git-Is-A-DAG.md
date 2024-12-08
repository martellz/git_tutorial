Imagine you have a growing collection of proofs and theorems, each at varying stages of refinement. You would like not only to record each improvement you make to a proof, but also to explore different directions without losing the work you’ve done so far. Git is a system designed to help you manage this evolving body of work seamlessly, allowing you to return to earlier states, work in parallel on different lines of thought, and merge these lines back together with mathematical precision.

## Core Concept

### Directed Acyclic Graph (DAG)

In case you are not familiar with the term, a **directed acyclic graph (DAG)** is a structure that consists of vertices and **directed edges** (arrows) connecting these vertices. The edges are **directed**, meaning they have a direction (from one vertex to another), and the graph is acyclic, meaning there should be no cycles (loops) in the graph.

Example
```
A -> B -> C
     |
     v
     D
```

Non-Example
```
A -> B -> C
^         |
|         v
E <- F <- G
```

### Git as a DAG

At its heart, a Git repository can be thought of as a **directed acyclic graph (DAG)** 

* whose **vertices represent “commits”** (snapshots of your work at given points in time) and 

* whose **edges represent the developmental lineage from one commit to the next**. 

Each commit is like a discrete state of your project—analogous to a well-defined mathematical object, such as a particular vector in a space of possible project states. 

The repository moves from one state to another as you progress, and because Git stores the entire structure, it is trivial to revert to a previous state or to compare two states.

This DAG structure can be considered similar to a partially ordered set: commits are partially ordered by their ancestry. You may have different “branches” within your repository, much like different solution paths stemming from a common set of axioms. Branches allow you to explore multiple approaches in parallel, as if you were conducting different proofs from the same starting theorem. Later, you can merge these branches, akin to identifying isomorphic structures and unifying them into a single, more advanced theorem.

### Most Important Understanding About Git

* Local Snapshots, Not Deltas: Git records full snapshots of your entire project at each commit, not just the changes. This makes it easy and efficient to jump backward and forward in time.

* Branching as Parallel Worlds: Branches allow you to investigate alternative solutions or algorithms without interfering with your main line of development. Imagine having multiple sequences of lemmas that might lead to a grand theorem; you can keep these sequences separate and clearly defined.

* Merging Without Data Loss: When two lines of thought (branches) converge, you can merge them. In an ideal scenario—analogous to merging isomorphic structures in a category—the final result incorporates the best features of each branch without losing any work.

### Three Frequently Used Workflows

#### Committing Your Changes (Local Commit Workflow)

**Example**: Suppose you are refining a proof in a file called `main_proof.tex`. You add a new lemma and reorganize the argument slightly.

**Process**:
        Stage your changes: git add main_proof.tex
        Capture a snapshot (commit): git commit -m "Refine proof of Lemma 2 and reorganize argument."

**Analogy**: This is like documenting a step in your proof’s evolution. Each commit is a recorded state in your DAG—a new vertex connected to the previous node.

#### Pushing to a Remote Repository (Push Workflow)

**Example**: After committing a few changes locally, you want to store them in a remote location (like a collaborative server) so that your colleague, working on a related lemma, can see them.

**Process**:
Send your local commits to a remote repository: git push origin main

**Analogy**: If your local repository is a private workspace (like your personal scratchpad), pushing is like publishing your current known results to a public archive, ensuring others can build upon this new state.

#### Incorporating Others’ Changes (Pull Workflow)

**Example**: Your colleague has improved a crucial step in the proof and committed these changes to the remote repository. To keep your version in sync, you download and integrate their modifications.

**Process**:
Retrieve and integrate the latest remote changes: git pull origin main

**Analogy**: Pulling is like receiving a new lemma from a collaborator and adding it to your body of knowledge. The repository’s state evolves, incorporating someone else’s contribution, and your graph of commits now includes their recent work.
