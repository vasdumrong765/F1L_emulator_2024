## F1L_emulator_2024: Exploring scRNA-seq expression heterogeneity among cancer cell lines
This repo is for tracking the progress on the F1L internship emulator based on Fiugre One Lab Dean Lee's LinkedIn articles. The progress will be first commited to the `dev` branch and pushed to the `main` branch when it reaches a certain milestone such as a completion of notes, scripts, etc.

You can find memos on various topics here in `README.md`. This memo is not meant to be a literature review. It is to invoke some thoughts and perspectives to accompany the topics discussed here.

**References to Dean Lee's articles**

- [X] [Week 1](https://www.linkedin.com/pulse/week-1-f1l-internship-emulator-ksq-dean-lee-354ke/)
- [ ] [Week 2](https://www.linkedin.com/pulse/week-2-f1l-internship-emulator-paper-dean-lee-3crce/)
- [ ] [Week 3](https://www.linkedin.com/pulse/week-3-f1l-internship-emulator-data-dean-lee-h83qe/)
- [ ] [Week 4](https://www.linkedin.com/pulse/week-4-f1l-internship-emulator-biology-dean-lee-ja4me/)
- [ ] [Week 5](https://www.linkedin.com/pulse/week-5-f1l-internship-emulator-slides-dean-lee-qqufe/)

## Week 1 - The Key Scientific Question (KSQ)

The KSQ: Using available scRNA-seq data from cancer cell lines, how would you explore the use of the following FDA-approved antibody therapies in additional cancers?
* Trastuzumab: Targets HER2 and is used in the treatment of HER2-positive breast and gastric cancers.
* Bevacizumab: Targets VEGF and is used for a variety of cancers, including colorectal, lung, glioblastoma, breast, liver, and kidney cancer.

#### <code style="color : LightSkyBlue">Quick info on these mAb's targets</code>
* HER2 is a member of the human epidermal growth factor receptor, a plasma-membrane-bound receptor tyrosine kinase (Gene name: *ERBB2*, Uniprot_ID: P04626). Activation of HER2, usually via homo/heterodimerization with EGFR, promotes cell proliferation. Overexpression or gene amplification of HER2 occurs in ~14% of breast cancer ([NIH Cancer Stat Facts](https://seer.cancer.gov/statfacts/html/breast-subtypes.html))

* VEGF stands for Vascular endothelial growth factor. VEGF binds to a tyrosine kinase VEGF receptors which is known to promote angiogenesis. Angiogenesis is a crucial step for tumorigenesis.

#### General thoughts
Cancer cells are known to exist in heterogenous subpopulations. Using scRNA-seq, we can hope to capture the information about their heterogeneity based on their transcriptional states. 

In the context of drug discovery and development, scRNA-seq can reveal important signatures for identifying which types of cancer cell subpopulation respond to treatment.
* scRNA-seq can argue for some subpopulation of cells defined by a consensus transriptional states. Let's call these intrinsic factors (e.g., presence-or-absence of gene expression, varying level of gene expression)
* Transcriptional states may change based on external factors such as tumor microenvironment, cell-matrix interactions, treatment, metabolic states, etc.
* Therefore, one may simply hypothesize that any two subpopulations from distinct cell types whose transcriptional programs are similar enough may have similar responses to the same external factor.
* How effective is the treatment against various cancer cell types and their subpopulation? <span style="color:#1E90FF"> This can be done by first identifying the cell type and subpopulation from the scRNAseq data, typically by clustering using some known markers (displayed on t-SNE, UMAP). Then, you perform differential gene expression, typically by a linear mixed model. </span>
* How does the level of target expression affect the treatment outcomes (phenotypes, survival, etc)? <span style="color:#1E90FF"> You can perform feature selection to select certain genes to correlate with phenotypes, used as a variable in survival analysis. In addition, you can project/group them into eigengenes with tools like `WGCNA`. Generally, eigengenes are usually overrepresented by co-expression or co-regulated components. </span>


Good experimental designs can help help counteract some "artificial" confounding factors based on experimentation.
* Are the cell lines representative of cancer states? Were they cultured as suspension, monolayer, 2D, 3D-organoids, in-vivo, patient-dervied xenografts, etc? Do we need to account for the donor's genomic landscapes? <span style="color:#1E90FF">There are a lot of things to think about here. An ideal experiment must balance between feasibility, needed resources, and context. It should also have appropriate controls. For example, gene expression in cell lines may not perfectly recapitulate cancer cells in vivo but they could offer a well-controlled experiment. On the other hand, cells harvested directly from a patient tumor may not be representative because it is extremely difficult to ascertain various confounding factors from patient life experience. Two patients may have very different lifestyles, genetic background, etc. </span>
* How were experiments conducted? How many batches are there? Were samples and batches randomized? How many people conducted the experiments? Were hands accounted for in the experimental design? 
* Genomic instability has been shown to be a part of many cancer cell types. Culture passages may change the "baseline" gene expression even for the same cell line.  
* What are the scRNA platform used? Are all ingested data harmonized and accounted for cross-platform data?

#### One way to think about the KSQ:
If we have scRNA-seq data from an experiment where Trastuzumab or Bevacizumab was used to treat a specific cancer cell line (each treatment has its own vehicle control), alongside another dataset of untreated scRNA-seq from different cancer cell lines, can we draw conclusions about the effectiveness of these treatments on the untreated cell lines?

## Week 2 - Kinker et al
This week, we are assigned to read a paper Pan-cancer single-cell RNA-seq identifies recurring programs of cellular heterogeneity by Kinker et al. This gives us a bit more context for the KSQ. 

#### My brief summary
The authors hypothesized that there could some intrinsic properties shared among cancer cells that could explain intratumor heterogenity in the absence of tumor microenvironments. To tackle this question, they conducted single-cell RNAseq experiments profiling 9 pools of cancer cell lines. Each of the eight pools is a mixture of 24-27 cell lines with similar proliferation rates from the Cancer Cell Line Encyclopedia (CCLE) collection. One additional customed pool includes head and neck squamous cell carcinoma (HNSCC) cell lines. They found that there exists recurrent heterogeneous programs (RHPs) of gene expression, concensus expression patternned shared by many types of cancer. The authors then highlighted several functional annotations of the RHPs. Following the overall description of RHPs, the authors chose to focus on Epithelial Senescence (EpiSen) program which are preferentially observed in G0 cells such as HNSCC cell lines. They isolated and experimented on high and low-EpiSen HNSCC cells and demonstrated these two subpopulation elicits distinct sensitivities to pharmacological treatment.

#### Some questions asked by Dean
* How did the authors handle the potential caveat of co-culturing cell lines before profiling by scRNA-seq? Why do you think that caveat was or was not adequately addressed?
* The authors identified discrete subpopulations of cells within a subset of individual cell lines (Fig. 2A-B). What might be the reason why some cell lines have these discrete subpopulations while others do not?
* What are Recurrent Heterogeneous Programs (RHPs) and how were they defined?
* How do the identified RHPs relate to in vivo programs of heterogeneity in tumors, and what evidence supports this relationship?
* Where can you download the scRNA-seq data as shown in Figure 1B?
* * I downloaded `Metadata.txt` and `UMIcount_data.txt` from https://singlecell.broadinstitute.org/single_cell/study/SCP542/pan-cancer-cell-line-heterogeneity#study-download

## Week 3

Setting up a new env with conda based on Mark Sanborn's youtube video:
```
conda create -n sc2024 python=3.9
conda activate sc2024
pip install notebook scanpy doubletdetection
```