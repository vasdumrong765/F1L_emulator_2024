## F1L_emulator_2024
This repo is for tracking the progress on the F1L internship emulator based on Dean Lee LinkedIn articles. The progress will be first commited to the `dev` branch and pushed to the `main` branch when it reaches a certain milestones such as a completion of notes, scripts, etc.

You can find memos on various topics here in `README.md`. This memo is not meant to be a literature review. It is to invoke some thoughts for those with some graduate or professional level of domain knowledge.

## Week 1 - The Key Scientific Question (KSQ)
Reference: https://www.linkedin.com/pulse/week-1-f1l-internship-emulator-ksq-dean-lee-354ke/

The KSQ: Using available scRNA-seq data from cancer cell lines, how would you explore the use of the following FDA-approved antibody therapies in additional cancers?
* Trastuzumab: Targets HER2 and is used in the treatment of HER2-positive breast and gastric cancers.
* Bevacizumab: Targets VEGF and is used for a variety of cancers, including colorectal, lung, glioblastoma, breast, liver, and kidney cancer.

#### General thoughts
Cancer cells are known to exist in heterogenous subpopulations. Using scRNA-seq, we can hope to capture the information about their heterogeneity based on their transcriptional states. 

In the context of drug discovery and development, scRNA-seq can reveal important signatures for identifying which types of cancer cell subpopulation respond to treatment.
* scRNA-seq can argue for some subpopulation of cells defined by a consensus transriptional states. Let's call these intrinsic factors (e.g., presence-or-absence of gene expression, varying level of gene expression)
* Transcriptional states may change based on external factors such as tumor microenvironment, cell-matrix interactions, treatment, metabolic states, etc.
* Therefore, one may simply hypothesize that any two subpopulations from distinct cell types whose transcriptional programs are similar enough may have similar responses to the same external factor.
* How effective is the treatment against various cancer cell types and their subpopulation? <span style="color:#1E90FF"> This can be done by first identifying the cell type and subpopulation from the scRNAseq data, typically by clustering using some known markers (displayed on t-SNE, UMAP). Then, you perform differential gene expression, typically by a linear mixed model. </span>
* How does the level of target expression affect the treatment outcomes (phenotypes, survival, etc)? <span style="color:#1E90FF"> You can perform feature selection to select certain genes to correlate with phenotypes, used as a variable in survival analysis. In addition, you can project/group them into eigengenes with toosl like `WGCNA`. Generally, eigengenes are usually overrepresented co-expression or co-regulated components. </span>


Good experimental designs can help help counteract some "artificial" confounding factors based on experimentation.
* Are the cell lines representative of cancer states? Were they cultured as suspension, monolayer, 2D, 3D-organoids, in-vivo, patient-dervied xenografts, etc? Do we need to account for the donor's genomic landscapes? <span style="color:#1E90FF">There are a lot of things to think about here. An ideal experiment must balance between feasibility, needed resources, and context. It should also have appropriate controls. For example, gene expression in cell lines may not perfectly recapitulate cancer cells in vivo but they could offer a well-controlled experiment. On the other hand, cells harvested directly from a patient tumor may not be representative because it is extremely difficult to ascertain various confounding factors from patient life experience. Two patients may have very different lifestyles, genetic background, etc. </span>
* How were experiments conducted? How many batches are there? Were samples and batches randomized? How many people conducted the experiments? Were hands accounted for in the experimental design? 
* Genomic instability has been shown to be a part of many cancer cell types. Culture passages may change the "baseline" gene expression even for the same cell line.  
* What are the scRNA platform used? Are all ingested data harmonized and accounted for cross-platform data?

#### One way to think about the KSQ:
If we have scRNA-seq data from an experiment where Trastuzumab or Bevacizumab was used to treat a specific cancer cell line (each treatment has its own vehicle control), alongside another dataset of untreated scRNA-seq from different cancer cell lines, can we draw conclusions about the effectiveness of these treatments on the untreated cell lines?