## **Next-generation sequencing (NGS) Mutation Analysis**

This program automates read validation and mutation mapping for next-generation sequencing (NGS) data. It investigates nucleotide mismatch patterns and substitution profiles associated with genotoxic agents in yeast samples.

### **How to run the program:**

1. Open the project in Google Colab.
2. Run the setup code cells to download the necessary datasets (`reads.csv`, `reference.txt`).
3. Run the notebook cells in order to define the functions and perform the analysis
4. Finally, run the final analysis cell to generate the results.

### **Inputs and Outputs**

**Inputs:**
 - 'reference.txt', a 200-nucleotide FASTA-like reference string
 - 'reads.csv', a CSV containing 6000 aligned sequencing reads (1000 reads per sample), each read 200 nucleotides long.
   
**Outputs:** 
 - Read validation statistics, including valid and invalid read counts.
 - Mismatch frequencies and mutation event counts.
 - Substitution mutation profiles, showing the frequency of different nucleotide substitutions.
 - Mutation position summaries, identifying the most frequently mutated positions.
 - Statistical comparison results, including Welch's t-test statistics and p-values for selected positions between the control and treatment groups.

### **Code design decisions:**

1. I used validate_read to process raw sequencing data, normalising lowercase inputs to uppercase and identifying incorrect sequence lengths or invalid characters. This produces structured validated results, ensuring invalid reads are excluded from downstream mutation analysis.
2. I used conditional statements and appropriate return values([] or None) to handle missing or unavailable data. An empty list represents no mutations, while None represents a percentage that cannot be calculated, as there are no valid reads. This helps prevent downstream numerical errors. 
4. I separated raw data validation from downstream mutation analysis and statistical calculations. This modular approach makes it easier to test, maintain, and scale.

### **Testing summary:**

The functions were tested using controlled datasets with known expected results to verify they actually met the requirements.
1. Read validation and mutation detection: I tested that lowercase sequences such as "atgc" successfully normalised to uppercase, and that the incorrect sequence lengths and invalid characters were correctly identified, including when multiple errors occur in the same read. This also checked that reads identical to the reference sequence return an empty mutation list ([]).

2. Read analysis and sample summaries: I tested that analyse_reads() correctly combined validation and mutation detection, preserves read order, stores normalised sequences and excludes invalid reads from mutation analysis. I also tested that summarise_samples() correctly calculates valid and invalid read counts, mismatch percentages, total mutation events, substitution frequencies and mutation position counts. Both functions were tested with empty inputs, and I checked that the original input data remains unchanged where required.

3. Statistical group comparisons: I tested that compare_positions() correctly identifies the three most frequently mutated positions, calculates individual sample percentages, group means and treatment-control differences, and returns statistical results from Welch's t-test. I also checked sample counts, tied mutation positions and empty input handling.