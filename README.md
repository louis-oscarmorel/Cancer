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


### Clinical Data

### Pathological Data

### Molecular Biology Data

In the era of post-genomic living (Lander, E. et al. Initial sequencing and analysis of the human genome. Nature (2001)), our ability to sequence DNA and integrate numerous biological data allows us to develop increasingly personalized approaches to understanding and treating cancer. In this challenge, in combination with "traditional" criteria for characterizing cancer (ie: clinical and pathological data), we will also be interested in genetic data.

Nous allons nous interesser pour chaque patient aux 50 gènes les plus mutés dans cette population.

connus comme étant impliqués dans les cancers d’une façon générale (gènes les plus mutés dans la population tumorale). Pour chaque gène et pour chaque patient, nous allons essayer d’obtenir 3 informations :

- Statut mutationnel CNV : Gain/Loss/normal/Unknown
	* Le gène peut avoir disparu ou avoir été dupliqué (augmentation du nombre de copies) au cours d’un incident de la machinerie cellulaire (pour plus d’info me demander ou regarder la page wikipédia ‘Replication de l’ADN’-→ anomalie). Ce type de mutation est différent d’une mutation SSM, car elle implique indirectement une augmentation ou diminution du nombre d’ARN produit et donc de protéine à la fin sans modification de la fonction de la protéine.
- Statut mutationnel SSM : type de mutation ponctuelle
	* La mutation ponctuelle va modifier un ou quelques nucléotides dans la séquence d’ADN. L’ARN recopié sera ainsi modifié et le ribosome recopiant l’ARN ne fera pas le bon match d’acide aminé → la protéine sera modifée et donc sa fonction également.
- Niveau d’expression du transcrit
	* Le transcriptome est la quantité d’ARN produit pour chaque gène. Il y a plus d’ARN différents que de gènes car le processus « d’épissage de l’ARN » ajoute un degré de liberté permettant à un gène de coder pour plusieurs protéines différentes. Il est ainsi intéressant de regarder ce niveau d’expression génétique car il renseigne plus directement sur le nombre de protéines et leur types que l’analyse de l’ADN uniquement.


## Exploratory Data Analysis

Pour que le challenger puisse naviguer dans ces données, nous avons préalablement collecté et formater ces caractéristiques dans un dataframe de grande dimension (dim*dim). Pour plus d'informations sur l'obtention de ces données: voir la partie **Data loading**.


