# **Introduction to Phylogenetics**

Welcome to the *Introduction to Phylogenetics* module

This course provides a hands-on overview of molecular phylogenetics

---

## 🕒 **Timetable**
> _Subject to change depending on the pace of the class._

| Time | Topic |
|------|-------|
| **09:30 – 10:30** |  Introduction to molecular phylogenetics |
| **10:30 – 11:15** |  Multiple sequence alignment |
| **11:15 – 11:30** |  Break |
| **11:30 – 12:30** |  Phylogenetic tree inference |
| **12:30 – 13:30** |  Lunch Break |
| **13:30 – 14:00** |  *Practical:* Phylogenetic inference with IQ-TREE |
| **14:00 – 15:00** |  Assessing tree confidence with bootstrap (*IQ-TREE*) |
| **15:00 – 15:15** |  Break |
| **15:15 – 16:30** |  *Practical:* Bayesian inference with BEAST |
| **16:30 – 17:30** |  *Practical:* Viral Phylogeography with BEAST |

---

##  **Software Setup**

>  Computers for the workshop will already be configured.  
> _Optional:_ Follow these steps if using your own computer.

###  Install the following:
- **FigTree**  
- **MAFFT**  
- **IQ-TREE v2**  
- **BEAGLE**  
- **BEAST v1**  
- **Tracer**

📁 Data used in this course: `data/`

---

##  **Prerequisites**
- Basic Unix command-line knowledge  
- Familiarity with key evolutionary concepts (common ancestry, mutations, selection)  
- Basic experience with DNA/protein sequence data  

---

##  **Setting up the environment**

### Create and activate Conda environment
```bash
conda create -n phylogenetics python==3.8 pandas numpy
conda activate phylogenetics
````

###  Install required packages

```bash
conda install -c bioconda figtree mafft iqtree tracer
conda install -c "bioconda/label/cf201901" beast
```

###  Activate / Deactivate

```bash
conda activate phylogenetics
conda deactivate
```

---

## 🧬 **Practical 1 — Newick (Introduction to Phylogenetics)**

> Represent and visualize a tree in **Newick** format.

1. Write your tree in Newick format and save it as a `.txt` file.
2. Open a terminal and run:

   ```bash
   figtree
   ```
3. Load your file (**File → Open**) and explore its structure.

---

## 🧬 **Practical 2 — Sequence Alignment (MAFFT)**

Run MAFFT on the primate dataset:

```bash
mafft primate-mtDNA_unaligned.fasta > primate-mtDNA_mafft-aligned.fasta
```

 Compare aligned vs unaligned files — what changes?
Then run the same for SARS-CoV-2 sequences — why does it take longer?

---

## 🧬 **Practical 3 — Maximum Likelihood Phylogenetics (IQ-TREE)**

###  Infer a tree with a GTR model:

```bash
iqtree3 -s primate-mtDNA_mafft-aligned.fasta -m GTR --prefix primate-mtDNA_iqtreeGTR
```

###  Find the best substitution model:

```bash
iqtree3 -s primate-mtDNA_mafft-aligned.fasta --prefix primate-mtDNA_iqtreeModelFinder
```

Compare topologies using **FigTree**.

---

## 🧬 **Practical 4 — Bootstrap Analysis**

### Standard bootstrap and TBE:

```bash
iqtree3 -s primate-mtDNA_mafft-aligned.fasta -m GTR -b 100 --tbe --prefix iqtree_tbe
```

### Ultra-Fast Bootstrap:

```bash
iqtree3 -s primate-mtDNA_mafft-aligned.fasta -m GTR -B 1000 --prefix iqtree_ufboot
```

###  aLRT-SH test:

```bash
iqtree3 -s primate-mtDNA_mafft-aligned.fasta -m GTR --alrt 1000 --prefix iqtree_alrt
```

---

## 🧬 **Practical 5 — Bayesian Phylogenetic Inference (BEAST)**

1. Create input `.xml` file in **BEAUti**
   It can be downloaded here: https://beast.community/programs

   ```bash
   beauti
   ```

   * File → Import data
   * Sites → GTR model
   * Trees → Yule process
   * Generate BEAST file

3. Run BEAST on terminal:

   ```bash
   beast primate-mtDNA_BEAST.xml
   ```

4. Analyse in **Tracer** (load `.log` file).

5. Process with **TreeAnnotator**:

   ```bash
   treeannotator
   ```

6. Visualize annotated tree in **FigTree**.

---

## 🧬 **Practical 6 — Phylogeography with BEAST**

###  Use SARS-CoV-2 genomes:

```bash
beauti
```

Include:

* **Dates:** `Tips → Import dates → _dates.txt`
* **Locations:** `Traits → Import traits → _locations.txt`
* **Create partition from trait**
* Generate BEAST file and run as before.

---

##  **Resources**

*  [Example: Phylogenomics from Whole-Genome Resequencing](https://www.science.org/doi/epdf/10.1126/science.1258524)
*  [Estimating MCMC iterations for convergence (Raftery–Lewis Diagnostic)](https://journal.r-project.org/articles/RN-2006-002/RN-2006-002.pdf)

---

*Prepared for the Introduction to Phylogenetics module*
📍 *University of Oxford*
