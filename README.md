# ccle_processing

__have a look at [DepMap](https://www.depmap.org)__

![](https://github.com/broadinstitute/ccle_processing/blob/master/documentation/depmap-logo.png)

What you need to process the Quarterly DepMap-Omics releases from Terra.

[Here](https://docs.google.com/presentation/d/1i0HI31dBejTYmzI9Cp6Ij7--t6eSR2r9vcC22TxSnNI/edit#slide=id.g525fd14bef_0_116) is a presentation of the pipeline.

We are using a set of key tools to process the sequencing output:
- __star__:
  - [https://www.ncbi.nlm.nih.gov/pubmed/23104886](https://www.ncbi.nlm.nih.gov/pubmed/23104886)
  - [https://github.com/alexdobin/STAR/blob/master/doc/STARmanual.pdf](https://github.com/alexdobin/STAR/blob/master/doc/STARmanual.pdf)
- __rsem__: 
  - [https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-12-323](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-12-323)
- __star fusion__: 
  - [https://github.com/STAR-Fusion/STAR-Fusion/wiki](https://github.com/STAR-Fusion/STAR-Fusion/wiki)
  - [http://biorxiv.org/content/early/2017/03/24/120295](http://biorxiv.org/content/early/2017/03/24/120295)
- __mutect__: 
  - [https://software.broadinstitute.org/cancer/cga/mutect](https://software.broadinstitute.org/cancer/cga/mutect)
  - [https://youtu.be/rN-cLrb5aGs](https://youtu.be/rN-cLrb5aGs)
  - [https://gatk.broadinstitute.org/hc/en-us/articles/360036490432-Mutect2](https://gatk.broadinstitute.org/hc/en-us/articles/360036490432-Mutect2)
  - [https://www.nature.com/articles/nbt.2514](https://www.nature.com/articles/nbt.2514)
- __gatk cnv__:
  - [https://software.broadinstitute.org/gatk/documentation/article?id=11682](https://software.broadinstitute.org/gatk/documentation/article?id=11682)
- __strelka__:
  - [https://www.nature.com/articles/s41592-018-0051-x](https://www.nature.com/articles/s41592-018-0051-x)
  - [https://github.com/Illumina/strelka](https://github.com/Illumina/strelka)

## Installation 

If you are not familiar with these notions, we will first recommend you get more knowledge into each:

- [python](https://www.learnpython.org/)
- [R](https://www.codecademy.com/learn/learn-r)
- [jupyter](https://jupyter.org/index.html)
- [WDL](https://software.broadinstitute.org/wdl/documentation/)
- [gcp](https://cloud.google.com/sdk/docs/quickstart-macos)
- [docker](https://docs.docker.com/get-started/)
- [Terra](https://software.broadinstitute.org/firecloud/documentation/)
- [dalmatian](https://github.com/broadinstitute/dalmatian)
- [Terra and gcp](https://docs.google.com/document/d/1zTtaN-Px64f8JvgydZNdBbzBpFWyZzEpshSNxQh43Oc/edit#heading=h.dz5wh0l4bu9g)


### install it 

`git clone http://github.com/BroadInstitute/ccle_processing.git && cd ccle_processing`
### :warning: this repository needs other repos

Some important data and code from the [JKBio Library](https://www.github.com/jkobject/JKBio).

`pip install JKBio`
### :warning: you would need the approriate R packages and python packages

1. You will need to install jupyter notetbooks and google cloud sdk
  - install [Google Cloud SDK](https://cloud.google.com/sdk/docs/downloads-interactive).
  - authenticate my SDK account by running `gcloud auth application-default login` in the terminal.

2. and GSVA for ssGSEA in R `R` run `R -e 'if(!requireNamespace("BiocManager", quietly = TRUE)){install.packages("BiocManager")};BiocManager::install(c("GSEABase", "erccdashboard", "GSVA", "DESeq2"));`

3. For Python use the requirements.txt file `pip install -r requirements.txt` 

## For Broad People

> Mind that you need to know about the tools listed above
- Ask dbgap access to your supervisor

### Getting Terra Access

1. You will need to request access to the following terra workspaces:
  - https://app.terra.bio/#workspaces/broad-firecloud-ccle/DepMap_Mutation_Calling_CGA_pipeline
  - https://app.terra.bio/#workspaces/broad-firecloud-ccle/DepMap_hg38_RNAseq
  - https://app.terra.bio/#workspaces/broad-firecloud-ccle/DepMap_WES_CN_hg38
The current owners of these workspaces should give you access.
2. For the mutation pipeline you will also need to request DBGap access (required for TCGA workflows): https://docs.google.com/document/d/1hwsjUypqUpse7IeMyBLKEXmdlXUzfBa4e4p9teCVtaw/edit?usp=sharing
3. Ask Sarah Young for access to required billing projects (e.g. broad-firecloud-ccle)
4. Get access to the following Terra groups:
  - DEPMAP_CCLE_DATA
  - DEPMAP-PIPELINES
  - CCLE2-DATA
  - CCLE-PIPELINE
5. If you need to get access to the depmap data:
  - __Exome__ [IBM](https://firecloud.terra.bio/#workspaces/broad-genomics-delivery/Getz_IBM_CellLines_Exomes/data)
  - __Exome__ [Broad](https://firecloud.terra.bio/#workspaces/broad-firecloud-ccle/CCLE_DepMap_WES)
  - __Exome__ [Broad](https://firecloud.terra.bio/#workspaces/broad-genomics-delivery/CCLE_DepMap_WES)
  - __rna__ [IBM](https://firecloud.terra.bio/#workspaces/broad-genomics-delivery/Getz_IBM_CellLines_RNASeqData/data)
  - __rna__ [Broad](https://firecloud.terra.bio/#workspaces/broad-firecloud-ccle/CCLE_DepMap_RNAseq)
  - __rna__ [Broad](https://firecloud.terra.bio/#workspaces/broad-genomics-delivery/CCLE_DepMap_RNAseq)
6. Request access to the data bucket `gs://ccle_bams/`
7. You will need also access to the billing project `broad-firecloud-ccle`


*more information on the firecloud workspaces and what they might contain is available on this [document](https://www.github.com/broadinstitute/ccle_processing/firecloud_documentation.html)

### additional logins:
- in order to run the imports [gsheets](https://pypi.org/project/gsheets/) and [taigapy](https://pypi.org/project/taigapy/), you will need to create a [taiga](https://cds.team/taiga) account and link your broad google account to access the cell line sheets.


### boot up

- You first need to go to [taiga](https://cds.team/taiga/dataset) and create some new datasets for the virtual release

We are instantiating all the parameters needed for this pipeline to run

#### Adding new data

We are looking for new samples in a range of workspaces.

They are quite messy and might contains duplicates, contain broken file paths...

- We are thus looking at the bam files one by one and comparing them with our own bams. 
- We remove broken files, duplicates and add new version of a cell line's bam if we find some.

#### Check that we have all the cell lines we expect for this release

This involves comparing to the list in the Google sheet "Cell Line Profiling Status."

_As the list cannot be parsed, we are not comparing it for now_


## For External Users:

> Mind that you need to know about the tools listed above

### Creating your Terra Workspaces:

1. Your first need a terra account with correct billing setup
2. use the different *_pipeline folders, they contain everything to setup the workspace correctly
  1. use the WDL scripts available in:
    - https://dockstore.org/my-workflows/github.com/broadinstitute/depmap_omics/WGS_pipeline
    - https://dockstore.org/my-workflows/github.com/broadinstitute/depmap_omics/WGS_aggregate
    - https://dockstore.org/my-workflows/github.com/broadinstitute/depmap_omics/RNA_pipeline
    - https://dockstore.org/my-workflows/github.com/broadinstitute/depmap_omics/RNA_aggregate
  2. export them to your workspace
  3. add he required workspace data listed in all_configs.json (under GENERAL.workspace.attributes)
  4. setup the right inputs and outpus for your workflows using the inputs_[WORKFLOW_NAME].json and outputs_[WORKFLOW_NAME].json files
3. load your samples so that their bam and bam index google storage filepath get listed in the right data column to WGS_pipeline and RNA pipeline.
4. create a sample set with the set of samples you want to analyse.

Once this is done, you can run your jupyter notebook server and open the `CCLE_\*` jupyter files corresponding to our RNA pipeline and WGS pipeline (older versions for WES (CN and mutations are available in a previous commit labelled 20Q4)).

Remark:
  1. you cannot run the `_...()` functions listed in the notebooks.
  2. you will need to use the `postProcesssing()` functions for post processing instead of the CCLE ones.
  3. you will need to change some of the variables in the prod config file.
  4. you wont be able to run the function conditional on the CCLE boolean. You can however reimplement them to create your own pipeline.

The notebook architectures are as follows:

1. UpLoading and preprocessing
2. Running the Terra Pipelines
3. DownLoading and postProcessing the samples
4. QC, grouping and uploading to the DepMap portal

## Running the pipeline

### 1. UpLoading and preprocessing 

The first phase really is about getting samples generated at the broad and located into different places. Looking for duplicates and finding/adding the metadata we will need in order to have coherent and complete sample information. __This is not something that you would need to run. you can skip directly to part2__.

**Remarks:** 
- in the initialization you might want to remove any import related to `taiga` and `gsheet` to not cause any errors.
- feel free to reuse `createDatasetWithNewCellLines`, `GetNewCellLinesFromWorkspaces` or any other function for your own needs.

### 2. Running Terra Pipelines

Before running this part, you need to make sure that your dalmatian `workspacemanager` object is initialized with the right workspace you created and that the functions take as input you workflow names. You also need to make sure that you created your sample set with all your samples and that you initialized the `sampleset` string with its name
You can then run this part for the pipeline to run on your samples. It should take around a day.

**Remarks:**
- for the copy number pipeline we have parametrized both an XX version and an XY version, we recommend using the XY version as it covers the entire genome
- for the mutation pipeline we are working on Tumor-Normal pairs which explain some of the back and forth between the two workspace data table. (workflows works as well with or without matched normals.)
- for the expression pipeline, we have an additional set of workflows to call mutations from RNAseq, this might not be relevant to your need.

### 3. DownLoading and postProcessing (often called **2.2-4 on local** in the notebooks)

This step will do a set of tasks:
- clean some of the workspace for large useless files.
- retrieve from the workspace interesting QC results.
- copy realigned bam files to some bucket.
- download the results.
- remove all duplicate samples from our downloaded file (keeping only thee latest version of each samples).
- saving the current pipeline configuration.

_You would only be interested here at minima in the result downloading_
 
...and post processing tasks.

> Unfortunately for now the postProcessing tasks are not all made to be easily run outside of the CCLE pipeline. Most of them are in R and are run with the Rpy2 tool.

So amongst these functions, some of them might be of a lesser interest to an external user. The most important ones for each pipelines are:

- `processSegments`
- `interpolateGapsInSegmented`
- `extendEndsOfSegments`
- `generateEntrezGenes`
- `generateGeneLevelMatrixFromSegments`

- `readMutations`
- `createSNPs`
- `filterAllelicFraction`
- `filterMinCoverage` *you would need to rewrite this function as it now runs on DepMap columns. In one line it requires that the total coverage of that site (aggregated across methods) > 8 and that there are at least 4 alternate alleles for each mutations*
- `maf_add_variant_annotations`
- `mutation_maf_to_binary_matrix`

- `readTranscripts`
- `readCounts`
- `readTPM`
- `readFusions`
- `filterFusions`
- the `step 2.2.5` where we remove samples with more then 39k transcripts with 0 readcounts.
- `prepare_depmap_\*\_for_taiga`

**Remarks:**
- in the RNAseq pipeline we have an additional sub-pipeline at the end of the notebook to process the fusion calls from starFusion
- to get the exact same results as in CCLE, be sure to run `genecn = genecn.apply(lambda x: np.log2(1+x))` to the genecn dataframe in the CNV pipeline (present at the end of the validation steps).
- we do not yet have integrated our germline calling in the mutation pipeline but you can still find the haplotypeCaller\|DeepVariant workflows and their parameters


### 4. QC, grouping and uploading to the portal

These tasks should not be very interesting for any outside user as they revolve around manual checks of the data, comparison to previous releases, etc.

We are also preparing the data to be released to different groups, removing the samples per access category: Blacklist\|Internal\|DepMapConsortium\|Public.

We are then uploading the data to a server called taiga where it will be used in the depmap portal


## File structure

There is for now 3 computation pipeline for depmap omics:
- Expression
- Mutations
- Copy number

Each:
- is contained in an jupyter notebook file
- gets data from Terra workspace's gcp buckets managed by Broad's Genomics Platform + DevOps, 
- updates the sample TSVs on Terra with path to the files, 
- compute the results for each samples by running workflows, 
- download the results, post process them with additional local functions and QC them.
- uploads them to taiga.

__data/__ Contains important information used for processing

__src__ Contains the location of function files

__\*\_pipeline__ Contains some of the pipeline's workflows' wdl files and script files used by these workflows 

__ccle_tasks__ Contains a notebook for each of the different additional processing that the CCLE team has to perform

__legacy__ Contains the previous R markdown files that were used as templates for the previous pipeline's post-processing

__readmes__ Contains some of the depmap readmes 

__temp__ Contains the temp file that can get removed after processing (should be empty)

__documentation__ Contains some additional files for documenting the pipelines


## Data


### PONS

for CN pons are made from a set of ~400 normals from the GTEx project as they were sequenced in the same fashion as CCLE samples with the same set of baits. you can see the ID of the samples in `data/samples_for_pons.csv`.
We have created pons for each bait set and using XY only.
We have used workflow from the pipeline:
`gatk/CNV_Somatic_Panel_Workflow`


### targets

The data we are presenting comes from different WES targets/baits/intervals.

We are currently using Illumina ICE intervals and Agilent intervals. you can find their related PON files and interval files as parameters in our workspace files in `data/xQx.json`


## CCLE Pipelines inner workings:

![schema](https://github.com/broadinstitute/ccle_processing/blob/master/documentation/architecture_diagram.png)

To run the CCLE pipeline we follow the installation process above and then boot up a GCP instance to run the notebooks from it.

You can find more documentation about the range of workspaces that have been created: [here](https://github.com/broadinstitute/ccle_processing/blob/master/documentation/firecloud_documentation.md)

Note: Slide 7 of the [CCLE pipelines and datasets presentation](https://docs.google.com/presentation/d/1i0HI31dBejTYmzI9Cp6Ij7--t6eSR2r9vcC22TxSnNI/edit#slide=id.g525fd14bef_0_240) provides another good view of what the pipeline is doing.

![](https://github.com/broadinstitute/ccle_processing/blob/master/documentation/slide7.png)

_What is explained below comes from the notebook's documentations and might be better understood by reading them directly on the notebooks_


### run Terra pipeline

We are using Dalmatian to send request to Terra, 

#### Copy Numbers

We are running a set of 5 functions/workflows To generate the copy number dataset in the following order:

1. [**BamToUnmappedRGBams_MC**](https://portal.firecloud.org/?return=terra#methods/vdauwera/BamToUnmappedRGBams/4)
2. [**Generate_uBAM_File_List**](https://portal.firecloud.org/?return=terra#methods/gkugener/ArrayOfFilesToTxt/1)
3. [**Realign_WES_GATK4**](https://portal.firecloud.org/?return=terra#methods/gatk/PreProcessingForVariantDiscovery_GATK4/7): This pipeline realigns bams to hg38 using BWA-MEM, marks duplicates, and applies Base Quality Score Recalibration ([BQSR](https://gatk.broadinstitute.org/hc/en-us/articles/360035890531-Base-Quality-Score-Recalibration-BQSR-)) to the final bam files.
4. [**CNV_sample_XX**](https://portal.firecloud.org/?return=terra#methods/gatk/CNV_Somatic_Pair_Workflow/9/wdl): This pipeline recieves read counts, which are the output of previous step, and determines the copy number segments and assigns them the deletion/amplification/neutral status. The pipeline requires an input PoN, which currently is defaulted on [hg38 ICE WES capture kit](gs://ccle_default_params/pons/hg38_ice_pon_XX.pon.hdf5). The following tools are run in the order shown:
   1. [*gatk DenoiseReadCounts*](https://gatk.broadinstitute.org/hc/en-us/articles/360037593691-DenoiseReadCounts): Denoises read counts to produce denoised copy ratios
   2. [*gatk ModelSegments*](https://gatk.broadinstitute.org/hc/en-us/articles/360036350172-ModelSegments): Models segmented copy ratios from denoised read counts and segmented minor-allele fractions from allelic counts
   3. [*gatk CallCopyRatioSegments*](https://gatk.broadinstitute.org/hc/en-us/articles/360036730311-CallCopyRatioSegments): Calls copy-ratio segments as amplified, deleted, or copy-number neutral
   4. *PlotDenoisedCopyRatios*
   5. *PlotModeledSegments*
5. [**Aggregate_CN_seg_files**](https://portal.firecloud.org/?return=terra#methods/gkugener/Aggregate_CN_seg_files/2)

This output file for download will be saved under the sample set under the combined_seg_file attribute.

There are several other tasks in this workspace. In brief:

*   **CNV_Somatic_Panel_Workflow_Agilent_XX** gatk/CNV_Somatic_Panel_WorkflowSnapshot ID: 11. This task was used in this workspace to generate the Sanger PON. In the Sanger dataset, there is a set of 40 normal cell lines samples (cell lines derived from matched normal tissue). We can use these to generate a PON to normalize to rather than using the Agilent PON we use for the other CCLE cell lines. This leads to less noisy results. HOWEVER, results using the PON from this workflow should not use the X chromosome, as the sanger normals are not exclusively female or male (it is likely a mix).
*   **SANGER_PON_CNV_sample_XX** gatk/CNV_Somatic_Pair_WorkflowSnapshot ID: 9. Same as the CNV_sample_XX_gatk, except that is uses the Sanger based PON. Should be used only for the Sanger cell lines.
*   **Sanger_PON_Aggregate_CN_seg_files** gkugener/Aggregate_CN_seg_filesSnapshot ID: 2. Aggregates the segment files for the samples that were run using the Sanger PON based CNV workflow. 


#### Mutation

We are running a set of 6 functions/workflows To generate the mutation dataset:

*   For new samples in DepMap, run the ICE version of this task. CCLE2 samples used Agilent targets, so this pipeline should be used instead. The pipelines are identical in terms of their outputs, but the proper targets, baits, and pseudo normal should be used based on how the samples were sequenced.

*    **ICE_CGA_Production_Analysis_Pipeline_Cell_Lines_copy** (cclf/CGA_Production_Analysis_Pipeline_Cell_Lines_debuggingSnapshot ID: 22) OR
*    **AGILENT_CGA_Production_Analysis_Pipeline_Cell_Lines** (cclf/CGA_Production_Analysis_Pipeline_Cell_Lines_debuggingSnapshot ID: 22)

1. [**CGA_WES_CCLE_Characterization_Pipeline_v0.1_Jul2019**](https://portal.firecloud.org/?return=terra#methods/getzlab/CGA_WES_CCLE_Characterization_Pipeline_v0.1_Jul2019/1): Run the CGA pipeline for mutation calling.
2. [**common_variant_filter**](https://portal.firecloud.org/?return=terra#methods/breardon/common_variant_filter/18): Apply common variant filters as described [here](https://github.com/vanallenlab/common_variant_filter).
3. [**filterMAF_on_CGA_pipeline**](https://portal.firecloud.org/?return=terra#methods/gkugener/filterMAF_on_CGA_pipeline/9): Applies several filters to the maf file including minimum allele frequency, Exac, COSMIC, and TCGA hotspot filters, retainin only coding regions, minimum coverage, and alternative reads filter, etc. Detailed process can be found in *gs://ccle_default_params/scripts/filterMAF.R*. The whitelisted mutations can be found here: *gs://ccle_default_params/references/all_hotspots_for_Mahmoud_083116_ExAC_filt.tsv*. Currently no mutations are blacklisted in this step.
4. [**aggregateMAFs_selectFields**](https://portal.firecloud.org/?return=terra#methods/gkugener/aggregateMAFs_selectFields_copy/1): Reads selected fields from maf files and aggregates them. Currently these fields are: *Hugo_Symbol, Entrez_Gene_Id, Center, NCBI_Build, Chromosome, Start_position, End_position, Strand, Variant_Classification, Variant_Type, Reference_Allele, Tumor_Seq_Allele1, Tumor_Seq_Allele2, dbSNP_RS, dbSNP_Val_Status, Genome_Change, Annotation_Transcript, Tumor_Sample_Barcode, cDNA_Change, Codon_Change, Protein_Change, t_alt_count, t_ref_count, tumor_f, isDeleterious, isTCGAhotspot, TCGAhsCnt, isCOSMIChotspot, COSMIChsCnt, i_ExAC_AF, PASS*. The script can be found in *gs://ccle_default_params/scripts/scripts_aggregate_selectedFields_MAF.R*

*NOTE:* Some further filtering occurs afterwards within the Jupyter Notebook, including hard filtering of allele frequency and coverage (see the section on local data analysis).

This outputs to be downloaded will be saved in the sample set that was run. The output we use for the release is:


*   **passedCGA_filteredMAF_aggregated** 

There are several other tasks in this workspace. In brief:

*   **CGA_Production_Analysis_Pipeline_Cell_Lines** (lelagina/CGA_Production_Analysis_Pipeline_Cell_LinesSnapshot ID: 12). This task is the same as the ICE and AGILENT prefixed version above, except that it relied on pulling the baits and targets to use from the metadata stored for the samples. Having AGILENT and ICE versions specified made the uploading and running process easier.
*   **SANGER_CGA_Production_Analysis_Pipeline_Cell_Lines** (cclf/CGA_Production_Analysis_Pipeline_Cell_Lines_debuggingSnapshot ID: 22). This task was trying to run the CGA pipeline on the Sanger WES data, using a Sanger pseudo normal. In its current implementation, this task fails to complete for the samples.
*   **UNFILTERED_aggregateMAFs_selectFields** (ccle_mg/aggregateMAFs_selectFieldsSnapshot ID: 1). Aggregates the MAF outputted by the CGA cell line pipeline prior to the common variant filter and germline filtering tasks. This can give us insight to which mutations are getting filtered out when. We may want to potentially include this MAF in the release so people can see why certain mutations of interest may be getting filtered out.
*   WES_DM_Mutation_Calling_Pipeline_(standard |expensive) (gkugener/WES_DM_Mutation_Calling_PipelineSnapshot ID: 2). This was a previous mutation calling pipeline implemented for CCLE. We do not use this pipeline any more as the CGA pipeline looks better.
*   aggregate_filterMAF_CGA (CCLE/aggregate_filterMAF_CGASnapshot ID: 1). An aggregation MAF task that we used in the past. We do not use this task anymore.
*   calculate_mutational_burden (breardon/calculate_mutational_burdenSnapshot ID: 21). This task can be used to calculate the mutational rate of the samples. We do not make use of this data in the release although it could be of interest.
*   summarizeWigFile (breardon/summarizeWigFileSnapshot ID: 5). CCLF ran this task (might be necessary for the mutational burden task). For our workflow, we do not run it.


#### RNAseq

We are running a set of 6 functions/workflows To generate the expression/fusion dataset:

We use the [GTEx pipeline](https://github.com/broadinstitute/gtex-pipeline/blob/v9/TOPMed_RNAseq_pipeline.md) to generate the expression dataset, run the following tasks on all samples that you need, in this order:

   1. [**samtofastq_v1-0_BETA_cfg**](https://portal.firecloud.org/?return=terra#methods/broadinstitute_gtex/samtofastq_v1-0_BETA/6): Converts bam files to fastq.
   2. [**star_v1-0_BETA_cfg**](https://portal.firecloud.org/?return=terra#methods/broadinstitute_gtex/star_v1-0_BETA/7): uses STAR to align fastq files to [hg38 reference genome](https://console.cloud.google.com/storage/browser/fc-secure-639c94ba-2b0d-4960-92fc-9cd50046a968/references/gtex?authuser=2).
   3. [**rsem_v1-0_BETA_cfg**](https://portal.firecloud.org/?return=terra#methods/broadinstitute_gtex/rsem_v1-0_BETA/5): run RSEM to quantify transcript abundances.
   4. [**rsem_aggregate_results_v1-0_BETA_cfg**](https://portal.firecloud.org/?return=terra#methods/broadinstitute_gtex/rsem_aggregate_results_v1-0_BETA/3)

The outputs to be downloaded will be saved under the sample set that you ran. The outputs we use for the release are:

*   rsem_genes_expected_count
*   rsem_genes_tpm
*   rsem_transcripts_tpm

****Make sure that you delete the intermediate files. These files are quite large so cost a lot to store. To delete, you can either write a task that deletes them or use gsutil rm*****

We use [STAR-Fusion](https://github.com/STAR-Fusion/STAR-Fusion/wiki) to generate gene fusion calls by running the following workflows:

1. [**hg38_STAR_fusion**](https://portal.firecloud.org/?return=terra#methods/gkugener/STAR_fusion/14)
2. [**Aggregate_Fusion_Calls**](https://portal.firecloud.org/?return=terra#methods/gkugener/Aggregate_files_set/2)

The outputs to be downloaded will be saved under the sample set you ran. The outputs we use for the release are: 

*   fusions_star

This task uses the same samtofastq_v1-0_BETA_cfg task as in the expression pipeline, although in the current implementation, this task will be run twice. It might be worth combing the expression/fusion calling into a single workflow. This task also contains a flag that lets you specify if you want to delete the intermediates (fastqs). 

There are several other tasks in this workspace. In brief:

*   Tasks prefixed with **EXPENSIVE** or **CHEAP** are identical to their non-prefixed version, except that they specify different memory, disk space, etc. parameters. These versions can be used when samples fail the normal version of the task due to memory errors.
*   The following tasks are part of the GTEx pipeline but we do not use them (we use RSEM exclusively): markduplicates_v1-0_BETA_cfg (broadinstitute_gtex/markduplicates_v1-0_BETA Snapshot ID: 2), rnaseqc2_v1-0_BETA_cfg (broadinstitute_gtex/rnaseqc2_v1-0_BETA Snapshot ID: 2)
*   **ExonUsage_hg38_fixed** (gkugener/ExonUsage_fixed Snapshot ID: 1): this task calculates exon usage ratios. The non-fixed version contains a bug in the script that is not able to handle chromosome values prefixed with ‘chr’. The ‘fixed’ version resolves this issue.
*   **AggregateExonUsageRObj_hg38** (ccle_mg/AggregateExonUsageRObj Snapshot ID: 2): combines the exon usage ratios into a matrices that are saved in an R object.

### On local

__We then save the workflow configurations used__
__,delete unmapped bams generated during the process__
__and move the hg38 aligned bams to our own datastorage bucket__
__We download and reprocess removing the appended version and keeping only the newest versions__

### post Procesing

The post processing happens in R using guillaume's and Allie's functions, in brief:

#### CN

- processSegments
- filterForCCLE
- interpolateGapsInSegmented
- extendEndsOfSegments
- reprioritizeData

dataPrioritization is done as explained in fig. 5 of https://www.biorxiv.org/content/10.1101/720243v1.full.pdf

![](documentation/prioritization.png)

##### creating gene copy number

- generateEntrezGenes
- generateGeneLevelMatrixFromSegments

##### Validation step

Once the files are saved, we load them back in python and do some validations, in brief:

- mean,max,var...
- to previous version: same mean,max,var...
- checkAmountOfSegments: flag any samples with a very high number of segments
- checkGeneChangeAccrossAll: flag any genes which stay at a similar value across all samples

#### Mutation

Here, rather than rerunning the entire analysis, because we know we are adding only WES samples, we can download the previous release's MAF, add the samples, update any annotations, and perform any global filters at the end.

First we need to do an additional step of filtering on coverage and number 

- readMutations
- createSNPs
- addToMainMutation
- filterAllelicFraction
- filterMinCoverage
- mergeAnnotations
- addAnnotation
- maf_add_variant_annotations
- mutation_maf_to_binary_matrix (x3)

##### validation

__Compare to previous release (broad only)__

I would run some checks here comparing the results to the previous releases MAF. Namely:

- Count the total number of mutations per cell line, split by type (SNP, INS, DEL)
- Count the total number of mutations observed by position (group by chromosome, start position, end position and count the number of mutations)
- Look at specific differences between the two MAFs (join on DepMap_ID, Chromosome, Start position, End position, Variant_Type). I would do this for WES only

__check if important mutations are present or not__

#### RNA

Here we get all data and remove the duplicates directly with the function `removeDuplicates`

We then run:

- readTranscripts
- readCounts
- readTPM
- renameFunction

- Allie's gene renaming / filtering and log transform

##### Validation

- mean,max,var...
- to previous version: same mean,max,var...
- we QC on the amount of genes with 0 counts for each samples

##### Generate filtered fusion table

Release: `r release`

We want to apply filters to the fusion table to reduce the number of artifacts in the dataset. Specifically, we filter the following:

* Remove fusions involving mitochondrial chromosomes, or HLA genes, or immunoglobulin genes
* Remove red herring fusions (from STAR-Fusion annotations column)
* Remove recurrent in CCLE (>= 25 samples)
* Remove fusion with (SpliceType=" INCL_NON_REF_SPLICE" and LargeAnchorSupport="No" and FFPM < 0.1)
* Remove fusions with FFPM < 0.05 (STAR-Fusion suggests using 0.1, but looking at the translocation data, this looks like it might be too aggressive)

With the functions:
- readFusions
- filterFusions
- prepare_depmap_fusion_data_for_taiga

### Upload to taiga (Broad only)

- We load the blacklisted/embargoed sample ids
- We log2 transform and create a file for each release (and one containing everything)
- We upload the files using taigapy in a corresponding taiga dataset with the corresponding description and also upload it to its virtual dataset


# Previous PiPelines

https://docs.google.com/document/d/1O6ZWGAnG6CO_smtaA-fqQmSqV64TF1GHFbj-ZeIqD6U/edit?usp=sharing

https://docs.google.com/document/d/1qHnqO3QGdubu8IvB9zI13Z48EbKwDTpgRg0TnT6GULw/edit?usp=sharing

https://docs.google.com/document/d/189K81MOIYlvg4ePvtHPBSfMen1sgYm7G1EncG5N8tFk/edit?usp=sharing

https://docs.google.com/document/d/19MvCIpRID12vfIlc5i2XmJB8yT2jJ2xwNM_PI1HRC0A/edit?usp=sharing

@[jkobject](https://www.jkobject.com)
@gkugener
@gmiller
@__[BroadInsitute](https://www.broadinstitute.org)

For any questions/issues, send us an email at ccle-help@broadinstitute.org or write down an issue on the github repo
