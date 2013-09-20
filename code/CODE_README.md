This folder contains all the scripts you'll need to recreate the analysis pipeline used in this thesis chapter.

It is an update of the method used in:
[*Cobbett, A., Wilkinson, M., and Wills, M. (2007). Fossils impact as hard as living taxa in parsimony analyses of morphology. Systematic Biology, 56(5):753-766*](http://dx.doi.org/10.1080/10635150701627296)


**Assumptions and pre-requisites**

1. This pipeline probably only works on Unix operating systems (Linux/Mac), I used Ubuntu 13.04
2. The cladistic data must be validly formatted for use with TNT
3. You must be able to call *TNT* from any terminal with 'tnt'
4. You must be able to call *PAUP** from any terminal with 'paup'
5. You must have *R* installed along with the package *phangorn* and its dependancies
6. All taxon-names must be unique in the first 10 characters e.g. *Crocodylus\_acutus* and *Crocodylus\_johnsoni* MUST be renamed as their first 10 characters are identical. (This pipeline makes use of PAUP\*'s PHYLIP tree-format export function which automatically truncates names to the first 10 characters)
7. The files provided work for datasets of upto 100 taxa - it's easy to extend them beyond this but you'll have to make some edits here and there.


### Analyzing a dataset

Assuming the dataset you want to test is in a file called *data.tnt* 

**The parsimony analyses**

1. execute *TNT* interactively
2. load in your dataset with *proc data.tnt*
3. do the parsimony analyses required with *proc tntdb.txt* (this executes the instructions in the *tntdb.txt* file, which does all the required parsimony analyses) N.B. by default, equally-weighted analyses are used. If you want to do implied-weighting analyses you may need to change one or two settings. 
4. quit *TNT* once all the searches are done

**Preparing treefiles for analysis within _R_ using PAUP**

5. in the terminal type *paup -n makerefs.txt ; paup -n makejacks.txt ;* \[this will call PAUP non-interactively to convert the output from TNT into separate ref\* and jack\* treefiles for further analysis in *R*\]

**Run _R_ to calculate the mean minimum tree-to-tree distances**

6. Edit the first line of *longtemp.R* to set your working directory
7. Interactively run the *longtemp.R* script in R so you can watch the progress of the calculations, if there are many MPTs to compare it can be very slow...
8. After it has executed you may need to run this command to make sure the mean-minumum treedistance calculations are saved before you exit R:
*write.csv(cbind(meantablerf,meantablepd),file="resultsR.csv")*

You will now have a simple two column csv file of the mean-mininum tree distances between the 'pruned tree set' and the 'jackniffed tree set' for each non-root taxon in your dataset, in the taxon-order that they are in the original matrix *data.tnt*.


**Backwards compatibility with DELBAT/DELSUM**

In order to provide backwards compatibility with the DELBAT/DELSUM scripts that Cobbett et al (2007) used, I have optionally provided the file *paupcmds.txt* which will convert the treefiles into a form amenable to analysis with the old pipeline. It just needs to be run after step 4 to produce all the \*.nex\*.tre files that the DELBAT/DELSUM pipeline needs.




