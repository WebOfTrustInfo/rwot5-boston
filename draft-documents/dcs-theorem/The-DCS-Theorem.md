---
title: "\\textbf{The DCS Theorem}"
author: Greg Slepak
date: \small October 4, 2017
abstract: "We present a probabilistic proof of the _DCS Triangle_ [@McConaghy2016][@SlepaksTriangle]. We use the triangle to show decentralized consensus systems cannot cannot scale to support the transactional demands of centralized consensus systems, and therefore any _single system_ can have _Decentralization_, _Consensus_, or _Scale_, but not all three properties simultaneously."
# output: pdf_document
output:
  pdf_document:
    latex_engine: xelatex
colorlinks: true
linkcolor: blue
urlcolor: blue
citecolor: blue
header-includes:
  - \usepackage[absolute]{textpos}
  - \usepackage{float}
  - \usepackage{afterpage}
  - \usepackage{pgfplots}
  - \textblockorigin{50mm}{10mm}
  - \renewcommand{\figurename}{Fig.}
  - \usepackage[font=footnotesize,labelfont=bf]{caption}
  - \usepackage{tikz}
  - \usetikzlibrary{shapes, arrows}
  - \renewcommand{\abstractname}{Abstract.}
  - \renewenvironment{abstract} {\small\quotation {\bfseries\noindent{\small\abstractname}\nobreak}} {\endquotation}
  - \usepackage{amsmath, amsthm, amssymb}
  - |
    \newtheoremstyle{plain}
    {\parsep}
    {\topsep}
    {\itshape}
    {0pt}
    {\bfseries}
    {.}
    {5pt}
    {}
  - \newtheorem{theorem}{Theorem}
  - \newtheorem{axiom}{Axiom}
  - \newtheorem{lemma}{Lemma}
  - |
    \newtheoremstyle{definition}
    {10pt}
    {5pt}
    {}
    {0pt}
    {\bfseries}
    {.}
    {5pt}
    {}
  - \theoremstyle{definition}
  - \newtheorem*{defn}{Definition}


# had to `brew install pandoc-citeproc` and download ieee.csl
# https://github.com/citation-style-language/styles/raw/master/ieee.csl
# https://gist.github.com/marcelofernandez/3264858
# ieee-trigraph + article-journal -> does et.al! :D
# —BUT! It doesn't put the freaking reference number in the bibliography!
# So I edited ieee.csl by comparing it. Turns out `et-al-min="7" et-al-use-first="1"` need to go into the <bibliography> tag!
csl: ieee.csl
# reference-section-title: "References"
# suppress-bibliography: false
link-citations: true
# http://docs.citationstyles.org/en/stable/specification.html#appendix-iv-variables
bibliography: dcs.bib
---

\begin{textblock}{3}(0,0)
\LARGE UNFINISHED DRAFT!
\end{textblock}

## Definitions

A _system_ is defined as any set of components (see \hyperref[sec:scope]{Scope}) following _precise rules_ in order to provide service(s) to the users of the system. These services constitute the system's _intended behavior_.

In other words, a system $S$ consists of a set of components, called its _scope_ $\{S\}$,  and a program ("state transition function", $f_S$), that together define the system's _intended behavior_, which means: upon receipt of message $m$, $S$ uses $f_S$ to update the internal state from $s$ to $s^\prime$ and send back reply $y$ within a time interval $S_\tau$.

$$
S(t) = \left\{
        \begin{array}{ll}
          \{S\} &= \{ component_1 , component_2, \cdots \} \\
          f_S(m, s) &= \{ s^\prime, y \}
        \end{array}
    \right.
$$
<!-- \right | \quad t=t_0 -->

We note, additionally:

- The _scope_ $\{S\}$ may change over time, but there are always several components of a consistent _type_ (i.e. "all systems always have at least one _CPU_, one _developer_, and one _user_")
- The system's state $s$ includes all data necessary for the system to compute $f_S$ given a message $m$
- $S$ is considered _compromised_ if it fails to perform its intended behavior within the interval $S_\tau$

We will proceed to prove that any single such system may possess, at most, two of three properties:

\clearpage

\begin{figure}
  \centering
  \vspace{0.2cm}
  \begin{tikzpicture}
    \draw (0,0) node[anchor=north east]{Consensus} -- (1,2) node[anchor=south]{Scale} -- (2,0) node[anchor=north west]{Decentralized} -- (0,0);
  \end{tikzpicture}
  % \caption{Slepak's Triangle}
  \vspace{0.2cm}
\end{figure}


- **Consensus** means the system's state, $s$ is a _shared state_ that is updated by nodes running a _consensus algorithm_ over a network, and that furthermore, the output of _consensus algorithm_ determines the network's accepted output of $f_S$, and whether or not $f_S$ completes within $S_\tau$.
- **Scale** means the system is capable of updating its state at the same (or greater) rate as any competing system providing the same service to the same arbitrary set of users across the globe (_"at scale"_).^[Examples of "services" include: streaming video, sending messages, maintaining balances on a ledger, etc.]
- **Decentralized** means the system has no _single point of failure or control_ (SPoF). Another way to state this is: the system continues to perform its intended behavior if any single element is removed from $\{S\}$, and no single component in $\{S\}$ has the power to redefine $f_S$ on its own.

Systems whose intended behavior can be modified without the consent of their users are considered _centralized_ due to the presence of a central point of control over the definition of the system.

## *Decentralization Scope* & *Relativity of Decentralization*
\label{sec:scope}

Implicit in our definition of a _decentralized system_ is the idea that the system is not compromised. A non-functioning system does not fulfill its intended behavior, and therefore, by our definition, is not decentralized.

Imagine a decentralized system $S$, whose intended behavior (its purpose) is to maintain the integrity of a database while being responsive to queries. It does so by attempting to eliminate all single points of failure within a given _scope._

<!--
> **Definition.** The ***scope*** of a system refers to all subcomponents and all entities "reasonably relevant" to a system's functioning.
-->

\begin{defn}
The $scope$ of a system refers to all subcomponents and all entities "reasonably relevant" to a system's functioning.
\end{defn}

If we consider the scope of our "decentralized" database to be a computer with two CPUs and two hard disks (one primary, another backup), then we can say $S$ is "decentralized" at $t=0$ (has no single point of failure). However, if at $t=1$ one of the hard disk fails, it is no longer decentralized since now there does exist a single component capable of compromising the entire system.

This means:

- Whether or not a system is decentralized can change over time.
- Any system can be called "decentralized" if we define the scope narrowly enough.
- All decentralized systems can be called "centralized" if we define their scope broadly enough.^[The entire Internet could be considered centralized if we include the entire solar system as part of the scope. The "single point of failure" could be the Earth itself, its atmosphere, the Sun, etc. Or, perhaps in the not distant future, a single ISP.]

The narrowing and enlarging of the scope is called the _relativity of decentralization_, and it is why first agreeing on a reasonable definition for a system's scope is vital before deciding whether or not it is "decentralized".

## Computational throughput of consensus systems

The _computational throughput_ $T(S)$ of any consensus system depends on three factors:

1. The computational power of each _consensus participant_ (those able to select transactions which are _written_ to the shared state).^[Note that participants who are only allowed to _verify_ state, but not participate in _creating_ it, are not considered consensus _participants_. Instead, they are called state _validators_.]
2. The amount of time the consensus algorithm considers messages to be lost (the _timeout_ period).
3. The consensus _threshold_ the consensus algorithm uses to decide whether consensus has been reached (e.g. "how big of a quorum is required").

Note that if the computational power of a consensus participant is significantly less than that of the other participants, they are more likely to be excluded from the deciding quorum for several reasons:

- If there are no network partitions to determine otherwise, fast consensus participants will process messages more quickly and therefore will be first to create a quorum.
- If there are enough fast consensus participants to create a large enough quorum to exceed the system's consensus threshold, then there is no need to wait for the slow participants to move the system forward.
- Slow consensus participants are more likely than fast consensus participants to hit the system's timeout period for processing and responding to messages, and therefore are more at risk of being excluded from the consensus process entirely.

Therefore, $T(S)$ is a function that is _limited by the slowest consensus participants not excluded in the deciding quorum._

## Coordination costs

Relevant for our proof is the notion of _coordination costs_, or the difficulty for one entity to engage another and work toward a common goal.

For example, when Bitcoin was first launched, it would be difficult for any miner to find enough collaborating miners to create a cartel with 51%+ of the hash power, simply because there were many "relevant miners" (consensus participants) distributed all over the world.

Today, however, there are significantly fewer consensus participants in Bitcoin, and it is much easier to (1) identify them, and (2) bring them together in a single room to coordinate around some goal. Therefore, we say the coordination costs are lower today than before.

We can approximate the coordination costs $C(S)$ of any consensus system as simply the number of consensus participants:

$$C(S) = \|\mathtt{consensus\_participants}(\{S\})\|$$

## Proof

We seek to prove the following restatement of the DCS Triangle:

\begin{theorem}
Decentralized consensus systems that scale to meet the demands of competing (and functionally equivalent) centralized consensus systems, become centralized.
\end{theorem}

Given these axioms:

\begin{axiom}
\label{AxCompPow}
In any sufficiently large population (at scale), individual access to computational power is not distributed uniformly. Most individuals have access to average computational power, and a few have access to large amounts.
\end{axiom}

\begin{axiom}
\label{AxDmd}
In any two systems offering the same service to the same large population, the transactional demands of the average user converge at scale.
\end{axiom}

\begin{lemma}
\label{LemTxn}
Let $S_1$ and $S_2$ be functioning consensus systems offering the same service to the same population of users at scale. Let $N$ be a function returning the number of active users on the system. If $N(S_1) > N(S_2)$, then $T(S_1) > T(S_2)$ converges to a true statement as the value $N(S_1) - N(S_2)$ increases.
\end{lemma}

\begin{proof}
This follows directly from (Axiom~\ref{AxDmd}).
\end{proof}

\begin{lemma}
\label{LemCoord}
The number of consensus participants decreases at scale, and therefore coordination costs decrease for systems at scale.
\end{lemma}

\begin{proof}
This follows from (Axiom~\ref{AxCompPow}) and our definition of $C(S)$. \em{[TBD. details.]}
\end{proof}

\begin{lemma}
"Increasing decentralization" of a consensus system at scale means making it slower and less capable of scale, therefore increase scale makes a system less capable of decentralization.
\end{lemma}

Follows from slow participants concept.

\begin{lemma}
\label{LemCensor}
The probability that $\{S\}$ contains a cartel capable of colluding to censor transactions approaches 1 at scale.
\end{lemma}

\begin{proof}[Proof of the Main Theorem]
foobar.
\end{proof}

<!--
https://tex.stackexchange.com/questions/43610/plotting-bell-shaped-curve-in-tikz-pgf
https://tex.stackexchange.com/questions/352933/drawing-a-normal-distribution-graph
-->

\pgfmathdeclarefunction{gauss}{2}{\pgfmathparse{1/(#2*sqrt(2*pi))*exp(-((x-#1)^2)/(2*#2^2))}%
}
\begin{tikzpicture}

\begin{axis}[no markers, domain=0:10, samples=100,
axis lines*=left, xlabel=Computational power, ylabel=Node count,
height=6cm, width=10cm, ytick=\empty,
enlargelimits=false, clip=false, axis on top,
grid = major]
\addplot [fill=cyan!20, draw=none, domain=-3:3] {gauss(0,1)} \closedcycle;
\addplot [fill=blue!20, draw=none, domain=2:3] {gauss(0,1)} \closedcycle;
\end{axis}
\end{tikzpicture}

_[This is where the paper currently ends. What follows below are "brain dumps" of random thoughts about how to go about proving the theorem. I expect the entire paper to be no more than 5 pages long.]_

## OLD STUFF - Outdated brain dumps [To be deleted]

Our definitions do not allow us to write a definitive proof but they do allow for a probabilistic proof. Similarly, the choice of scope cannot be clearly defined for arbitrary systems, but must be arrived at by probability of what is "likely" to be a "reasonable" or "characteristic" scope of these systems.

So we start with a simple model of two systems of 1000 nodes in consensus with each other and of random compute power and observe:

1. High throughput (scale) implies few elite consensus nodes, no matter how they're arrived at.
2. Few consensus nodes implies low coordination costs.
3. Low coordination costs implies higher probability of failure (censorship).
4. High coordination costs + more consensus participants implies lower probability of failure (censorship) and also no scale.

The power to exclude slow nodes, must not exist in decentralized systems.

- The more users a system has the more valuable it is
- The more valuable a system is the higher the reward is for controlling it
- The lower coordination costs the easier it is to control a system
- The more valuable a system is, the more incentive there is for a controlling group to censor it, and the cost of not censoring it is high
- If a system has scale it is more valuable than a system that does not have scale.

If the coordination costs are sufficiently low enough (define, possibly with an assumption), and the $rewards-costs$ (profit) for colluding are high enough (define, possibly with an assumption), then the consensus group acts as a single entity with high probability, creating a single point of failure. At the very least, we can be _certain_ that it is _much more likely_ to act as a single entity than in a situation where coordination costs are high.

This is a "probabilistic analysis" (and not a very specific one) — not a proof.

## Relationship between consensus and $f_S$

We have, up to this point, made it very clear that for $f_S$ to remain uncompromised and fulfill its _intended behavior_, it must produce expected output in a reasonable time. If it fails, it ceases to fit our definition of being a single, unique and consistently identifiable system.

There is, in other words, the opportunity for users of the system to at one point see system A that processes their transactions, behaves as they expect, and moments later experience a _functionally different_ system B that ignores their messages or otherwise behaves entirely differently.

The presence of a consensus algorithm in $S$ introduces a dangerous hazard into our definitions and assumptions. Various results from distributed systems, like the FLP impossibility result and the CAP theorem, point out that distributed systems cannot always fulfill this demand. Messages can be dropped due to mysterious network outages, etc.

Under these circumstances it is not always possible for the system to maintain a single consistent shared state, even in highly centralized, controlled environments.

Furthermore, in a _decentralized_ system that employs consensus, there cannot be a gatekeeper that decides who the consensus participants are, for such a gatekeeper would have the potential to remove all participants, or choose only participants who suddenly ignore the messages of existing users, and therefore they would represent a single point of failure.

The intuition behind our theorem is that in order for a consensus system to be decentralized, it must be more permissive as to who the consensus participants are, this permissiveness reduces the transaction capacity of the system as a whole (not everyone can run a data center at home).

The difference between a "_distributed_ consensus system" and a "_decentralized_ consensus system" is implied in the name. Decentralized consensus systems do not have a "center" deciding who the consensus participants are allowed to be.


## Proof stuff

-------

with $n_t$ nodes at time $t$, all running $f_S$, and a second similar system $S_2$, except unlike $S_1$, the system employs a _consensus algorithm_ to update its shared state.

Each system has At time $t_0$, running on $n$ nodes, where the _average computational power_ of nodes is $c_{t_0}$.

We define the _transactional capacity_ of a system, $T_c(S)$, as the maximum transaction rate a system can sustain _at scale_ without dropping messages.

Note the

Consider a universe $U$ consisting of $n$ entities, each of which we will label $e_i$.

Within $U$ we define a system $S$ that has a consensus process, meaning that the system's participants come to agreement about the system's state $state(S)$ at interval $\tau$.

Each consensus participant bears a computational load $c$ that is a function of the number of users that are sending messages through the system.

So the system $S$ has:

- $n_u$ number of users, each of which is sending some number of transactions per day. For simplicity's sake we will assume that each user sends an average of $X$ transactions per day.
- $n_c$ number of consensus participants, each bearing a load $c_c$ that is a function of $n_u$, likely with some cap beyond which the system simply begins adding transactions to a backlog.

Each user has a computational capacity of $c_u$. The condition $c_u=c_c$ means that all users of the system, including consensus participants, have equal computational capacity. We note that each additional new user added to the system increases the number of transactions that the system has to process, and that there exists a number beyond which the transactional load exceeds $c_u$. At that point, any additional users added to the system will result in transactions being added to a backlog.

To clear the backlog, either the number of users has to go down, or the computational capability of each consensus participant has to go up.

Increasing the computational capacity of consensus participants while preserving $c_u=c_c$ implies a simultaneous forced hardware upgrade of all users of the system. At global scale, this is unheard of. Hardware upgrades do happen, but they are not simultaneously enforced globally. Therefore there now exists the condition that $c_c > c_u$, meaning that not all users can participate in the consensus process any longer.

If the system gains users at a rate that exceeds the rate at which users of the system can upgrade their computational capacity, then $n_c / n_u$ will continue to become smaller and smaller.

We further note, that even if global computational capacity upgrades kept pace with the number of new users entering the system, each new _consensus participant_ adds $t(n_c)$ _additional_ time to the amount of time it takes consensus participants to reach consensus. We note that physics puts an upper bound on the amount of time it takes messages to propagate through the system, and therefore there exists an upper theoretically limit to the number of consensus participants, even assuming infinite computational capacity.

If $\sum t(n_c) > \tau$, the system will again have a backlog of messages.

Therefore we note two types of limits:

- A fundamental physical limit based on the speed of light that exists irrespective of computational power and is a function purely of $n_c$
- A practical limit that is a function of $n_c$, the rate at which computational upgrades occur in the system ($R_c$), and the rate at which users are added to the system ($R_u$).

We note that these limits only exist when there is a need for consensus. If there are no consensus participants (because there is no consensus), then transaction limit of the system is now "parallelized" instead of "serialized".

We note that if the ratio $R_c / R_u$ is such that new users are joining the system faster than they are able to upgrade their hardware to meet the increasing computational demands of consensus, then $n_c$, the number of consensus participants, becomes increasingly smaller with respect to $n_u$.

Here is a graph using Moore's law:

If we attempt to scale the system quickly, the triangle says that we will either lose Consensus or Decentralization. Why?

Well, if the system remains decentralized ...

If the system has consensus then ...

We see that as time goes on, the system is no longer able represent each user. In effect they are not "counted", and therefore $D_2$ is never met. If only 1% of users can participate in consensus, then there is no way to "count" their votes. Whether the system uses Proof-of-work or Proof-of-stake is irrelevant, because consensus participants determine which transactions are allowed to be "heard" (included) in the consensus-process, and they are free to simply ignore any "votes" of non-consensus participants.

## Characteristics of decentralized systems

Note that our definition of _decentralized_ necessarily implies various characteristics about the system.

#### Permissionless

Permission to run $f_S$ implies the existence of a gatekeeper (or gatekeepers). In practice this can manifest as closed source software, licenses, DRM, etc.

In our terminology, "at scale" means the system must support a global and _arbitrary_ set of users. This means, if the system operates at scale,

## Appendix A: The "DSS" Triangle

Scale-Security-Decentralization. Just another name for the same thing, but poorly defined.

## Appendix B: Examples of all three types of systems

Decentralized consensus:
Centralized consensus:


## Appendix C: Errata from "Slepak's Triangle"

- Note name change
- Note I meant subset not superset

## Characteristics of decentralized systems

To understand the proof, we must understand the characteristics of decentralized systems.

### Low-cost of participation

Decentralized systems typically have a low-cost of participation. In other words, little effort is needed to use the system, and anyone can play any role.

High costs usually point to the existence of a privileged entity with the power to exclude others from participation (a form of censorship). Such an entity represents a single point of failure ($D_1$) that could prevent the system from fulfilling its intended purpose for most of its users.

### Permissionless and inclusive
\label{sec:inclusive}

Our definition for decentralization means there is no trusted third-party deciding who can or cannot participate. Anyone around the world can join the system as long as they meet very basic resource requirements (e.g. an Internet connection).

Gatekeepers represent a central point of control, a violation of $D_1$ and $D_2$.

Most importantly, decentralized systems do not exclude inefficient participants. Rather, they go out of their way to ensure the most amount of participation. This is what keeps decentralized systems decentralized, as otherwise economies of scale will push the cost of participation up until a controlling group emerges, creating a single point of failure ($D_1$), along with the ability for that group to dictate behavior to the rest of the system ($D_2$).

This does not imply that decentralized systems are slow, but it does mean that decentralized **consensus** systems are _always_ significantly slower than their centralized counterparts.

### Censorship-resistant

The permissionless nature of decentralized systems, and their lack of a central point of control or failure, means they inherently resist all attempts at censorship.

### Can centralize over time

_Protocols_ and _implementations of protocols_ are two different things. A protocol can only provide _the ability_ for a decentralized system to exist, it does not provide a guarantee.

All decentralized systems, even those without consensus, can be centralized if steps are not taken to combat their centralization. Single points of failure are likely to emerge as the system gains more users and interacts with the systems around it.

Decentralized systems _involving consensus_ are especially vulnerable to centralization. An increase in the number of users represents two fundamental obstacles to their decentralization:

1. The system's shared resource becomes more valuable as it gains users, which increases the reward for successfully compromising the system. Furthermore, the system acts as a threat to the value managed (or monopolized) by established centralized players. Combined, these factors incentivize attackers to either find or create a single point of failure in the new system.
2. More users means more diversity of opinion over the system's future direction and the fate of its shared resource. Simultaneously, it becomes more difficult to distinguish real users from fake sybils or deliberate attempts at sabotage. As the distance between the system's maintainers and its average user increases, so too do misunderstandings. It becomes increasingly likely that _any_ decision over the fate of the system will result in the alienation of a significant fraction of users.

## Examples

## A Narrow Proof

We will construct a proof based on our very narrow definition of the term **"mainstream"**, which—it must be emphasized—we feel is _reasonably close but not identical to_ various colloquial understandings of the term.

It is important to understand what we _are not_ asserting:

- We **do not assert** that it is impossible for a decentralized consensus system to reach mainstream adoption. It is certainly possible:
  -  One could create a second system along the _decentralized-mainstream_ edge of the triangle and tie it to the first. This is what Bitcoin's Lightning network does.
  - It might be possible to connect multiple decentralized-consensus systems to each other while maintaining the decentralization of the system-of-systems, although this is still unproven. This is what the Mauve paper[2] and Tree-Chains[3] attempt to do.
  - More extreme measures include reducing the world's population to the point where "Mainstream" means "10 people" and therefore the difference between decentralized consensus systems and their centralized counterparts is negligible.
- We **do not assert** that decentralized consensus systems of _the future_ cannot compete with the centralized systems of _the present._ Certainly, as technology improves around the world the performance all systems improves. However, if one were to bring technology from the future to the present, that technology would improve the performance of centralized systems just the same.

### The proof

We will construct our proof by making three assertions:

1. _Decentralized consensus systems_ cannot process information as quickly as their centralized counterparts.
2. _Decentralized consensus systems_ have an upper user limit, which, if exceeded, makes the system increasingly centralized.
3. If the previous two assertions are true, the triangle holds.

#### 1. Decentralized consensus systems are slower

TODO: read:
- https://jvns.ca/blog/2016/11/19/a-critique-of-the-cap-theorem/
- https://www.cs.cornell.edu/courses/cs614/2006fa/Slides/FLP_and_Paxos.pdf
- http://book.mixu.net/distsys/abstractions.html

A consensus system $S$, whether it is decentralized or not, is comprised of consensus participants $p$ (nodes). As before, the time it takes for those nodes to come to consensus on the system's state is its _period_, $\tau$.

The difference between a centralized consensus system $\Bbb{C}$, and a decentralized consensus system $\Bbb{D}$, is that membership in $\Bbb{D}$ is not pre-determined. In other words, the members $p \in \Bbb{D}$ are not specified by any single entity (that is what it means for the system to be _permissionless_ and _inclusive_). Otherwise, the system \hyperref[sec:inclusive]{would violate} $D_1$ and $D_2$.

At the same time, the inclusive nature of the decentralized consensus system cannot mean that any single participant is capable of preventing consensus. If that were the case, the system would again violate $D_1$ and $D_2$.

We observe that in both $\Bbb{C}$ and $\Bbb{D}$, each participant $p$ takes _validation time_ $V_p$ to process and validate the messages it receives (determined by its computation capability), and adds an additional coordination cost/overhead $O_p$ to $\tau$, the amount of time it takes the system to reach consensus (determined by the connections between participants).

Next, we say that the system reaches consensus once some threshold (greater than 50%) of participants agree on the system's state.

We define $M$ as the set of messages the system can process during $\tau$.

Clearly, given two systems, $S_1$ and $S_2$, identical in all respects except by the speed with which members process and relay messages, the system whose members are slower will process fewer messages.

Now, let us consider two hypothetical "fastest possible" systems, $\Bbb{C}$ (centralized) and $\Bbb{D}$ (decentralized).

Let us consider $\Bbb{C}$ first. We note that if the system did not employ consensus (e.g. $N=1$), then the speed at which the system could process messages would be fully determined by $V_{p_0}$, and therefore $p_0$ would have to represent the "fastest available hardware" for a single node.

Extending this to $\Bbb{C}$, where $N \ge 2$, we observe that for any given $M$, the "fastest possible" centralized consensus system would have to consist of some optimal number of nodes, $N$, beyond which the coordination costs incurred by adding an extra node reduce the system's performance as a whole.

Therefore a lower-bound for $\tau$ is defined as:

$$\tau \ge \sum_{i=0}^N (p_i)$$

Given the same high transactional demands (e.g. 1 million messages), we denote $\Bbb{C}_\tau$ as the time taken by the fastest possible centralized consensus system to process those messages, and $\Bbb{D}_\tau$ as the time taken by the fastest possible decentralized system.



How do we know when the system has reached consensus to begin with?

We can start with the trivial case of there being a _leader_ node, $p_1$, that determines the value that the system is coming to agreement on. Obviously, if $p_1$ is faulty, the system will never reach consensus because all the other nodes depend up on it.

Since each node in the system

As \hyperref[sec:inclusive]{mentioned}, decentralized systems must be _permissionless_ and _inclusive_, otherwise they violate $D_1$ and $D_2$.

This coordination cost increases as more nodes are added as participants in the consensus.

If consensus is added on top of a decentralized system, the requirement for inclusivity does not go away. Thus the system must allow even "inefficient" participants to participate.

A _centrally managed_ distributed system can ensure that all consensus participants meet a certain minimum processing capabilities by virtue of there being a single point of control over the system (a single point of failure). Decentralized consensus systems do not have this single point of failure, but in giving it up they also give up the efficiency gains

As suggested by Liebig's law of the minimum^[https://en.wikipedia.org/wiki/Liebig%27s_law_of_the_minimum], and as demonstrated by Croman _et. al._[@Croman2015] in their analysis of blockchain scaling, the growth (or size) of a decentralized consensus system is limited by the scarcest resource.

#### 2. Decentralized consensus systems have an upper user limit

If the system enforces high resource requirements on participants in the pursuit of higher throughput, then the system become becomes increasingly centralized and the likelihood of central points of failure increases.

More users are forced to trust an increasingly smaller group to determine what the state of the system is. A deadly mixture emerges:

1. Reality starts to diverge from marketing claims the so-called "decentralized" system.
2. Simultaneously, the system's advocates point to "cheaper fees" due to "increased capacity".
3. News of "progress" and "cheaper fees" in this "decentralized" system attracts more users.

In reality, while _using_ the system may be less expensive, _participating_ in the system as an equally privileged node becomes significantly more expensive. The "increase" in capacity is also illusory, for by now the system has long exceeded its tolerable capacity for maintaining its decentralization.^[Threat of DDoS also goes up.]

<!-- \clearpage -->

A feedback "death spiral" occurs:
<!--
https://tex.stackexchange.com/questions/2275/keeping-tables-figures-close-to-where-they-are-mentioned -->
\begin{figure}[H] % REQUIRED! or else "pandoc Paragraph ended before was complete"
\centering
% https://www.sharelatex.com/blog/2013/08/29/tikz-series-pt3.html
\tikzstyle{block} = [rectangle, draw, text width=10em, text centered, rounded corners, minimum height=2em]
\tikzstyle{line} = [draw, -latex']
\begin{tikzpicture}[node distance = 1.3cm, auto]
% \begin{tikzpicture}[node distance = 2cm]
  \node [block] (users) {more users};

TODO: Maybe make next node "increase the capacity!"
  \node [block, below of=users, xshift=3.5cm] (demands) {harder to participate in consensus};
  \node [block, below of=demands, xshift=-3.5cm] (fewer) {fewer consensus participants};
  \node [block, above of=fewer, xshift=-3.5cm] (capacity) {more “fake capacity”};
  \path [line] (users) -- (demands);
  \path [line] (demands) -- (fewer);
  \path [line] (fewer) -- (capacity);
  \path [line] (capacity) -- (users);
\end{tikzpicture}
% \caption{}
\end{figure}

The Croman work expanded on prior research [@??] and showed that global bandwidth is, at present, the scarcest resource limiting Bitcoin's growth. Further, it shows that 4MB is the absolute.

#### 3. Given (1) and (2), the triangle holds

## Appendix A: Choosing a safe redefinition threshold
\label{sec:a}

Link to flocking study and point out how 95% creates a central point of failure.

The more value being considered / the more potential harm, the higher the threshold must be.

Because not all users can vote, because forks are high-stakes irreversible decisions[@Slepak2016], and because a split vote indicates strong community indecision/disagreement, it is usually better to use a higher threshold.

The reason for very high thresholds is due to the fact that most users of the system will be unable to vote because there's no way to safely "count" their votes.

Now we instantly see a relationship between Consensus and $D_2$. We also observe that "users" is ambiguous. In Bitcoin, is it token holders? Is it miners? Developers? How do you measure these?

However, we have a serious problem: we can't measure whether we've reached the threshold beyond ~150 users! We only assume we can. OTOH, with certain hierarchical counting methods, where there is both transparency and everyone is incentivized to verify that the vote is accurate, maybe you can. E.g. CNN had a centralized website showing the numbers for various precincts reporting in, and each presinct can check that their number is accurately represented. With CONIKS and/or PoW, it maybe be possible to use such a method to count more people.

One way to get around this limit is to reduce the amount of information-flux/change that the system is expected to handle. We can do this by making the system immutable (or mostly immutable). For example, religions are systems too, and they are capable of supporting so many "users" precisely because they are based on texts that are widely distributed and not only do not change, but are explicitly expected _not_ to change.

It's 75% of *users* not stake or CPU!

PoS voting doesn't count if stake is centralized, and by Zipfs law we can expect it to be. Same for PoW.

A human being physically cannot verify a vote count involving more people than what they can visually distinguish in their visual field of view without running into the Sybil attack or PoS (e.g. $1-1-vote).

# References
