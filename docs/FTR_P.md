# Adapter Removal using PoreChop <img src="figures/ONT.png" height="40px">

[{% octicon arrow-left height:32 class:"right left" vertical-align:middle aria-label:hi %}](FTR.md) [{% octicon home height:32 class:"right left" aria-label:hi %}](index.md) [{% octicon arrow-right height:32 class:"right left" aria-label:hi %}](ASS.md)

Similar to 2nd generation sequencing platforms data from most 3rd generation sequencing platforms contain linker, barcode or adapter sequences at the read beginning or end. Additionally, some sometimes artificial sequences are also included in the middle, e.g., for 2D library preparations of Oxford Nanopore sequencers. 

Although ONT's new basecaller *Guppy* can trim adapters (if told to) it might be a good idea to check and remove additional/overlooked adapters. Multiple tools exist for adapter trimming and filtering for 2nd generation Illumina reads, e.g. [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic). In contrast, currently only one tools exists for trimming of Oxford Nanopore adapters: Porechop. <u>Unfortunately, the development of porechop is discontinued and it might not work for new library preparation kits</u>. However, for completeness I still include it in this practical as it may be useful for the older “standard” library preparation kits. Let’s hope that the developer (Ryan Wick) will find someone to continue the development.

Create a directory *porechop* in the directory *~/course_data/practicals/trimming_practical* and use porechop to remove adapters from the (pre-compiled) guppy reads we used in the basecalling tutorial.

```
mkdir ~/course_data/practicals/trimming_practical/porechop

porechop –i ~/course_data/precompiled/guppy_output/all_guppy.fastq \
-o trimming_practical/porechop/porechopped.fastq --discard_middle
```
<br>
<div style="background-color:#fcfce5;border-radius:5px;border-style:solid;border-color:gray;padding:5px">
  {% octicon info height:32 class:"right left" aria-label:hi %} 
  The “\” at the end of each line is only for convenience to write a long command into several lines. It tells the command-line that all lines still belong together although the are separated by “enter” keys. However, if you type all of the command, i.e., paths etc, in one line don’t’ use the backslash at the end of the lines.
</div>

The above command will use the default values of porechop to search for adapters in all fastq files of the input directory, trim the reads and write them to file porechopped.fastq in the created porechop directory.  The “--discard_middle” option will remove reads with internal adapters (needed for 2D libraries and downstream us of  nanopolish).

<div style="background-color:#cfedfe;border-radius:5px;border-style:solid;border-color:gray;padding:5px">
  {% octicon question height:32 class:"right left" aria-label:hi %} 
  <ol>
    <li>How many adapters did porechop remove?</li>
    <li>Did it discard any reads? Why not?</li>
  </ol>
</div>
[Answers](APP_ANS.md#1-how-many-adapters-did-porechop-remove)

## QC after trimming

Use the tool FastQC to look at your data and compare it to the un-chopped data (see the QC_practical for an introduction to FastQC). 

 1. Open FastQC by typing fastqc on the command line
 2. Use the File->Open menu in FastQC to first open the raw (concatenated) guppy fastq file
 3. When FastQC is done with the first file open the chopped fastq file

<div style="background-color:#cfedfe;border-radius:5px;border-style:solid;border-color:gray;padding:5px">
  {% octicon question height:32 class:"right left" aria-label:hi %} 
  <ol start="3">
    <li>Inspect the different graphs. Did the porechop step improve the data? If so, which parts were improved?</li>
    <li>Are there still areas of the sequences that you’d like to improve?</li>
  </ol>
</div>
[Answers](APP_ANS.md#3-inspect-the-different-graphs-did-the-porechop-step-improve-the-data-if-so-which-parts-were-improved)
