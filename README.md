# Integrative-Multi-Omics-Analysis-of-Amphotericin-B-Resistance-in-Leishmania-mexicana

# Overview
- This project investigates Amphotericin B resistance in Leishmania mexicana using an integrative multi-omics approach combining genomics, metabolomics, and structural biology.
- By linking genetic variation → metabolic rewiring → protein-level effects, this study reveals a multi-layered mechanism of drug resistance.

# Key Findings
- Identified 29,755 SNPs, with 419 unique to resistant strain
- Discovered CYP51 N176I mutation in sterol biosynthesis pathway
- Observed ergosterol depletion and accumulation of alternative sterols
- Structural modeling shows:
  - No major fold change
  - Increased protein stability
  - Reduced protein–protein interaction

# 1. Genomics: Identifying Resistance Variants
## Variant Validation (IGV)
A high-confidence A>T SNP in CYP51 (chr11:443299) is uniquely present in the amphotericin B-resistant strain, with strong read support and no heterogeneity.

## Pipeline Summary
```bash
fastqc *.fastq -o qc/
trim_galore --phred64 --paired R1.fastq R2.fastq
bowtie2 -x ref -1 R1 -2 R2 -S output.sam
samtools sort output.sam -o sorted.bam
freebayes -f ref.fa sorted.bam > variants.vcf
vcffilter -f "QUAL > 20" variants.vcf > filtered.vcf
snpEff annotate filtered.vcf > annotated.vcf
```
# 2. Metabolomics: Detecting Biochemical Changes
## Global Metabolic Shift
PCA shows clear separation between wild-type and resistant strains (PC1 = 56.8%), indicating large-scale metabolic reprogramming
## Differential Metabolites
346 significantly altered features (p < 0.05), confirming widespread metabolic disruption.
## Ergosterol Depletion
Peak 655 (ergosterol candidate) is strongly reduced in resistant strains, suggesting loss of Amphotericin B target.
## Alternative Sterol Accumulation
Multiple sterol-like intermediates are enriched in resistant strains, indicating pathway rerouting.

# 3. Structural Biology: Mechanistic Insight
## Protein Structure Comparison
The N176I mutation does not disrupt overall CYP51 structure, suggesting resistance is not due to protein misfolding.
## Substrate Docking
Similar binding energies between WT and mutant indicate that substrate binding is preserved.
## Molecular Dynamics
The mutant protein shows reduced radius of gyration, indicating increased compactness and structural stability.

# Integrated Mechanism of Resistance
This study supports a multi-layered resistance mechanism:
- Genomics → CYP51 N176I mutation
- Metabolomics → Loss of ergosterol + accumulation of alternative sterols
- Structural biology → Altered protein dynamics and reduced enzyme interactions
- Together, these changes disrupt ergosterol biosynthesis and reduce Amphotericin B efficacy.
  
# Reproducibility Note
This workflow was originally executed on a university HPC cluster.
Commands provided here are reconstructed to reflect the analytical steps and ensure reproducibility.
