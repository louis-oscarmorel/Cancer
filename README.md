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





## Get started
The starting kit notebook can be found [here](https://github.com/MathieuJuttet/Cancer/blob/main/Starting_kit.ipynb). It provides detailed information on the project and explanations on the data.

Début topo projet : 

Le but de ce projet est de trouver des profils de patients ayant des caractéristiques  associées à une bonne ou mauvaise réponse à un traitement spécifique. Ainsi, en fonction des données dont nous disposerons, notre but sera d’affecter le bon traitement correspondant pour chaque patient ainsi améliorant sa survie.

La biologie du cancer est complexe. Ainsi, nous avons beaucoup d’élements pour essayer de le caractériser précisément et proposer le meilleur traitement possible.

Historiquement, on se base sur des données cliniques :
- Liste des données cliniques

La médecine du Xxème siècle se base sur les données anatomopathologiques :
Classification pTMN, Type histologique etc..

La médecine du XXI combine a celles-ci les données moléculaires de la tumeur pour gagner de la précision dans l’orientation thérapeutique.

ADN : ‘hardware’ du monde vivant se trouvant chez l’homme dans le noyau des cellules. Il est le même pour chaque cellules d’un individu (quasiment à quelques mutations près). C’est une suite d’unités appelées nucléotides (A,T,C,G). Un gène : une portion d’ADN qui produit un ARN. 

L’ARN est une suite nucléotidique (A,U,C,G) qui est recopié sur le modèle de l’ADN par une enzyme (protéine) au cours du processus de la « transcription ». Cet ARN sort du noyau de la cellule pour être « traduit » en protéine par un ribosome. Le ribosome fait correspondre à chaque triplet de nucléotide de l’ARN un acide aminé. La suite des acides aminés constitue une protéine. Les protéines ont des groupements chimiques leur permettant d’avoir une influence sur leur environnement et sont donc l’un des support de la vie.

Le cancer est caractérisé par une accumulation de mutations au niveau de l’ADN, entrainant une modification de la fonction des protéines et donc du comportement des cellules, les rendant :
- Immortelles
- Proliférantes
- Instables d’un point de vue génétique (vont faire de plus en plus de mutations).
- etc...

On va s’intéresser pour chaque patient à 50 gènes connus comme étant impliqués dans les cancers d’une façon générale (gènes les plus mutés dans la population tumorale). Pour chaque gène et pour chaque patient, nous allons essayer d’obtenir 3 informations :

- Statut mutationnel CNV : Gain/Loss/normal/Unknown
	* Le gène peut avoir disparu ou avoir été dupliqué (augmentation du nombre de copies) au cours d’un incident de la machinerie cellulaire (pour plus d’info me demander ou regarder la page wikipédia ‘Replication de l’ADN’-→ anomalie). Ce type de mutation est différent d’une mutation SSM, car elle implique indirectement une augmentation ou diminution du nombre d’ARN produit et donc de protéine à la fin sans modification de la fonction de la protéine.
- Statut mutationnel SSM : type de mutation ponctuelle
	* La mutation ponctuelle va modifier un ou quelques nucléotides dans la séquence d’ADN. L’ARN recopié sera ainsi modifié et le ribosome recopiant l’ARN ne fera pas le bon match d’acide aminé → la protéine sera modifée et donc sa fonction également.
- Niveau d’expression du transcrit
	* Le transcriptome est la quantité d’ARN produit pour chaque gène. Il y a plus d’ARN différents que de gènes car le processus « d’épissage de l’ARN » ajoute un degré de liberté permettant à un gène de coder pour plusieurs protéines différentes. Il est ainsi intéressant de regarder ce niveau d’expression génétique car il renseigne plus directement sur le nombre de protéines et leur types que l’analyse de l’ADN uniquement.
