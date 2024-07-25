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
* How effective is the treatment against various cancer cell types and their subpopulation?
* How does the level of target expression affect the treatment outcome (phenotype, survival, etc)?
* Are the cell lines representative of cancer states? Were they cultured as suspension, monolayer, 2D, 3D-organoids, in-vivo, patient-dervied xenografts, etc?

Why are these questions important?
* scRNA-seq can argue for some subpopulation of cells defined by a consensus transriptional states. Let's call these intrinsic factors (e.g., presence-or-absence of gene expression, varying level of gene expression)
* Transcriptional states may change based on external factors such as tumor microenvironment, cell-matrix interactions, treatment, metabolic states, etc.
* Therefore, one may simply hypothesize that any two subpopulations from distinct cell types whose transcriptional programs are similar enough may have similar responses to the same external factor.

Good experimental designs can help help counteract some "artificial" confounding factors based on experimentation.
* What are the sources of cancer cell lines? Are they immortalized or patient-derived? Do we need to account for the donor's genomic landscapes?
* How were experiments conducted? How many batches are there? Were samples and batches randomized? How many people conducted the experiments? Were hands accounted for in the experimental design? 
* Genomic instability has been shown to be a part of many cancer cell types. Culture passages may change the "baseline" gene expression even for the same cell line.  
* What are the scRNA platform used? Are all ingested data harmonized and accounted for cross-platform data?

#### One way to think about the KSQ:
If we have scRNA-seq data from an experiment where Trastuzumab or Bevacizumab was used to treat a specific cancer cell line (each treatment has its own vehicle control), alongside another dataset of untreated scRNA-seq from different cancer cell lines, can we draw conclusions about the effectiveness of these treatments on the untreated cell lines?

## Week 2 - Kinker et al
Reference: https://www.linkedin.com/pulse/week-2-f1l-internship-emulator-paper-dean-lee-3crce/?trackingId=D%2Fv8Iq3CREOcoeJT2FnV8A%3D%3D
This week, we are assigned to read a paper Pan-cancer single-cell RNA-seq identifies recurring programs of cellular heterogeneity by Kinker et al. This gives us a bit more context for the KSQ.

#### My brief summary




#### Some questions asked by Dean
* How did the authors handle the potential caveat of co-culturing cell lines before profiling by scRNA-seq? Why do you think that caveat was or was not adequately addressed?
* The authors identified discrete subpopulations of cells within a subset of individual cell lines (Fig. 2A-B). * * What might be the reason why some cell lines have these discrete subpopulations while others do not?
* What are Recurrent Heterogeneous Programs (RHPs) and how were they defined?
* How do the identified RHPs relate to in vivo programs of heterogeneity in tumors, and what evidence supports this relationship?
* Where can you download the scRNA-seq data as shown in Figure 1B?