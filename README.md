Next-generation sequencing (NGS) Mutation Analysis
This program automates read validation and mutation mapping for NGS to investigate nucleotide mismatch patterns and signatures induced by genotoxic agents in yeast samples.

To run the program: open the project in Google Colab, execute the setup code cells to download the necessary datasets (`reads.csv`, `reference.txt`), and run the final analysis cell to execute the analysis.

Inputs: a 200-nucleotide reference string and a CSV containing 6000 aligned sequencing reads, 1000 reads per sample.
Outputs: summary validation statistics, mismatch frequencies, substitution mutation profiles and statistical t-test metrics for highly mutated positions.

Code design decisions: 
1. I used validate_read to handle raw experimental data, repairing lowercase inputs into uppercase, compiling an error list with tags such as wrong_length and invalid_characters, and returning structured validated data that ensures faulty reads do not ruin downstream loops.
2. To avoid issues arising from missing data, I used the if/else function to employ [] or None; this prevents downstream numerical errors and preserves the dataset integrity without dropping data. 
3. I separated raw data cleansing from downstream statistical analysis to create a base that is easier to test, maintain and scale.

Testing summary: 
Testing (~60 words describing three informative tests you performed)
