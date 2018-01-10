---
# default latex template: https://github.com/jgm/pandoc-templates/blob/master/default.latex
title: "\\textbf{The DCS Theorem}"
# The author is specified in header-includes because the line break doesn't work otherwise
# author: Greg Slepak^\dag^, Anya Petrova
# author: Greg Slepak \\ \href{mailto:hi@okturtles.com}{hi@okturtles.com} \and Anya Petrova \\ \href{mailto:a.petrova.ds@gmail.com}{a.petrova.ds@gmail.com}
# date: \small ^\dag^okTurtles Foundation, USA
date: October 4, 2017
abstract: "Blockchain design involves many tradeoffs, and much debate has focused on tradeoffs related to scaling parameters such as blocksize. To address some of the confusion around this subject, we present a probability proof of the _DCS Triangle_ [@McConaghy2016][@SlepaksTriangle]. We use the triangle to show decentralized consensus systems, like blockchains, can have _Decentralization_, _Consensus_, or _Scale_, but not all three properties simultaneously. We then describe two methods for getting around the limitations suggested by the triangle."
# https://shd101wyy.github.io/markdown-preview-enhanced/#/pandoc-pdf
output:
  pdf_document:
    latex_engine: xelatex
    number_sections: true
# secnumdepth: 2
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
  - \usetikzlibrary{shapes, arrows, patterns}
  - \pgfplotsset{compat=1.14}
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
  - \urlstyle{tt}
  - \author{Greg Slepak \\ \href{mailto:hi@okturtles.com}{\texttt{hi@okturtles.com}} \and Anya Petrova \\ \href{mailto:a.petrova.ds@gmail.com}{\texttt{a.petrova.ds@gmail.com}}}


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

<!-- \begin{textblock}{3}(0,0)
\LARGE DRAFT
\end{textblock} -->

# Definitions
\label{sec:defs}

A _system_ is defined as any set of components (see \hyperref[sec:scope]{Decentralization Scope}) following _precise rules_ in order to provide service(s) to the users of the system. These services constitute the system's _intended behavior_.

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

- The _scope_ $\{S\}$ may change over time, but there are always several components of a vital type (i.e. "all systems always have at least one _CPU_, one _developer_, and one _user_").
- The system's state $s$ includes all data necessary for the system to compute $f_S$ given a message $m$. The system may limit messages to those that are authorized in some way (in order to prevent denial-of-service).^[For decentralized systems, this is okay as long as there is no central authority determining who is or isn't authorized.]
- $S$ is considered _compromised_ if it fails to perform its intended behavior within the interval $S_\tau$.

We will proceed to prove that any single such system may possess, at most, two of three properties:

<!-- \clearpage -->

\begin{figure}
  \centering
  \vspace{0.2cm}
  \begin{tikzpicture}
    \draw (0,0) node[anchor=north east]{Consensus} -- (1,2) node[anchor=south]{Scale} -- (2,0) node[anchor=north west]{Decentralized} -- (0,0);
  \end{tikzpicture}
  % \caption{Slepak's Triangle}
  \vspace{0.2cm}
\end{figure}

\label{sec:triangle}

- **Consensus** means the system uses a collective decision-making process ("consensus algorithm") to update the system's state, $s$, which is shared by all _\hyperref[sec:consensus]{consensus participants}_. The result of the consensus algorithm determines the network's accepted output of $f_S$, and whether or not $f_S$ completes within $S_\tau$.
- **Scale** means the system is capable of handling the transactional demands of any competing system providing the same service to the same arbitrary set of users across the globe (_"at scale"_).^[Examples of "services" include: streaming video, sending messages, maintaining balances on a ledger, etc.]
- **Decentralized** means the system has no _single point of failure or control_ (SPoF). Another way to state this is: if any single element is removed from $\{S\}$, the system continues to perform its intended behavior, and no single component in $\{S\}$ has the power to redefine $f_S$ on its own.

## Consensus participants and "full" consensus
\label{sec:consensus}

The concept of a "consensus participant" is sometimes confused with the concept of a "validator", and in order to understand what the DCS Triangle is saying it's necessary to understand the difference between the two.

Every consensus process has three ingredients: voters (consensus participants), voting rules, and the votes themselves.

In distributed systems, the job of a _validator_ is to verify that the voting rules were followed, accepting the outcome of the vote if that is so, and rejecting the outcome otherwise. For example, in the physical world a validator might be responsible for verifying ballot forms were filled out correctly and were cast by registered voters only, but beyond that they do not (generally speaking) have the ability to influence the outcome of the vote.

Consensus participants, on the other hand, are the voters themselves, and their job is to not only ensure that voting rules are followed, but to cast a vote on some decision.

In Bitcoin, for example, "miners" are consensus participants whose job is to vote on which transactions are accepted into the blockchain, whereas non-mining "full nodes" are validators only, and their job is to ensure that miners do not produce invalid blocks.

\begin{defn}
$Consensus\ participants$ are independent entities who each maintain a complete copy of a system's state, and together vote on updates to this shared state.
\end{defn}

The notion of a "complete copy of a system's state" is of utmost importance for our proof. In other words, our proof focuses specifically on the strongest notion of "consensus", where each consensus participant has full knowledge of the entire system state, and therefore is able to cast a vote without needing to trust any other participant.

To emphasize this notion of consensus over weaker forms, we'll refer to it as _full_ consensus in our theorem.

In *\hyperref[AppendixA]{§3 - Getting around the DCS Triangle}*, we'll explore how, by loosening this requirement and treating "consensus" as a spectrum of trust assumptions, it may be possible to design decentralized consensus systems that scale with "good-enough-consensus".

## Decentralization *scope* & *relativity*
\label{sec:scope}

Implicit to our definition of a _decentralized system_ is the idea that the system is not compromised. A non-functioning system does not fulfill its intended behavior, and therefore, by our definition, is not decentralized.

Imagine a decentralized system $S$, whose intended behavior (its purpose) is to maintain the integrity of a database while being responsive to queries. It does so by attempting to eliminate all single points of failure within a given _scope._

\begin{defn}
The $scope$ of a system refers to all subcomponents and all entities reasonably relevant to a system's functioning.
\end{defn}

If we consider the scope of our "decentralized" database to be a computer with two CPUs and two hard disks (one primary, another backup), then we can say $S$ is "decentralized" at $t=0$ (has no single point of failure). However, if at $t=1$ one of the hard disk fails, it is no longer decentralized since now there does exist a single component capable of compromising the entire system.

This means:

- Whether or not a system is decentralized can change over time.
- Any system can be called "decentralized" if we define the scope narrowly enough.
- All decentralized systems can be called "centralized" if we define their scope broadly enough.^[The entire Internet could be considered centralized if we include the entire solar system as part of the scope. The "single point of failure" could be the Earth itself, its atmosphere, the Sun, etc. Or, perhaps in the not distant future, a single ISP.]

The narrowing and enlarging of the scope is called the _relativity of decentralization_, and it is why first agreeing on a reasonable definition for a system's scope is vital before deciding whether or not it is "decentralized".

## Computational throughput of consensus systems

\begin{defn}
The $computational\ throughput$ of a consensus system refers to the rate at which the system updates its state by processing all input messages.
\end{defn}

We'll use the shorthand $T(S)$ to represent this concept and note three factors that determine its value:

1. The _computational power_^[This refers to all computational requirements relevant for consensus participation, such as bandwidth, data storage, and processing speed.] of each consensus participant.
2. The amount of time after which the consensus algorithm considers messages to be lost (the _timeout_ period).
3. The consensus _threshold_ that decides when consensus has been reached (i.e. "how big of a quorum is required").

Note that if the computational power of a consensus participant is significantly less than that of the other participants, they are more likely to be excluded from the deciding quorum for several reasons:

- If there are no network partitions to determine otherwise, fast consensus participants will process messages more quickly and therefore will be first to create a quorum.
- If there are enough fast consensus participants to create a large enough quorum to exceed the system's consensus threshold, then there is no need to wait for the remaining votes of the slow participants.
- Slow consensus participants are more likely than fast consensus participants to hit the system's timeout period for processing and responding to messages, and therefore are more at risk of being excluded from the consensus process entirely.

Therefore, $T(S)$ is a function that is limited by the slowest consensus participants not excluded in the deciding quorum.

## Coordination costs

Relevant for our proof is the notion of _coordination costs_, or the difficulty for one entity to engage another and work toward a common goal, because that can result in the formation of a cartel, which in turn violates the requirement that consensus participants be _independent_.

For example, when Bitcoin was first launched, it would be difficult for any miner to find enough collaborating miners to create a cartel with >50% of the hash power, simply because there were many "relevant miners" (consensus participants) distributed all over the world.

Today, however, there are significantly fewer consensus participants in Bitcoin, and it is much easier to (1) identify them, and (2) bring them together to coordinate around some goal. Therefore, we say the coordination costs are lower today than before.

We can approximate the coordination costs $C(S)$ of any consensus system simply as the number of consensus participants:

$$C(S) = \mathtt{num\_consensus\_participants}(\{S\})$$

\begin{figure}

    \centering
    \begin{tikzpicture}
    \begin{axis}[
  	    domain=0:5,
  	    xmin=-0.1, xmax=5.1, ymin=-0.1, ymax=5.1,
  	%   axis equal image,
  	    set layers,
  	    xlabel=Population of potential users,
  	%    xlabel style={scale=0.7},
  	    xticklabels={},
  	    xtick=\empty, ytick=\empty,
  	%    axis line style={opacity=0.3},
  	]
  	\addplot [gray, only marks, mark=* , samples=500, mark size=0.75, on layer=axis background] {5*abs(rand)};
  	\begin{pgfonlayer}{axis foreground}
  		\draw (3.5,3.5) node [
  			ellipse, minimum width=3.7cm, minimum height=2.5cm, fill=pink, opacity=0.6,
  			label={[scale=0.8,fill=white,draw,ultra thin]below:Users of $S_1$}
  		] {};
  		\draw (3.7,3.8) node [
  			ellipse, minimum width=2cm, minimum height=0.9cm, fill=green, opacity=0.5,
  			label={[scale=0.7,fill=white]below:Consensus participants}
  		] {};
  	\end{pgfonlayer}
  	\end{axis}
    \end{tikzpicture}
    \caption{If $S_1$ is a decentralized consensus system, the DCS Theorem states that as the number of users increases (red circle), the number of consensus participants decreases (green circle).}
\end{figure}

# Proof

\begin{theorem}
Decentralized consensus systems centralize at scale when consensus participants maintain full consensus over the entire state of the system.
\end{theorem}

We begin with the following axioms accepted as true:

\begin{axiom}
\label{Ax1}
In any sufficiently large population (at scale), individual access to computational power is distributed unequally. Most have access to average computational power, and a few have access to large amounts.
\end{axiom}

Justification: empirically true.

\begin{axiom}
\label{Ax2}
For any two systems offering the same service to the same large population, the transactional demands of the average user converge at scale.
\end{axiom}

Justification: follows from central limit theorem and the law of large numbers.

\begin{axiom}
\label{Ax3}
Most users of a system do not have the computational power required to store and process all of the messages generated by all of the users of that system at scale.
\end{axiom}

Justification: empirically true.^[And perhaps provably true, though such a proof is beyond the scope of this paper.]

From those axioms, we derive the following lemmas:

\begin{lemma}
\label{Lem1}
Let $S$ be a decentralized consensus system whose consensus participants maintain full consensus over the system's state. Let $T(S)$ refer to its computational throughput and $c$ refer to the average computational power of all historical consensus participants at any relevant instant in time. At scale, $T(S)$ exceeds $c$, and the more users $S$ obtains, the more $T(S)$ exceeds $c$.
\end{lemma}

\begin{figure}

    \centering
    \begin{tikzpicture}
    \begin{axis}[domain  = 1:2,
                 samples = 100,
                 clip = false,
                 xmin    = 1,
                 xmax    = 2,
                 ymin    = 0,
                 ymax    = 1,
                 ytick   = \empty,
                 xtick   = \empty,
                 xlabel  = {Throughput capability},
                 ylabel  = {\# users with capability},
                 xlabel shift = {12pt},
                 % xlabel near ticks,
                 ylabel near ticks,
                 set layers,
                ]
      \addplot[thick, samples=400] {1/x^5};
      % this requires clip=false
      \node [anchor=near xticklabel] at (xticklabel cs:0.05) {slow};
      \node [anchor=near xticklabel] at (xticklabel cs:0.95) {fast};
    \end{axis}
    % we can optionally do it this other way if clip=false isn't set.
    % \node at (rel axis cs:0.03,-.04) {slow};
    % \node at (rel axis cs:0.91,-.04) {fast};
    \end{tikzpicture}
    \caption{Visualization of (Axiom~\ref{Ax1}).}
\label{fig:CP}
\end{figure}

\begin{proof}
This follows directly from Axiom \ref{Ax1}, \ref{Ax3}, and our definition of a decentralized system, which includes the \hyperref[sec:scope]{understanding} that for a system to be considered decentralized, it must be uncompromised, and that in turn means it successfully processes all authorized\footnote{See footnote 1 on page 1.} messages from new users within some interval $S_t$. For it to do this, $T(S)$ must exceed $c$, per (Axiom~\ref{Ax1}) and (Axiom~\ref{Ax3}).
\end{proof}

\begin{lemma}
\label{Lem2}
Let $S$ be a consensus system as in (Lemma~\ref{Lem1}). The coordination costs for $S$, $C(S)$, decrease at scale.
\end{lemma}

\begin{proof}
This follows directly from our proof for (Lemma~\ref{Lem1}) and our definition of $C(S)$. The more $S$ scales, the more $T(s)$ exceeds $c$, and the fewer potential consensus participants are able to participate in consensus. This, in turn, makes it easier for the remaining consensus participants to identify and coordinate with each other.
\end{proof}<!-- Figure~\ref{fig:CPS} visualizes this point.-->

<!--
\begin{figure}

    \centering
    \begin{tikzpicture}
    \begin{axis}[domain  = 0.97:2.3,
                 samples = 100,
                 xmin    = 1,
                 xmax    = 2,
                 ymin    = 0,
                 ymax    = 1,
                 ytick   = \empty,
                 xtick   = \empty,
                 xlabel  = {Throughput capability},
                 ylabel  = {\# users with capability},
                 xlabel near ticks,
                 ylabel near ticks,
                 set layers,
                ]
      \addplot[thick, samples=400] {1/x^5};

      \addplot [draw=none, fill=red!25, domain=1.8:2] {1/x^5} \closedcycle;
      \addplot [draw=none, fill=blue!25, domain=1.6:1.8] {1/x^5} \closedcycle;

      \draw[dashed,thin,color = blue] (axis cs: 1.6, 1 )-- (axis cs: 1.6, -0.5);
      \draw[dashed,thin,color = red] (axis cs: 1.8, 1 )-- (axis cs: 1.8, -0.5);      
      \node[anchor = south] at (rel axis cs:0.94,0) {fast};
      \node[anchor = south] at (rel axis cs:0.07,0) {slow};  
      \node[anchor = north, color = red] at (rel axis cs:0.9,0.8) {$C(S_2)$};
      \node[anchor = north, color = blue] at (rel axis cs:0.7,0.8) {$C(S_1)$};
    \end{axis}
    \end{tikzpicture}
    \caption{Highlighted regions show .. TBD. Show movement of same system at time $t=0$ to $t=1$. Fix vertical lines. Make clear what $C(S)$ represents.}
\label{fig:CPS}
\end{figure}
-->

\begin{lemma}
\label{Lem3}
Let $S$ be a consensus system as in (Lemma~\ref{Lem1}). The probability that $\{S\}$ contains a colluding group capable of censoring transactions increases at scale, and therefore $S$ tends toward centralization at scale.
\end{lemma}

\begin{proof}[Proof of the Main Theorem]
The final lemma restates our original theorem. As coordination costs decrease (Lemma~\ref{Lem2}), the probability of a colluding group (a cartel) increases. The presence of a cartel capable of controlling consensus represents a single point of failure \emph{capable} of preventing the system from fulfilling its intended purpose. The definition of a centralized system is one that has a single point of failure. Therefore, we've shown that the probability of the initially decentralized system becoming centralized increases at scale.

It is also worth considering our definition of \hyperref[sec:triangle]{scale} and the implications of (Axiom~\ref{Ax2}). Per (Axiom~\ref{Ax2}), when a decentralized consensus system $S_1$ scales to the size of a similar centralized consensus system $S_2$, it will experience the same transactional demands as $S_2$. However, $S_2$ may scale to a size that would guarantee cartel formation in $S_1$ if it were to scale to the same size. Therefore, $S_1$ cannot scale to such a size while remaining decentralized, and therefore $S_1$ cannot satisfy our definition of scale.
\end{proof}


<!--
https://tex.stackexchange.com/questions/43610/plotting-bell-shaped-curve-in-tikz-pgf
https://tex.stackexchange.com/questions/352933/drawing-a-normal-distribution-graph
-->

# Getting around the DCS Triangle
\label{AppendixA}

As mentioned, the DCS triangle applies to systems employing "full consensus", or in other words, when all consensus participants are required to fully and independently verify the entire state of the system.

It may be possible to "get around" the DCS Triangle by relaxing our definition of consensus. In this section we'll consider two such approaches.

## Combining DC and DS systems

Let us suppose we have a DC-system that we wish to scale while preserving its decentralization. An example of such a system is Bitcoin.[@Bitcoin2008]

Per the triangle, we know that increasing the system's throughput, $T(S)$, via any mechanism that requires all consensus participants to process the additional data, will result in a reduction in the number of independent consensus participants. And so, instead, we may choose to pair our DC-system with a DS-system in some clever way.

\begin{figure}

    \centering
    \begin{tikzpicture}
    \draw (0,0) node[anchor=north east]{\textbf D} -- (1,2) node[anchor=south]{S} -- (2,0) node[anchor=north west]{\textbf C} -- (0,0);
    \draw [line width=3pt,cap=round,xshift=0.2cm] (0,0) -- (1.6,0);
    \draw (3.5,1) node {\textbf +};
    \draw [dashed,yshift=-0.25cm] (2.6,0) -- (4.4,0);
    \draw [xshift=5cm] (0,0) node[anchor=north east]{C} -- (1,2) node[anchor=south]{\textbf S} -- (2,0) node[anchor=north west]{\textbf D} -- (0,0);
    \draw [xshift=5cm,line width=3pt,cap=round,rotate around={-63.435:(2,0)}] (0,0) -- (1.8,0);
    \end{tikzpicture}
\end{figure}

Our DS-system will give us the scale we're looking for, while our DC-system provides a stable and secure source of "ultimate truth" on an as-needed basis. We can connect the two systems in such a way that our DS-system only requires consensus in rare moments, and when it does it may communicate with our DC-system.

The Lightning Network[@Poon2016] is a real-world example of such a pairing.

## Combining multiple DC systems

Yet another possibility is to combine multiple DC systems to create a super-system of DC _groups_.

This approach explores a middle-ground within the DCS triangle, and is the approach taken by systems like OmniLedger.[@Eleftherios2017]

\begin{figure}

    \centering
    \begin{tikzpicture}
    % See "tikz pgf manual.pdf" for info on options
    % \draw is an abbreviation for \path[draw]
    % \shade is an abbreviation for \path[shade]
    % \shadedraw is an abbreviation for \path[shade,draw]
    \shadedraw[top color=gray!30, middle color=white, shading angle=180] (0,0) node[anchor=north east]{Consensus} -- (1,2) node[anchor=south]{Scale} -- (2,0) node[anchor=north west]{Decentralized} -- (0,0);
    \draw[->,thick] (1,0.3) -- (1,1.6);
    \end{tikzpicture}
\end{figure}

Also known as _sharding,_ each group (or _shard_) of consensus participants no longer has complete knowledge of the entire system state, and therefore must (at least partially) trust the other consensus groups. Transparency techniques, such as merkle tree logs, make it possible to minimize the amount of "faith" groups must place in each other.

Overall system consensus is progressively "sacrificed" as the system scales, but only in small, manageable increments. If the system does not need much inter-group consensus, it can scale significantly without issue. If necessary, a DS-system can be added for additional scale.

# Acknowledgements

Thanks to Trent McConaghy and Andrea Devers for their feedback.

# References
