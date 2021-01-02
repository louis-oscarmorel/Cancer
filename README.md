# Prediction of the most effective treatment for patients with breast cancer

This repository is the fruit of the collaborative work of **Eloi Ancellin**, **Maxime Bouthors**, **Joël Garde**, **Mathieu Juttet**, and **Louis-Oscar Morel**.
It was created as an assignement of the Data Camp course of the Master 2 Data Science of the Polytechnic Institute of Paris during the year 2021.

## Breast Cancer ; An introduction

Breast cancer is the most common cancer in women with 2 million new cases annually worldwide according to the WHO. It alone is responsible for more than 500,000 deaths per year and nearly one in seven women will develop this disease in her lifetime. Breast cancer is detected by mammography, but it is the pathological examination of the tissues taken from the patient that makes it possible to establish the precise diagnosis of breast cancer.

Pathology analysis is a complex process, **the challenge of which is to be able to offer the best treatment to each patient, thereby improving her chances of survival**. Therefore, the pathologist's role is to characterize the tumor so that the oncologist can give the best medicine. The diagnosis is based on the microscopic analysis of the lesion. 

The characterization of the tumor is based on (i) the analysis of its morphology which makes it possible to define its histological type (more than 25 types) and on (ii) its molecular characteristics.

The morphological analysis corresponds to the traditional anatomopathological examination, based on the analysis of cell types, their relationships, and whether or not the overall architecture of the tissue is respected.

Molecular analysis refine the type of tumor. Indeed, the development of therapies specifically targeting certain tumor molecular alterations present only in subgroups of patients, currently allows an increasingly important personalization of cancer treatment. The detection of these molecular abnormalities relies on the quantification of specific proteins in tumor tissue (Immunohistochemistry), the fluorescence quantification of specific genetic elements in tumor cells (FISH), the identification of tumor genomic abnormalities by sequencing of the DNA (NGS) [1 to 8]. Taking these characteristics into account when choosing the therapeutic approach has shown strong impacts on reducing the risk of disease progression (eg 35% for the treatment of metastatic breast cancer with Alpelisib, a molecule prescribed for female patients presenting RH + cancers (immunohistochemical characterization) with the presence of activating genomic mutations of the PIK3CA gene (NGS characterization)).

**It is the tumor precise characterization that makes it possible to better understand the biology of a given patient's cancer and thus to prescribe the most suitable treatment.**


However,**the complexity and number of examinations to perform for the precise characterization of the tumor increases the risk of errors.** For example, the proposal for innovative targeted chemotherapies is based on the combined interpretation by the physician of (i) morphological examination, HE biopsy, (ii) of the Extended Evaluation, (iii) of immunohistochemistry, (iv) of genomic analysis by DNA sequencing. The use of more and more parameters tends to make the diagnosis impracticable by the physician alone.

The development of statistical learning algorithms and Data Science has opened up opportunities for improvement in this field, but are still very limited. Indeed, these developments require access to data that are difficult to obtain, are based on complex interdisciplinary know-how (mathematics, medicine and Computer Science). Recent advances in AI are promising, but operate in a black box, thus slowing the adoption of these solutions by pathologists in the medical community.

### Conclusion:

The complexity of tumor diagnosis requires the development of new solutions allowing the automatic integration of multiparametric morphological and molecular analyzes allowing physician support in their diagnostic process, thus improving their analytical capacities and their ability to offer effective personalized treatments.

## Molecular Biology ; Key concepts to understand the work that needs to be done

**The aim of this project is to find profiles of patients with characteristics associated with a good or bad response to a specific treatment. Depending on the data we have, our goal will be to assign the right treatment for each patient, thus improving their chances of survival.**

The biology of cancer is complex. In this challenge, we will focus on (i) clinical data, such as age, ethnicity etc ...; (ii) the anatomopathological characteristics, ie the grade of the lesion, its stage and its histological type and; (iii) molecular biology, respectively genomic alteration (DNA mutation) and genomic expression (RNAseq) data.


The proposal for highly personalized treatments must take into account this very large amount of information. We will approach here very quickly the fundamental notions of biology so that the reader can understand the data and can work on the dataframe to reduce its dimensions and create relevant composite criteria for his prediction work.


DNA, or deoxyribonucleic acid, is a series of four chemical units called nucleotides (A, T, C, G), the combination of which supports information from living things. In humans, this “hardware” support is located in the nuclei of cells and represents a combination of 3 billion nucleotides grouped together in 23 pairs of chromosomes. The majority of this DNA (70%) is said to be non-coding, ie it does not allow the production of protein. The remaining 30% is divided into 20k-30k pairs of genes. A gene is a portion of DNA that produces messenger RNA (mRNA).


RNA is a sequence of nucleotides (A, U, C, G) which is copied from the DNA model by an enzyme (protein) during the process of "transcription". This mRNA leaves the nucleus of the cell to be then "translated" into protein by a ribosome (RNA/proteic complex). The ribosome matches each RNA nucleotide triplet with an amino acid. The sequence of these amino acids constitutes a protein. Proteins have chemical groups that allow them to influence their environment and are therefore one of the supports of life.


Cancer is characterized by an accumulation of mutations in DNA, causing changes in the function of proteins and therefore in the behavior of cells, making them:
- self-sufficient in growth signals;
- Insensitive to growth inhibiting signals;
- Capable of avoiding apoptosis (cell immortality);
- Capable of replicating indefinitely (infinite growth)
- Capable of inducing angiogenesis and forming metastases.



# Getting started
The starting kit notebook can be found [here](https://github.com/MathieuJuttet/Cancer/blob/main/Starting_kit.ipynb). It provides detailed information on the project and explanations on the data.

## Data Loading and Processing

Collecting large and complete data for tumor characterization is a complex task. We have chosen to base ourselves on the GDC Portal, which aggregates many databases specializing in cancer. The GDC Data Portal is a robust data-driven platform that allows cancer researchers and bioinformaticians to search and download cancer data for analysis.

The GDC Data Portal combines 67 projects focusing on 68 different cancers for a total of 84,392 patients. We were interested in patients with primary breast cancer (9,115 cases). Data retrieval for these 9115 patients was achieved by sending a JSON through the GDC API.
(insert code).

expliquer le travail qui a été fait sur la récuperation des données, son organisation, pourquoi on a viré certaines colonnes etc...
(insert code)


### Clinical Data

### Pathological Data

### Molecular Biology Data

In the era of post-genomic living (Lander, E. et al. Initial sequencing and analysis of the human genome. Nature (2001)), our ability to sequence DNA and integrate numerous biological data allows us to develop increasingly personalized approaches to understanding and treating cancer. In this challenge, in combination with "traditional" criteria for characterizing cancer (ie: clinical and pathological data), we will also be interested in genetic data.

Nous allons nous interesser pour chaque patient aux 50 gènes les plus mutés dans cette population.

connus comme étant impliqués dans les cancers d’une façon générale (gènes les plus mutés dans la population tumorale). Pour chaque gène et pour chaque patient, nous allons essayer d’obtenir 3 informations :

The molecular data that interests us here are of two kinds:
- Genomic data: DNA mutations
- Transcriptomic data: number of mRNA copies that each gene produces.

## Genomic data:

We will be interested in genetic mutations for the 50 most mutated genes in the population of patients with breast cancer.

There are two main types of mutations:
- "Copy Number Variation" (CNV) type mutations and "Single somatic Mutation" (SSM) type mutations.

CNVs are a variation in the copy number of a given gene. Indeed, a gene is a sequence of several thousand nucleotide base pairs. A CNV gain causes an increase in the number of copies of this gene, thus being able to produce more RNA transcripts and therefore potentially more proteins leading to a modification of the biology of the cell. A CNV loss will lead to a disappearance of the gene leading to a loss of the protein and therefore of its biological functionality.

SSMs are so-called ponctual mutations. The ponctual mutation will change one or a few nucleotides in the DNA sequence. This will change the copied RNA and the RNA-copying ribosome will not make the correct amino acid match. Thus, the protein will be modified and therefore its functionality as well.

## Transcriptomic data:

It is extremely relevant to add the so-called “transcriptomic” data to these genomic data. They correspond to the level of expression of the gene. The transcriptome represents the amount of mRNA produced for each gene. It is therefore interesting to look at this level of gene expression because it provides more direct information on the number of proteins and their types than analysis of DNA alone.

## Limitation of this challenge:

The data has been simplified for easier analysis. There are many different types of genomic mutations, involving different biological changes. To simplify this aspect, we produced a relatively arbitrary intermediate score to quantify the importance of the mutations for each gene.

@Maxime: insert code with score and explanation of the choice of scoring.

There are more different RNAs than genes because the process of "alternative RNA splicing" adds a degree of freedom for a gene to encode several different proteins. We have considered here all the mRNAs of a gene as coming from a single transcript.

@Maxime: insert code and explanation.


# Exploratory Data Analysis

Pour que le challenger puisse naviguer dans ces données, nous avons préalablement collecté et formaté ces caractéristiques dans un dataframe de grande dimension (dim*dim). Pour plus d'informations sur l'obtention de ces données: voir la partie **Data loading**.

## Clinical 

Number of cases
Disease Type (histology)
  - number of each subtypes (can we split ductal and lobular ?)
  - Age at Diagnosis for each subtype → statistical difference for each type ? (p-value)
  - Survival for each disease type → statistical difference for each type ? (p-value)
  - General treatment for each subtype ? (Treatment Type in GDC) → normally we just have 1098 cases for which we have pharmaceutical therapy/radiation therapy
      Surgery ?
      Radiotherapie?
      Chemotherapy ?
      Which drugs are used ?


## Genomic Data :

50 most mutated genes
  General number of mutations for each histological subtypes
  Are the three most mutated genes known for being involved with each cancer ? 
  Is the presence of these mutations correlated with bad survival ?
Let's be a little bit more precise : many types of mutations

    SSM
      Types of SSM → Explication Louis. pie chart by histo types ?
      frequency of SSM (by histological type ?)
      People with more than one SSM in the same gene → we’ll have to deal with that.
      Other ?
    CNV
      Types of CNV → Explication Louis. Pie chart by histo types ?
      frequency of CNV (by histological type ?)
      Comparison SSM/CNV
      
Within the mutations : compare top 3 for CNV (in frequency) vs top 3 for SSM → is there a difference ? is it known ? (biblio check Louis)

As we explained in the scientifical background → the impact of genetic mutations on cancer biology mostly depends on protein modification. Having information on the amount of RNA should give additional information (especially in the case of CNV -> is an increase in the number of copies associated with an increase in the number of transcripts?)

## Transcriptomic Data

for how many people did we get the transcriptomic data ?
Correlation (Heatmap) for CNV gain/loss and increase/loss number of transcript for these genes. 
→ focus on HER2 : (HER2 amplification is super important in breast cancer treatment → Target chimio if amplified)
correlation for each histological subtype.
Difference in terms of survival (how to plot that precisely ?


# Submission

Travail de prédiction :

## Best objective : Prediction of the most effective treatment in patients with breast cancer
## Side objective : Histological category prediction
## Side objective : Survival prediction

