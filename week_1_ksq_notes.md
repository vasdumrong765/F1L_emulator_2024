### Week 1 - The Key Scientific Question (KSQ)
Reference: https://www.linkedin.com/pulse/week-1-f1l-internship-emulator-ksq-dean-lee-354ke/

The KSQ: Using available scRNA-seq data from cancer cell lines, how would you explore the use of the following FDA-approved antibody therapies in additional cancers?
* Trastuzumab: Targets HER2 and is used in the treatment of HER2-positive breast and gastric cancers.
* Bevacizumab: Targets VEGF and is used for a variety of cancers, including colorectal, lung, glioblastoma, breast, liver, and kidney cancer.

#### General thoughts
Cancer cells are known to exist in heterogenous subpopulations. Using scRNA-seq, we can hope to capture the information about their heterogeneity based on their transcriptional states. 

In the context of drug discovery and development, scRNA-seq can reveal important signatures for identifying which types of cancer cell subpopulation of respond to treatment.
* How effective is the treatment to various cancer cell types and their subpopulation?
* How does the level of target expression affect the treatment outcome (phenotype, survival, etc)?
* Are the cell lines representative of cancer states? How are they cultured, monolayer, 2D, 3D organoids, etc?

In terms of experimental designs:
* What are the sources of cancer cell lines? Are they immortalized or patient-derived? Do we need to account for the donors?
* How were experiments conducted? How many batches are there? Were samples and batches randomized? How many people conducted the experiments? Were hands accounted for in the experimental design? 
* Cell lines may be depending how many splits you have performed. This could be a confounding factor.
* What are the platform and flow cells that were used to profile RNA expression?

### KSQ:
If we have scRNA-seq data from an experiment where Trastuzumab or Bevacizumab was used to treat a specific cancer cell line (each treatment has its own vehicle control), alongside another dataset of untreated scRNA-seq from different cancer cell lines, can we draw conclusions about the effectiveness of these treatments on the untreated cell lines?

