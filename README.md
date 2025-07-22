#  Variant Impact Analysis: Clinvar-based-variant-impact-study


##  Project Overview

This project aims to simulate a diagnostic gene panel analysis by evaluating and interpreting variants from three disease-relevant genes: **BRCA1**, **CFTR**, and **GJB2**. Using publicly available databases and prediction tools, I assess the clinical significance of each variant by comparing computational scores with known ClinVar annotations.

The goal is to demonstrate how computational predictions like SIFT, PolyPhen-2, MutationTaster, and CADD align or conflict with clinical significance labels. This helps build an understanding of variant interpretation pipelines .
---


##  Full Project Report

You can view or download the complete Project Summary report here:

 [View Report](https://github.com/AbhishiktaPradhan-code/Clinvar-based-variant-impact-study/blob/main/Project_Report.pdf)



##  Total Variants Studied

| Gene  | Variants |
|-------|----------|
| BRCA1 | 6        |
| CFTR  | 7        |
| GJB2  | 7        |
| **Total** | **20** variants |

---

##  Example Variant Entry

| Variant           | ClinVar Label           | SIFT    | PolyPhen | MutationTaster | CADD | Interpretation Summary |
|------------------|-------------------------|---------|----------|----------------|------|-------------------------|
| 17:43045726C>A   | Benign/Likely benign    | 0 (Del) | 0.263 (Benign) | Deleterious    | 22.6 | Tools predict harm, but ClinVar and PolyPhen suggest benign — likely a false positive. |

---

##  Tools & Databases Used

- [**ClinVar**](https://www.ncbi.nlm.nih.gov/clinvar/) – for clinical significance annotations  
- [**dbSNP**](https://www.ncbi.nlm.nih.gov/snp/) – for variant IDs and genomic positions  
- [**Ensembl VEP**](https://www.ensembl.org/Tools/VEP) – for annotation, SIFT, PolyPhen, and consequence terms  
- [**MutationTaster**](https://www.mutationtaster.org/) – for disease-causing prediction  
- [**CADD**](https://cadd.gs.washington.edu/) – for combined annotation-dependent deleteriousness scores  
---


##  Predictive Pipeline for Interpreting Genomic Variants
![Pipeline](https://github.com/AbhishiktaPradhan-code/Clinvar-based-variant-impact-study/blob/main/variant_pipeline_diagram.png)


##  Technical Note

This project is **entirely tool-based** (no coding). All analyses were conducted using:

-  Online tools (VEP, MutationTaster, PolyPhen, SIFT, CADD)
-  Excel / Google Sheets for variant merging and scoring
-  BioRender  exports for figure creation



##  Selected Genes for the project

This diagnostic gene panel includes three clinically significant genes, each with well-characterized pathogenic and benign variants. These genes were selected based on their medical relevance, availability of variant data in public databases, and their utility in evaluating variant interpretation tools such as SIFT, PolyPhen-2, CADD, and MutationTaster.

## 🔬 Selected Genes for Diagnostic Variant Impact Analysis

---

###  BRCA1 – *Hereditary Breast & Ovarian Cancer*
- **Inheritance:** Autosomal Dominant  
- **Function:** Tumor suppressor involved in DNA repair (especially double-strand breaks) and transcriptional regulation.  
- **Clinical Relevance:** Accounts for ~40% of inherited breast cancers and >80% of combined breast–ovarian cancer cases. A gold-standard gene in cancer diagnostics.

---

###  CFTR – *Cystic Fibrosis*
- **Inheritance:** Autosomal Recessive  
- **Function:** Chloride ion channel regulating salt/water transport in epithelial tissues.  
- **Clinical Relevance:** Causes cystic fibrosis; ΔF508 is the most common pathogenic variant. One of the most well-studied Mendelian disorders.

---

###  GJB2 – *Non-syndromic Hearing Loss*
- **Inheritance:** Autosomal Recessive  
- **Function:** Encodes connexin 26, enabling ion flow in cochlear cells via gap junctions.  
- **Clinical Relevance:** Leading cause of inherited childhood hearing loss (~50% of cases). Offers diagnostic insight into sensory disorders.
 
##  Understanding Prediction Tool Discrepancies


| **Tool**         | **Primary Focus**              | **Key Factors Considered**                             |
|------------------|--------------------------------|---------------------------------------------------------|
| **SIFT**         | Protein function disruption    | Sequence conservation, amino acid substitution         |
| **PolyPhen-2**   | Structural protein impact      | 3D structure, domains, chemical properties              |
| **MutationTaster** | Disease relevance              | Gene models, known variants, splice impact, conservation |
| **CADD**         | Overall variant deleteriousness| Integrated score from multiple genomic annotations      |

###  Tool Comparison Table
![Tools](https://github.com/AbhishiktaPradhan-code/Clinvar-based-variant-impact-study/blob/main/Tool%20Comparison%20Table.png)

###  Why Do Predictions Differ?

- **Transcript dependency**: Some tools score variants based on specific transcripts (e.g. MANE vs others). A variant might be missense in one transcript, UTR in another.
- **Conservation bias**: Tools like SIFT weigh sequence conservation heavily. Variants in less-conserved regions may be scored as benign despite functional relevance.
- **Scope mismatch**: CADD integrates regulatory and epigenetic features, while SIFT and PolyPhen are limited to protein-coding consequences.
- **Protein context**: MutationTaster may factor in broader gene context or clinical relevance, explaining why it sometimes flags more variants as “disease-causing.”

---

###  Takeaway

These differences emphasize the importance of:
- Using **multiple tools** for variant evaluation.
- Interpreting predictions **in combination with clinical databases** like **ClinVar**.
- Making room for **functional annotations and transcript-aware scoring**.


Note: MutationTaster “Score” reflects internal classifier strength, not probability. Not intended for cross-variant comparisons. Use only as supporting info.

###  Pathogenicity Classification Decision Tree
![Decision Tree](https://github.com/AbhishiktaPradhan-code/Clinvar-based-variant-impact-study/blob/main/Pathogenicity%20Classification%20Decision%20Tree.png)


##  Variant Impact Summary 

#  BRCA1: Master Variant Impact Analysis


Below is the master summary table of all interpreted variants, integrating clinical classification (ClinVar) with computational predictions from SIFT, PolyPhen-2, MutationTaster, and CADD.

###  Variant Interpretation Table

| **Variant**     | **AA Change** | **MutationTaster** | **ClinVar Significance**     | **CADD PHRED** | **SIFT**                            | **PolyPhen**              | **Variant Type**           | **Notes** |
| --------------- | ------------- | ------------------ | ---------------------------- | -------------- | ----------------------------------- | ------------------------- | -------------------------- | --------- |
| 17:43045685T>A  | H1862L        | Deleterious (99)   | Benign/Likely benign         | 10.58          | deleterious\_low\_confidence (0.01) | benign (0.013)            | SNV (missense, UTR)        | MANE      |
| 17:43045726C>A  | Q1848H        | Deleterious (24)   | Benign/Likely benign         | 22.6           | deleterious (0)                     | benign (0.263)            | SNV (synonymous, UTR)      | MANE      |
| 17:43045752A>AG | Stop lost     | Deleterious        | Pathogenic/Likely pathogenic | 27.1           | N/A                                 | N/A                       | Insertion (frameshift)     | MANE      |
| 17:43045759C>A  | W1837C        | Deleterious (215)  | Pathogenic/Likely pathogenic | 27.6           | deleterious (0)                     | probably damaging (0.991) | SNV (missense, UTR)        | MANE      |
| 17:43045784T>TA | Stop lost     | Deleterious        | Pathogenic                   | 36             | N/A                                 | N/A                       | Duplication (stop lost)    | MANE      |
| 17:43047654T>A  | N1819I        | Benign (149)       | Benign/Likely benign         | 7.686          | deleterious (0)                     | benign (0.015)            | SNV (missense, synonymous) | MANE      |

---

##   Observations & Reflections (BRCA1)

*  **Stop-lost and frameshift variants** are strongly predicted as pathogenic (e.g., CADD > 27, MT = Deleterious), aligning with known functional impact.
*  **Mixed predictions** seen for `17:43045726C>A`  SIFT predicts deleterious, but PolyPhen and ClinVar disagree → highlights need for clinical context.
*  **SIFT can produce false positives** in variants labeled benign by ClinVar, especially in genes tolerant to missense mutations.
*  **CADD scores show good alignment** with known pathogenic variants (>25), but scores between 10–20 are often ambiguous.



#  CFTR: Master Variant Impact Analysis

##  Summary Table

| Variant | MutationTaster | AA Change | ClinVar Significance | CADD | Variant Type | SIFT | PolyPhen | Molecular Consequence |
|--------|----------------|-----------|------------------------|------|---------------|-------|----------|------------------------|
| 7:117479208C>T | Benign | – | Benign/Likely benign | 6.987 | SNV | N/A | N/A | – |
| 7:117479208G>C | Benign | – | Benign/Likely benign | – | SNV | N/A | N/A | – |
| 7:117480097G>A | Deleterious | M1? (initiator loss) | Pathogenic/Likely pathogenic | 24.9 | SNV | deleterious_low_confidence(0) | benign(0.362) | missense / initiator codon |
| 7:117480117insG | Deleterious | A9Gfs*36 | Pathogenic/Likely pathogenic | 21.8 | Duplication | N/A | N/A | Frameshift |
| 7:117480134delAAACT | Deleterious | F16Tfs*30 | Pathogenic | 38 | Deletion | N/A | N/A | Frameshift |
| 7:117531108insCC | Deleterious | K162Pfs*5 | Pathogenic/Likely pathogenic | – | Insertion | N/A | N/A | Frameshift |
| 7:117535451A>G | Benign | – | Benign | – | SNV | N/A | N/A | Intron variant |

##  Interpretation Summary

- **Frameshift variants** (e.g., A9Gfs*36, F16Tfs*30, K162Pfs*5) are consistently marked as **pathogenic** by tools and ClinVar  reflecting strong disruption of CFTR protein structure.
- **Initiator codon loss** (`M1`) is interpreted as deleterious due to loss of normal translation start  supported by CADD and MutationTaster.
- **Two common SNVs** (C>T and G>C at 7:117479208) are unanimously predicted as benign, with low CADD scores or no protein consequence.
- **Intronic variant** (7:117535451A>G) is likely benign with no splicing or functional implications, matching ClinVar annotation.
- **No major disagreement** exists between tools and ClinVar for CFTR  predictions show high consensus in this dataset.


##  GJB2 Master Variant Impact Table

| Variant | MutationTaster | CADD PHRED | AA Change | Variant Type | SIFT | PolyPhen | ClinVar Label | Molecular Consequence |
|--------|----------------|-------------|------------|---------------|------|-----------|----------------|------------------------|
| 13:20188790G>A | Benign | 4.39 | – | Single nucleotide variant | N/A | N/A | Benign | 3′ UTR variant |
| 13:20188817A>C | Benign | 15.06 | – | Single nucleotide variant | N/A | N/A | Benign | 3′ UTR variant |
| 13:20188976insAAATT... | Deleterious | – | C202Wfs*10 | Duplication | N/A | N/A | Pathogenic/Likely pathogenic | Nonsense |
| 13:20189006delTG | Deleterious | – | V193Cfs*3 | Microsatellite | N/A | N/A | Pathogenic/Likely pathogenic | Frameshift variant |
| 13:20189017delCT | – | – | – | Deletion | N/A | N/A | Pathogenic/Likely pathogenic | Frameshift variant |
| 13:20189125C>A | Benign | 20.4 | V153F | Single nucleotide variant | Tolerated_low_confidence (0.19) | N/A | Benign/Likely benign | Missense variant |
| 13:20189303C>G | Deleterious | 25.1 | M93I | Single nucleotide variant | Deleterious_low_confidence (0) | N/A | Pathogenic/Likely pathogenic | Missense variant |

---

###  GJB2 Variant Interpretation Summary

- **Stop-lost and frameshift variants** (`13:20188976ins...`, `13:20189006delTG`, `13:20189017delCT`) are consistently predicted as **deleterious** by MutationTaster and labeled **Pathogenic/Likely pathogenic** in ClinVar, supporting strong concordance between computational tools and clinical annotations.

- **Missense variant `13:20189303C>G (M93I)`** is flagged as **deleterious** by MutationTaster and SIFT and also marked **Pathogenic** by ClinVar, demonstrating high confidence in functional impact.

- **Benign predictions** (`13:20188790G>A`, `13:20188817A>C`) lie in the **3′ UTR**, which is non-coding and often tolerates variation. Their **low CADD scores** and **benign ClinVar status** confirm low likelihood of disease relevance.

- **Mixed predictions for `13:20189125C>A (V153F)`**: CADD is **moderately high (20.4)**, but SIFT gives **low-confidence tolerance**, and ClinVar still classifies it as **Benign/Likely benign**, suggesting it may lie in a **non-critical or tolerated protein region**.

- **Overall**, **coding-region variants** with truncating or frameshift effects align well across all tools and ClinVar, whereas **non-coding UTR variants** tend to show consistent benign predictions.
