<div align="center">
  <h1><b>Genome Sequence Analysis with an HMM</b></h1>
  <img src="https://images.weserv.nl/?url=avatars.githubusercontent.com/u/61354833?v=4&h=100&w=100&fit=cover&mask=circle&maxage=7d">
  <p><b>🧬 Code by <a href="https://github.com/TomMakesThings">TomMakesThings</a></b> 🧬</p>
  <p><b><sub>October 2021</sub></b></p>
</div>

---

## Methodology
In <a href="https://github.com/TomMakesThings/Genome-Sequence-Analysis-HMM/blob/main/GSA.ipynb">this Jupyter notebook</a>, coding regions of <a href="https://www.ncbi.nlm.nih.gov/genome/gdv/browser/genome/?id=GCF_000146045.2">*S. cerevisiae* chromosome III</a> DNA were inferred by modelling regions of the genome via a hidden Markov model (HMM). The chromosome was binned into 100 base-pair long windows and the percentage of G and C per window calculated. The %GC per window was then labelled with one of five possible categories, e.g. %GC < 33%, and the encoded genome modelled as an emitted sequence of the HMM. This allowed the Baum-Welch algorithm to be run to estimate the HMM's parameters. The coding and non-coding regions of DNA could then inferred through estimating the most probable sequence of hidden states via the Viterbi algorithm.

<img src="https://github.com/TomMakesThings/Genome-Sequence-Analysis-HMM/blob/assets/Images/HMM-State-Diagram.png">
<sub>Figure (A) HMM state transition diagram is shown in the centre, with number above each arrow depicting the inferred probability of jumping from one state to another, e.g. there is a 9% probability of transitioning from a coding to non-coding region. To the left/right are the probabilities of the HMM emitting different %GC depending on whether the model is in the coding or non-coding state.</sub>

## Results
Looking at the first 150 windows of encoded *S. cerevisiae* chromosome III, the first 9 were predicted to be a coding region. This is because the first 1,098 base pairs are known to be the telomeric region TEL03L, and in most organisms telomeric regions have high %GC. The telomere is followed by 251bp long terminal repeat and a 744bp dubious open reading frame. As these regions consecutively have lower %GC, they have been predicted non-coding by the Viterbi algorithm.

In long genomic sequences, higher %GC is indicative of the presence of genes. The next region predicted as coding is between bins 23 to 37, i.e. base pairs 2300 to 3700. When compared against the known annotation, the high %GC in this area can be explained by the presence of two pseudogenes between 2126bp - 2566bp and 2824bp - 3750bp.

Other regions of interest include GEX1, a gene encoding a proton:glutathione antiporter between 6479bp - 8326bp, VBA3, a vacuolar basic amino acid transporter between 9706bp - 11082bp and YCL068C, a putative protein of unknown function between 11503bp - 12285bp. The HMM successfully identifies the location of YCL068C, however it is not always precise demonstrated as it only picked up on the first half of GEX1 and did not pinpoint VBA3.

<img src="https://github.com/TomMakesThings/Genome-Sequence-Analysis-HMM/blob/assets/Images/Annotated-Chromosome-Emission.png">
<sub>Figure (B) 100bp windows of S. cerevisiae chromosome III (x-axis), their %GC (y-axis) and the HMM's predicted state. Known coding regions of the genome are annotated in grey via the reference below. A higher emitted value represents higher %GC, with 1 representing %GC < 33 and 5 representing %GC > 45. A predicted state of 0 indicates the HMM predicted a coding region, while 1 indicates a prediction of a non-coding region.</sub>
