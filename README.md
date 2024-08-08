# BIO2_Symposium_Poster_2024
### BACKGROUND

RNA sequencing (RNASeq) allows researchers to analyze gene expression within organisms on a wide scale and can help identify functions of previously unknown genes. The standard analysis workflow typically involves taking sequenced RNA read samples and aligning them to a genome, where the quantification of these read alignments can then be used to evaluate expression levels of certain genes. While the development of RNASeq analysis pipelines have been ongoing for more than a decade, the complexity arising from the numerous computational steps often leads to issues related to reproducibility, time efficiency, and error susceptibility. Furthermore, conducting analysis for non-model organisms introduces additional challenges, including the absence of high-quality genome references and a lack of existing tools for downstream functional analysis. To address problems such as reproducibility and time efficiency, integrated workflow management systems like Nextflow have been created to manage large-scale data files and consolidate individual analysis software components into a cohesive workflow.


Nextflow as a workflow manager adheres to a principle called the dataflow paradigm. Parallelization is built into the Nextflow model so there is no explicit requirement to specify which tasks should be parallelized. Similar to UNIX pipes, output data is streamed into the next process without having to read or write temporary files as input. Another interesting characteristic of this paradigm is that each process will start automatically when it receives streamed input data, heightening the efficiency of the workflow. This in turn also makes scaling the workflow during the development process an easier endeavour. 


Nextflow will automatically store executed tasks in a cache directory. Certain tasks are able to be re-used in future runs and reduce the amount of computation performed. It can also be useful when disruptions occur in the pipeline due to errors, allowing users to run again from the most recent successful step. This is increasingly important when cost and computation quota is involved when operating on the HPC or cloud services.


When dealing with complex pipelines, handling numerous different software packages and maintaining compatibility can easily become a burden. Each package may require updates from time to time, which may also conflict with other existing packages. It has also been shown that different operating systems can influence analysis results. To deal with these issues, Nextflow incorporates containerized environments into its workflow modules. Containers, like Docker and Singularity, allow execution and reproducibility across different operating systems by keeping dependencies self-contained within their own modules. 


Beyond just local environments, it has built-in support for job scheduling softwares like SLURM on HPC and cloud computing services like AWS, GCP, Azure. This supports the need for increased computation and allows researchers to scale their workflow for larger datasets and operations, all the while maintaining reproducibility between different computing infrastructures.


Nextflow also has a large public community called nf-core that has published more than a hundred pipelines that are actively maintained. The pipelines serve as a template for good Nextflow practices but also include a range of configurations, making them adaptable for researchers to customize according to their research needs. 


#### AAFC Problem Background

Deoxynivalenol (DON) is a toxic secondary metabolite produced by Fusarium species that frequently contaminates corn, wheat, oats, barley, and rice, which affects the health of livestock consuming the DON-contaminated feed. 


Some bacterial species have been recently discovered to have the ability to transform DON into a safer alternative. 


Discovery of novel enzymes originating from these bacteria offers potential effective and eco-friendly detoxification solutions.
### METHOD
A workflow will be designed to analyze RNA sequencing data from bacteria expressing detoxification enzymes.
- Data will be preprocessed to allow for prokaryotic compatibility with the nf-core stage
- Extensive annotation will allow for in-depth enrichment and pathway analysis
- Alphafold2 will be used to generate protein structures for differentially expressed genes of interest


Workflow will be implemented in the Nextflow system to maximize efficiency through the use of parallel computing resources


Utilize containers to ensure data is processed in consistent software environments, allowing for the generation of reproducible results. 


### RESULTS
Stages
1.	Pre-processing subworkflow framework completed. Still needs to be tested as part of the larger workflow.
2.	The core RNASeq workflow already existed as part of the nf-core¬ open-source community that regularly maintains commonly used bioinformatics pipelines within Nextflow. 
3.	Annotation subworkflow framework completed. Still needs to be tested as part of the larger workflow.
4.	A R script that utilizes the degust package for differential gene expression analysis has been incorporated into a module.

#### Degust
[EXAMPLE OF DEGUST WEB APPLICATION](https://degust.erc.monash.edu/degust/compare.html?code=example#/)

#### Clusterprofiler
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/GO_biological_process_network.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/GO_molecular_function_upset.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/kegg_ora_barplot.png)



#### Pathway Analysis
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/eay00500.pathview.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/eay02030.pathview.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/eay02040.pathview.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/eay03010.pathview.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/report-resource-cpu.png)
![image](https://github.com/ediconchan/BIO2_Symposium_Poster_2024/blob/main/report-resource-job-duration.png)

![image](https://github.com/user-attachments/assets/c2b04560-5114-4a2c-bbea-44a39e9d74d1)



### Challenges
On top of being familiar with RNASeq analysis and the software tools that are used to perform the tasks, additional time must be spent on learning the Nextflow system. While time consuming, the benefits of efficiency should outweigh the costs in the long term. See an example of how a Nextflow workflow is [organized](https://github.com/nf-core/rnaseq)


One of the many intricacies of AAFC’s HPC is that the compute nodes responsible for heavy workload do not have online internet access. Nextflow’s default settings assume internet access is available, which it uses to download assets like docker containers.
### Next Steps
While half of the subworkflows have already been completed, the remaining subworkflows need to be finished. Many of the subworkflows also need to have some components modularized before it can be initialized.

Like most machine learning models, AlphaFold2 will require GPU utilization to efficiently perform computational tasks. Extra effort will be needed incorporate an AlphaFold2 container into a Nextflow module and determine AAFC’s GPU allocation rules on its HPC.


### Acknowledgements
I would like to thank my advisors, Dion Lepp, Lewis Lukens, and Khurram Nadeem. Special thanks to Dion Lepp and Agriculture and Agri-Food Canada for providing the degust and clusterProfiler visualizations for the poster, as well as conceiving and funding the project. I also would like to thank Cynthia Du for designing the University of Guelph Bioinformatics logo and providing it for use.

### References
1. 	Kukurba KR, Montgomery SB. 2015. RNA sequencing and analysis. Cold Spring Harb Protoc 2015. 
2. 	Simoneau J, Dumontier S, Gosselin R, Scott MS. 2021. Current RNA-seq methodology reporting limits reproducibility. Brief Bioinform https://doi.org/10.1093/bib/bbz124. 
3. 	Lataretu M, Hölzer M. 2020. Rnaflow: An effective and simple rna-seq differential gene expression pipeline using nextflow. Genes (Basel) 11. 
4. 	Chalifa-Caspi V. 2021. RNA-Seq in Nonmodel Organisms Methods in Molecular Biology. 
5. 	Di Tommaso P, Chatzou M, Floden EW, Barja PP, Palumbo E, Notredame C. 2017. Nextflow enables reproducible computational workflows. Nat Biotechnol https://doi.org/10.1038/nbt.3820. 
6. 	Ma T, Zhang A. 2017. Omics Informatics: From Scattered Individual Software Tools to Integrated Workflow Management Systems. IEEE/ACM Trans Comput Biol Bioinform 14. 
