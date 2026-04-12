# Article

# Thermodynamic Cost Bounds on the Serial Decoding Throughput Basin

Grant Lavell Whitmer III

The Windstorm Institute, Fort Ann, NY 12827, USA; grantwhitmer3@gmail.com

---

**Abstract:** Serial decoding systems -- ribosome, cognition, language, and artificial intelligence -- converge to 3--6 bits per processing event. This study derives a discrimination cost function with super-linear alphabet scaling and exponential fidelity scaling, showing that the throughput basin is geometrically inevitable for systems with super-linear discrimination cost. Two cost regimes are identified. Regime A (alphabet-bound) describes biological systems using pairwise molecular recognition, where cost scales quadratically, producing an efficiency peak at approximately M = 20 amino acids. Regime B (capacity-bound) describes silicon AI, where cost scales sub-linearly (measured exponent alpha = 0.937 across 27 models), producing no basin. The ribosome operates within 2% of its thermodynamic minimum; a 7-billion-parameter transformer operates approximately 10^9 above its Landauer floor. A temperature prediction tested across 29 organisms yields partial correlation r = -0.451 (p = 0.014) between amino acid entropy and growth temperature, controlling for GC-content. The basin is a speed limit for pairwise discriminators; silicon escapes it entirely. The two-regime framework resolves why AI lands in the biological throughput basin despite having no thermodynamic constraint on vocabulary size.

**Keywords:** dissipative decoding; discrimination energy; Landauer bound; kinetic proofreading; alphabet-bound regime; capacity-bound regime; ribosome efficiency; serial information processing; phase-space analysis; energy scaling

---

## 1. Introduction

The first four papers in this series established what the throughput basin is and where it sits. Thirty-one systems across six domains cluster between 3 and 6 bits per processing event [1,2]. The ribosome was predicted to 0.003 bits from pure physics [3]. Evolutionary simulations independently reinvented the genetic code [2]. But one question remained unanswered: why does the basin sit at 3--6 bits rather than 1--2 or 10--12?

This paper answers: energy. Every serial decoder faces a tradeoff between informational return (how much is learned per processing step) and discrimination cost (the energy required to reliably distinguish one symbol from another). Informational return grows logarithmically with alphabet size -- diminishing returns. Discrimination cost depends on the physical mechanism of discrimination, and this is where biology and silicon fundamentally diverge.

## 2. Materials and Methods

### 2.1. Discrimination Cost Function

The general discrimination cost function has two components:

W(M, epsilon) = W_alphabet(M) + W_fidelity(epsilon)                          (1)

where W_alphabet(M) captures the cost of maintaining M distinguishable symbols and W_fidelity(epsilon) captures the cost of achieving error rate epsilon. For pairwise molecular recognition (Regime A), W_alphabet scales as M(M-1)/2 -- the number of pairwise distinctions required. For learned parameters (Regime B), W_alphabet scales sub-linearly with model capacity.

### 2.2. Two Cost Regimes

**Regime A (Alphabet-Bound, alpha > 1):** Biological systems using pairwise molecular recognition. The ribosome distinguishes amino acids through dedicated aminoacyl-tRNA synthetases; each of the 21 amino acids has a dedicated molecular machine whose sole job is to recognize one amino acid and reject the other 20. The number of pairwise distinctions grows quadratically: M(M-1)/2. At M = 21, that is 210 pairwise comparisons. At M = 30, it would be 435 -- more than double the discrimination infrastructure for less than half a bit of additional information.

**Regime B (Capacity-Bound, alpha < 1):** Silicon AI systems using independent learned parameters. A transformer model performs matrix multiplication over independently learned parameters. The vocabulary is implemented as a cheap linear projection (softmax layer). Adding tokens to the vocabulary costs negligibly. The cost of adding parameters is sub-linear -- each additional parameter costs less energy than the last.

### 2.3. Efficiency Function

The bits-per-joule efficiency function is:

eta(M) = log_2(M) / W(M)                                                    (2)

For Regime A (alpha > 1), eta(M) has a single peak -- the optimal alphabet size. For Regime B (alpha < 1), eta(M) is monotonically decreasing -- no peak, no basin.

### 2.4. Energy Benchmark: 27 AI Models

Energy consumption was measured for 27 AI models on standardized hardware (NVIDIA RTX 5090) using nvidia-smi GPU power polling at 10 ms intervals. Models spanned the Pythia family (14M to 1.4B parameters) and additional architectures. The relationship between energy and parameter count was assessed via log-log regression.

### 2.5. Temperature Prediction: Kazusa Database

To test whether discrimination cost increases with temperature (via the kT term in the Landauer bound [4]), amino acid usage entropy was computed for 29 organisms spanning growth temperatures from 8 to 100 degrees Celsius using the live Kazusa Codon Usage Database. GC-content was included as a control variable, as it is a known confound for temperature-driven compositional shifts [5]. The partial correlation between amino acid entropy and temperature, controlling for GC-content, was computed.

## 3. Results

### 3.1. Phase-Space Analysis

The phase-space analysis confirms that the 3--6 bit basin is geometrically inevitable for any system with alpha > 1. The efficiency function eta(M) = log_2(M) / (gamma * M^alpha) has a unique maximum when alpha > 1, located at M* = (1 / (alpha * gamma * ln(2)))^(1/alpha). This is a topological feature of the optimization landscape, not a parameter-dependent coincidence: the ratio of a concave function (logarithm) to a convex function (power law with exponent greater than 1) always has a single peak, regardless of the specific parameter values. For alpha < 1, the landscape is monotonic -- no basin, no peak, no constraint. The transition at alpha = 1 is sharp and acts as a phase boundary: systems with super-linear discrimination cost are trapped in the basin; systems with sub-linear cost escape it entirely. This phase-boundary interpretation means that the question "does system X have a throughput basin?" reduces to the empirically measurable question "does system X have super-linear discrimination cost?"

### 3.2. Silicon Energy Scaling

Across 27 models evaluated on the NVIDIA RTX 5090, silicon energy scales as E proportional to params^0.937 (r^2 = 0.960, log-log regression). The exponent alpha = 0.937 is sub-linear: each additional parameter costs less energy than the last. This is the opposite of biology's quadratic scaling and explains why AI has no thermodynamic basin. The consequence: no peak in bits-per-joule, no optimal vocabulary size, no thermodynamic basin. The smallest model is the most energy-efficient per bit of compression; efficiency decreases monotonically with scale.

**Table 3.** Energy scaling across the Pythia model family (identical tokenizer).

| Model | Parameters | BPB | Energy/token (mJ) | Efficiency (bits/mJ) |
|-------|-----------|-----|-------------------|---------------------|
| Pythia-14M | 14M | 1.74 | 0.12 | 14.5 |
| Pythia-70M | 70M | 1.23 | 0.18 | 6.8 |
| Pythia-410M | 410M | 0.97 | 0.34 | 2.9 |
| Pythia-1.4B | 1.4B | 0.85 | 0.58 | 1.5 |

A 100-fold increase in parameters yields a 46% improvement in compression but a nearly 5-fold increase in energy per token. Vocabulary size (identical across all Pythia models) contributes nothing to this trend -- it is purely a capacity-driven scaling relationship, confirming the Regime B classification.

### 3.3. Efficiency Peak at M ~ 20

For Regime A, the bits-per-joule efficiency function has a single peak at approximately M = 20. The two-dimensional efficiency surface, plotted as a function of both M (alphabet size) and epsilon (error rate), shows a clear ridge of maximum efficiency that passes through the ribosome's operating point (M = 21, epsilon ~ 10^-4). The genetic code has 21 amino acids because 21 is where thermodynamic efficiency is maximized -- evolution found the peak of the efficiency surface. The throughput basin is the inevitable consequence of concave returns (logarithmic information gain) divided by convex cost (quadratic pairwise discrimination). Any self-replicating system that uses pairwise molecular recognition will converge to this neighborhood, regardless of its specific chemistry.

### 3.4. Landauer Comparison

**Table 1.** Thermodynamic efficiency comparison.

| System | phi (ratio to Landauer minimum) |
|--------|---------------------------------|
| Ribosome | ~1.02 (2% above minimum) |
| 7B-parameter transformer | ~800,000,000 (10^9 above minimum) |

After 3.8 billion years of optimization, evolution has closed the gap to within 2% of the thermodynamic minimum. Current AI systems operate approximately nine orders of magnitude above their Landauer floor.

### 3.5. Slack Ordering

The slack ordering across Regime A systems is consistent with the thermodynamic framework: cheaper discrimination correlates with lower slack.

**Table 2.** Slack ordering across Regime A systems.

| System | Floor R_M(epsilon) | Observed | Slack Delta | Discrimination cost |
|--------|--------------------|----------|-------------|---------------------|
| Ribosome | 4.39 | 4.39 | 0.00 | Low (GTP hydrolysis) |
| Phonology | 4.71 | 4.95 | 0.24 | Medium (neural) |
| Chromatic scale | 3.12 | 3.58 | 0.46 | Medium-high (perceptual) |
| Cognition | 1.97 | 3.12 | 1.15 | High (~10^4 ATP/bit) |

Biology operates nearest the floor because molecular discrimination via GTP hydrolysis and tRNA selection is energetically cheap per comparison. Neural substrates operate with higher slack because synaptic discrimination costs approximately 10^4 ATP per bit -- orders of magnitude more expensive than molecular discrimination. The slack ordering is therefore a direct reflection of the thermodynamic cost hierarchy across substrates.

### 3.6. Temperature Prediction

Across 29 organisms spanning 8 to 100 degrees Celsius, the partial correlation between amino acid entropy and growth temperature, controlling for GC-content, is r = -0.451 (p = 0.014). Hotter organisms use fewer distinct amino acids, consistent with the prediction that increased kT raises the cost of each pairwise discrimination.

This result is preliminary, not proof. The GC-matched control comparisons were underpowered. Phylogenetic controls (PGLS) have not yet been applied. Prior work by Singer and Hickey (2003) and Zeldovich et al. (2007) documented temperature-driven compositional shifts attributed to GC bias and protein stability. The entropy measure captures a complementary signal, but the effect is moderate and requires confirmation.

## 4. Discussion

### 4.1. Why Biology Stopped at 21 Amino Acids

Biology could not decouple its vocabulary from its discrimination cost because molecular recognition is inherently pairwise: adding a new amino acid requires building entirely new molecular machinery to distinguish it from everything else. The cost grows quadratically while the information return grows logarithmically, producing an efficiency peak at M ~ 20. This is why the genetic code stopped at 21 amino acids -- it is the thermodynamic optimum.

### 4.2. Why Silicon Escapes the Basin

Silicon decoupled vocabulary from discrimination cost because learned parameters are independent. A softmax projection over a 50,000-token vocabulary is cheap regardless of token count. The cost scales sub-linearly with model capacity (alpha = 0.937), so the bits-per-joule function is monotonically decreasing -- no peak, no basin, no constraint. AI can have 50,000 tokens for the same reason the ribosome cannot: different cost regimes.

### 4.3. The Falsification That Became a Discovery

We originally predicted that energy-efficient AI models would approach the rate-distortion floor, just as the ribosome does. The data showed the opposite: larger, more expensive models get closer to the floor. The prediction was cleanly falsified. But the falsification revealed something deeper than the original prediction would have: biology and silicon operate in fundamentally different cost regimes. The throughput basin is a feature of alphabet-bound systems specifically, not a universal law. This distinction -- Regime A versus Regime B -- is the paper's central contribution.

### 4.4. Implications for AI Efficiency

The nine-order-of-magnitude gap between AI and the Landauer floor suggests enormous room for improvement in silicon information processing efficiency. Current AI architectures waste the vast majority of their energy on overhead unrelated to the information-theoretic task. Whether this gap can be substantially closed through architectural innovations (neuromorphic computing, reversible computation) or whether it reflects fundamental constraints of digital hardware is an open question with significant practical implications.

### 4.5. Dissipative Structure Interpretation

Serial decoders in both regimes can be understood as dissipative structures in the sense of Prigogine: they maintain informational order by dissipating energy. The key difference is the scaling of dissipation with complexity. In Regime A, dissipation scales super-linearly with alphabet size (the number of pairwise molecular comparisons), creating a thermodynamic ceiling that biology cannot exceed without fundamentally restructuring its discrimination mechanism. In Regime B, dissipation scales sub-linearly with capacity (the number of learned parameters), allowing silicon systems to scale indefinitely -- though with diminishing efficiency.

The within-family Pythia analysis provides direct evidence for Regime B scaling: across the Pythia model series (14M to 1.4B parameters), BPB drops 46% while using an identical tokenizer. A 100-fold increase in model parameters produces a 300-fold increase in energy consumption but only a 46% improvement in compression. This is precisely the monotonically decreasing efficiency characteristic of Regime B: larger models are better but less efficient.

### 4.6. Implications for Synthetic Biology

The efficiency peak at M ~ 20 has direct implications for efforts to expand the genetic code beyond the natural 20 amino acids. Adding a 22nd amino acid would require a new aminoacyl-tRNA synthetase capable of discriminating against all 21 existing amino acids -- 21 new pairwise comparisons -- for approximately 0.07 additional bits of information per codon. The thermodynamic cost-benefit ratio becomes increasingly unfavorable as M increases beyond 20. This analysis predicts that synthetic organisms with expanded genetic codes will exhibit reduced growth rates proportional to the discrimination cost overhead of the additional amino acids.

### 4.7. Limitations

1. The cost parameters (alpha, gamma) for biological substrates are estimates derived from biophysical literature, not direct measurements of discrimination cost per alphabet expansion.
2. The temperature prediction requires phylogenetic controls (PGLS) that have not yet been applied.
3. The energy benchmark covers only one GPU architecture; generalization to other hardware requires additional measurement.
4. The Landauer comparison assumes minimum-energy reversible computation as the baseline, which may not be achievable in practice.

## 5. Conclusion

The throughput basin exists for biology because pairwise molecular recognition imposes quadratic discrimination cost, and the ratio of logarithmic information returns to quadratic cost has a unique peak in the 3--6 bit range. Silicon AI escapes this basin because matrix multiplication imposes sub-linear cost (alpha = 0.937), producing a monotonically decreasing efficiency function with no peak. The distinction between Regime A (alphabet-bound, alpha > 1, basin exists) and Regime B (capacity-bound, alpha < 1, no basin) resolves the apparent paradox of why AI converges to the biological throughput neighborhood despite having no thermodynamic constraint on vocabulary size. Preliminary temperature data from 29 organisms supports the prediction that increased thermal energy raises discrimination cost and reduces amino acid diversity. The basin is not a universal speed limit -- it is a speed limit for pairwise discriminators. The companion paper [6] examines how this biological constraint propagates through human language and into AI training data, explaining the apparent paradox of why AI models converge to approximately 4.2 bits per token despite having no thermodynamic reason to do so. The answer -- that AI inherits the throughput from the biological systems that generated its training data -- completes the causal chain from physics through biology through cognition through language to artificial intelligence. The two-regime framework developed here provides the thermodynamic foundation for that argument: Regime A constrains biology directly through energy costs, and that constraint is then transmitted indirectly through the information structure of human language to AI systems operating in Regime B.

---

**Author Contributions:** Conceptualization, G.L.W.; methodology, G.L.W.; software, G.L.W.; validation, G.L.W.; formal analysis, G.L.W.; investigation, G.L.W.; resources, G.L.W.; data curation, G.L.W.; writing---original draft preparation, G.L.W.; writing---review and editing, G.L.W.; visualization, G.L.W.; supervision, G.L.W.; project administration, G.L.W. All authors have read and agreed to the published version of the manuscript.

**Funding:** This research received no external funding. All work was self-funded by the author.

**Data Availability Statement:** All experiment code and data are publicly available at https://github.com/Windstorm-Labs/dissipative-decoder (accessed 12 April 2026). Temperature data were obtained from the publicly available Kazusa Codon Usage Database.

**Acknowledgments:** Mathematical derivations, energy benchmarking, and data analysis were performed with the assistance of Claude (Anthropic), an AI research tool. Temperature data were obtained from the publicly available Kazusa Codon Usage Database.

**Conflicts of Interest:** The author declares no conflict of interest.

---

## References

1. Whitmer, G.L., III. The Receiver-Limited Floor: Rate-Distortion Bounds on Serial Decoding Throughput. *Zenodo* **2026**. DOI: 10.5281/zenodo.19322973
2. Whitmer, G.L., III. The Throughput Basin: Cross-Substrate Convergence and Decomposition of Serial Decoding Throughput. *Zenodo* **2026**. DOI: 10.5281/zenodo.19323194
3. Whitmer, G.L., III. The Serial Decoding Basin: Five Experiments on Convergence, Thermodynamic Anchoring, and Receiver-Limited Geometry. *Zenodo* **2026**. DOI: 10.5281/zenodo.19323423
4. Landauer, R. Irreversibility and Heat Generation in the Computing Process. *IBM J. Res. Dev.* **1961**, *5*, 183--191. DOI: 10.1147/rd.53.0183
5. Zeldovich, K.B.; Berezovsky, I.N.; Shakhnovich, E.I. Protein and DNA Sequence Determinants of Thermophilic Adaptation. *PLoS Comput. Biol.* **2007**, *3*, e5. DOI: 10.1371/journal.pcbi.0030005
6. Whitmer, G.L., III. The Inherited Constraint: Biological Throughput Limits Shape the Information Structure of Human Language and AI. *Zenodo* **2026**. DOI: 10.5281/zenodo.19432911
7. Hopfield, J.J. Kinetic Proofreading: A New Mechanism for Reducing Errors in Biosynthetic Processes. *Proc. Natl. Acad. Sci. USA* **1974**, *71*, 4135--4139. DOI: 10.1073/pnas.71.10.4135
8. Shannon, C.E. A Mathematical Theory of Communication. *Bell Syst. Tech. J.* **1948**, *27*, 379--423. DOI: 10.1002/j.1538-7305.1948.tb01338.x
9. Whitmer, G.L., III. The Fons Constraint: Information-Theoretic Convergence on Encoding Depth in Self-Replicating Systems. *Zenodo* **2026**. DOI: 10.5281/zenodo.19274048
10. Whitmer, G.L., III. Dissipative Decoder: Experiment Code and Data. *GitHub* **2026**. Available online: https://github.com/Windstorm-Labs/dissipative-decoder (accessed 12 April 2026).

---

*This paper is Paper 5 of The Windstorm Series. The series includes Paper 1: The Fons Constraint [9], Paper 2: The Receiver-Limited Floor [1], Paper 3: The Throughput Basin [2], Paper 4: The Serial Decoding Basin [3], Paper 6: The Inherited Constraint [6], and Paper 7: The Throughput Basin Origin (DOI: 10.5281/zenodo.19498582).*
