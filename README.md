# Genome Sequence Analysis with an HMM
## About
In this project, coding regions of S. cerevisiae chromosome III DNA were inferred by modelling regions of the genome using a hidden Markov model (HMM). In <a href="https://github.com/TomMakesThings/Genome-Sequence-Analysis-HMM/blob/main/GSA.ipynb">this Jupyter notebook</a>, the Baum-Welch algorithm has been implemented to estimate the HMM's parameters using the chromosome's encoded %GC as an emitted sequence. The most probable sequence of hidden states representing coding and non-coding regions of DNA is then inferred by applying the Viterbi algorithm.

<img src="https://github.com/TomMakesThings/Genome-Sequence-Analysis-HMM/blob/assets/HMM-State-Diagram.png">

<img src="https://github.com/TomMakesThings/Genome-Sequence-Analysis-HMM/blob/assets/Annotated-Chromosome-Emission.png">

## Data
The FASTA file containing the chromosome for S. cerevisiae was downloaded from <a href="https://www.ncbi.nlm.nih.gov/genome/gdv/browser/genome/?id=GCF_000146045.2">NCBI</a>

To encapsulate the model, I created a Python class HMM. During initialisation, this either
takes the parameters directly or reads them from a file. Parameters include the state space S,
emission space V, transition matrix A, initial distribution μ0, and emission matrix B. Additionally,
the expected emission length is given as a parameter N.

After running the Viterbi algorithm on the binned yeast chromosome, a subset of bins can be plotted and coloured to visualise their predicted states. For example in the plot below, state 0 captures runs of high GC content, while state 1 encodes lower GC content.

Telomeres are repetitive nucleotide sequences found in eukaryotes at the beginning of chromosomes. In most organisms they have a high GC content since they play a protective role against double strand breaks. In the case of *S. cerevisiae* chromosome III, the first 1098 base pairs are known to be the telomeric region TEL03L. The first 9 bins were predicted state 0, effectively identifying the first 900 base pairs belonging to this telomeric region. The telomere is followed by 251bp long terminal repeat and a 744bp dubious open reading frame. As these regions consecutively have lower \%GC, they have been predicted state 1 by the Viterbi algorithm.

In long genomic sequences, higher GC content is indicative of the presence of genes. The next region predicted as state 0 is between bins 23 to 37, i.e. base pairs 2300 to 3700. When compared against the known annotation, the high \%GC in this area can be explained by the presence of two pseudogenes between 2126bp - 2566bp and 2824bp - 3750bp.

Other regions of interest include GEX1, a gene encoding a proton:glutathione antiporter between 6479bp - 8326bp, VBA3, a vacuolar basic amino acid transporter between 9706bp - 11082bp and YCL068C, a putative protein of unknown function between 11503bp - 12285bp. The HMM successfully identifies the location of YCL068C, however only picked up on the first half of GEX1 and did not pinpoint VBA3.
