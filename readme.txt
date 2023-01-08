## Table of Contents
1. [Project title] (#Project title)
2. [Motivation] (#Motivation)
2. [Screenshots] (#Screenshots)
5. [Code Examples] (#Code Examples)
6. [Main function] (#Main function)
7. [How to use?] (#How to use)
### Project title
***
Gene Mutaion Pattern Visualization
## Motivation
***
It is known that there are about 20,000 genes in humans. 
Each gene has several functions, and some genes are known to be associated with specific diseases. 
Accordingly, in this project, a specific disease called Lung Cancer was selected, and the genes causing Lung Cancer were searched based on the phenotype-Gene relationship, and the mutation patterns appearing in these were analyzed and visualized.
In particular, the goal was to provide more intuitive information through mutation pattern analysis and visualization. 
When checking the variant data in the related database, there is a problem in that it is difficult to confirm the relationship between the mutation and the symptom regarding what kind of mutation has visually occurred and what symptoms the mutation causes. 
Therefore, through this project, we tried to realize a visual increase in understanding of mutation patterns. T
hrough this project, patients with related diseases can better understand their diseases, and researchers want to contribute to the collection of mutation data and other processes for the progress of related research.
##Screenshots
***
https://drive.google.com/drive/folders/1HlaVWZP1420E4EEeJoAicuwDRS_e-oRS?usp=sharing
##Code Example
***
CASP8 = pd.read_csv(path_list[0],header=None)
>#PIK3CA = pd.read_csv(path_list[1],header=None)
>#MAP3K8 = pd.read_csv(path_list[2],header=None)
>#FASLG = pd.read_csv(path_list[3],header=None)
>#IRF1= pd.read_csv(path_list[4],header=None)
>#PPP2R1B = pd.read_csv(path_list[5],header=None)
>#KRAS = pd.read_csv(path_list[6],header=None)
>#ERBB2 = pd.read_csv(path_list[7],header=None)
>#EGFR = pd.read_csv(path_list[8],header=None)
>#BRAF = pd.read_csv(path_list[9],header=None)
>#CYP2A6 = pd.read_csv(path_list[10],header=None)
>#PRKN = pd.read_csv(path_list[11],header=None)
>#ERCC6 = pd.read_csv(path_list[12],header=None)
Put various genes as input values and select genes through annotation processing to visualize
>condition1 = (CASP8['Reference'] == 'A') | (CASP8['Reference'] == 'C') | (CASP8['Reference'] == 'G') | (CASP8['Reference'] == 'T')
>condition2 = (CASP8['Alternate'] == 'A') | (CASP8['Alternate'] == 'C') | (CASP8['Alternate'] == 'G') | (CASP8['Alternate'] == 'T')
Select the continent column. Compare the column values with the condition and assign the result to a new variable.
>figure, (ax1, ax2) = plt.subplots(nrows=1, ncols=2)
>figure.set_size_inches(14,5)
>sns.countplot(data=CASP8[condition1 & condition2], x="Reference", ax=ax1)
>sns.countplot(data=CASP8[condition1 & condition2], x="Alternate", ax=ax2)
Graph reference and alternative data
>figure, (ax1, ax2) = plt.subplots(nrows=1, ncols=2)
>figure.set_size_inches(14,5)
>sns.countplot(data=CASP8[~(condition1 & condition2)], x="Reference", ax=ax1)
>sns.countplot(data=CASP8[~(condition1 & condition2)], x="Alternate", ax=ax2)
Count reference and alternative data and plot the graph according to the type of mutation.
>CASP8_S = CASP8[condition1 & condition2]
>#CASP8_S = CASP8_S['Reference'].str.cat(CASP8_S['Alternate'], sep='>')
>CASP8_S['Reference_Alternate'] = CASP8_S[['Reference', 'Alternate']].apply(lambda x: '>'.join(x), axis=1)
>CASP8_S
>figure, (ax1) = plt.subplots(nrows=1, ncols=1)
>figure.set_size_inches(14,5)
>sns.countplot(data=CASP8_S, x="Reference_Alternate", ax=ax1)
For Reference and Alternate, the distribution of each substitution type by nucleotide type is visualized in a bar chart.
>variants=list(CASP8['VEP Annotation'])
>cnt=0
>for r in range (759): #length of variants
  if variants[r] == 'synonymous_variant':
    cnt = cnt+1
>cnt
>data = [111,648] # data = [num.of synonymous variants, num. of total variants]
>figure, plt.pie(data, labels=['Synonymous Variants', 'Nonsynonymous Variants'], autopct="%.2f%%")
The ratio of Synonymous Variants and Nonsynonymous Variants is expressed in a pie chart.
##Main function
***
The main function of this program is to receive protein mutation data as input and visualize the mutation distribution in various formats. 
And it shows the result of expressing the ratio of Synonymous Variants and Nonsynonymous Variants in a pie chart.
##How to use?
***
Upload gene mutation data to Google Drive, modify the initial path, and load it into the program. 
Alternatively, you can uncomment the already loaded genes and visualize the data.
If you run google colab, you can get the gene mutation visualization result.

