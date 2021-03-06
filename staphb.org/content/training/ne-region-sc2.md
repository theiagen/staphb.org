---
title: "Northeast Region SARS-CoV-2 Training"
date: 2020-09-01T16:31:01Z
draft: false
---

### Training Prerequisites
In order for this training to be effective for all students participating, each student should perform the following before the first class:
1. Confirm that they can connect to their VM.
2. Watch a 75 minute video on the linux operating system.
3. Watch a short video on tmux, a linux application that allows for multiple terminals.

###### *Connect to your VM*

In the slack channel will be listed your VM IP address, along with a ssh key file. This information will be posted on Monday, June 29th. In order to connect to this VM, you will need to download the terminal program MobaXterm. MobaXterm can be downloaded from [https://mobaxterm.mobatek.net/download-home-edition.html](https://mobaxterm.mobatek.net/download-home-edition.html). IMPORTANT: Please download the “Portable edition”, not the “Installer edition”. The “Portable edition” will allow you to run the application without installing it, thus no admin rights needed. Once you have downloaded MobaXterm and have access to your IP address and ssh key, watch the youtube video on [How to Connect to Your VM](https://youtu.be/CWEA86aRkg8). I will also post the username and passphrase in slack.

###### *Linux video*

The video link is [https://www.youtube.com/watch?v=oxuRxtrO2Ag](https://www.youtube.com/watch?v=oxuRxtrO2Ag). This video will give you a basic understanding of navigating around the bash terminal in linux. It is well worth the 75 minutes before the course, working within your own VM.

###### *Tmux video*

Many of the processes we will be running will require long processing times that could be interrupted by network connection issues. To avoid this, we will perform the exercises in the class using the tmux application. This [tmux tutorial video](https://youtu.be/BHhA_ZKjyxo) will guide you through the process of using tmux.

Some additional resources that you will find useful when starting out are:

*   [Linux command reference](https://fossbytes.com/a-z-list-linux-command-line-reference/)
*   [tmux cheat sheet](https://tmuxcheatsheet.com/)

### Agenda Overview


*__Session 1 - Background on Viral Genomics and Coronaviruses__*  - Tuesday, Sept 8th, 12 PM and 3 PM EDT   
*__Session 2 - Sequencing Methods for SARS-CoV-2__* - Wednesday, Sept 9th, 11 AM and 2 PM EDT   
*__Session 3 - Linux__* - Friday, Sept 11th, 11 AM and 2 PM EDT   
*__Session 4 - StaPH-B Toolkit and Cecret__* - Monday Sept 14th, 11 AM and 2 PM EDT   
*__Session 5 - Terra.bio__* - Wednesday Sept 16th, 11 AM and 2 PM EDT  
*__Session 6 - Terra.bio__* - Friday Sept 18th, 11 AM and 2 PM EDT   
*__Session 7 - NGS Data Visualization for QC of Results__* - Monday Sept 21st, 11 AM and 2 PM EDT  
*__Session 8 - Data Sharing with GISAID and NCBI SRA__* - Wednesday Sept 23rd, 11 AM and 2 PM EDT  
*__Session 9 - Data Sharing with NCBI Genbank__* - Friday Sept 25th, 11 AM and 2 PM EDT

Office hours will be offered each week on Tuesday from 2 PM to 4 PM EDT and on Thursday from 12 PM to 2 PM EDT, and by request.


*__Session 1 - Background on Viral Genomics and Coronaviruses__*

__[Recording for Session 1 - 12 PM EDT](https://youtu.be/smCB4QRRw3M)__

* Register for a [GISAID](https://www.gisaid.org/registration/register/) account
* Viral genomics primer
* Considerations of bacteria vs viral pathogens
* Coronavirus, the new flu.
* [Papers on Coronaviruses](https://paperpile.com/shared/dU0ZnG)

*__Session 2 - [Sequencing Methods for SARS-CoV-2](https://github.com/CDCgov/SARS-CoV-2_Sequencing)__*

__[Recording for Session 2 - 11 AM EDT](https://youtu.be/QawI3oXmKMo)__

__[Recording for Session 2 - 2 PM EDT](https://youtu.be/ffrTOpWNb-s)__

* Metagenomics, enrichment, amplicon
* The [ARTIC](https://artic.network/ncov-2019) protocol
* [ARTIC + Illumina DNA Flex - Part 1](https://www.protocols.io/view/sars-cov-2-sequencing-on-illumina-miseq-using-arti-bfefjjbn) at protocols.io.
* [ARTIC + Illumina DNA Flex - Part 2](https://www.protocols.io/view/sars-cov-2-sequencing-on-illumina-miseq-using-arti-bffyjjpw) at protocols.io.

*__Session 3 - Linux__*

__[Recording for Session 3 - 11 AM EDT](https://youtu.be/4LSiFbaug50)__

* Linux basics
* Working in Tmux
  * [Tmux Cheat Sheet](https://tmuxcheatsheet.com/)
  * [Tmux Video](https://www.youtube.com/watch?v=oxuRxtrO2Ag)
* Connecting to Basespace
  * [Basespace CLI](https://developer.basespace.illumina.com/docs/content/documentation/cli/cli-overview)
* Connecting to cloud resources
  * [gsutil](https://cloud.google.com/storage/docs/gsutil)
* Transferring data to your VM for the class



__Commands used in this session__
```
***bash commands***

dir                           #lists out a directory
ls                            #also lists out a directory
ls -la                        #lists out a directroy with details
ll                            #alias for ls -la
cd <directory>                #change directory
cd                            #will bring you to your home directory
mkdir <dir>                   #make directory
rmdir <dir>                   #remove directory if it is empty
rm -rf <dir>                  #remove directory if it is full
gzip <name.fastq>             #zip a read file

***tmux***

tmux ls                       #list open tmux sessions
tmux new -s <name>            #start a tmux session called <name>
tmux a -t <name>              #attach to tmux session called <name>
tmux kill-session -t <name>   #kill tmux session called <name>
Ctrl-b ,                      #rename current window
Ctrl-b c                      #create new window
Ctrl-b n                      #go to next window
tmux info                     #help

***basespace cli***

bs auth                                   #authenticate to Basespace
bs list projects                          #list projects in basespace
bs download project -n <name> -o <dir>    #download project files to <dir>

***gsutils***

gsutil ls                                 #list storage buckets
gsutil cp <source> <destination>          #cp data from storage bucket

***sra-toolkit*** - might need to "sudo apt-get install sra-toolkit"

prefetch <sra_id>
fastq-dump --split-files --gzip <sra_id>
```

*__Session 4 - StaPH-B Toolkit - Monroe__*

__[Recording for Session 4 - 11 AM EDT](https://youtu.be/wUPaF9id3oo)__

__[Recording for Session 4 - 2 PM EDT](https://youtu.be/bC9sZccWwBc)__

* Monroe pipeline
* pe_assembly
* cluster_analysis

[Documentation on Monroe](https://staph-b.github.io/staphb_toolkit/workflow_docs/monroe/)

Some commands to make today's session easier

```
***Configure Cecret***

tmux new -s session4	#starts a new tmux session if you don't have one already

cd	#moves you to your home directory

rm -rf Cecret/	#removes old Cecret installation

git clone https://github.com/UPHL-BioNGS/Cecret.git	#clones new Cecret

cd <workspace>	#move to workspace directory

***let's copy over some files

gsutil ls
gsutil ls gs://mtn-class-bucket/
gsutil -m cp gs://mtn-class-bucket/cecret.tar .
gsutil -m cp gs://mtn-class-bucket/monroe.tar .
gsutil -m cp gs://mtn-class-bucket/Cecret.nf .

***move the Cecret.nf folder to the Cecret location***

mv Cecret.nf ~/Cecret/   

***unwrap tar files***

tar -xvf cecret.tar
tar -xvf monroe.tar

mkdir cecret_live
mkdir monroe_live

cd monroe
cp 20-07-01_* ../monroe_live/
cp -r reads/ ../monroe_live/   #you can use optional SRA method at the end to copy into a reads folder
cd ..
cd monroe_live

staphb-wf monroe pe_assembly --primers V3 --output pe_assembly_1 --config 20-07-01_pe_assembly.config reads

***Before we launch cluster_analysis, we need to go into the monroe_live/pe_assembly_1/assemblies/ directory
***and remove/modify the failed assemblies.  This will be discussed in the video.  Failure to do so will
***create incorrect results for the cluster_analysis step.

***example data screening***
mv SRR12542859_consensus.fasta SRR12542859_consensus.fasta.fail
mv SRR12542860_consensus.fasta SRR12542860_consensus.fasta.fail
mv SRR12542861_consensus.fasta SRR12542861_consensus.fasta.fail
mv SRR12542863_consensus.fasta SRR12542863_consensus.fasta.fail
mv SRR12542869_consensus.fasta SRR12542869_consensus.fasta.fail
***end data screening***

staphb-wf monroe cluster_analysis --output cluster_analysis_1 --config 20-07-01_cluster_analysis.config pe_assembly_1/assemblies/

***If the data wasn't already copied over from the storage bucket, they
***following would download the data needed from SRA

***retrieving data from SRA***

prefetch SRR12542859 SRR12542860 SRR12542861 SRR12542862 SRR12542863 SRR12542864 SRR12542865 SRR12542866 SRR12542867 SRR12542868 SRR12542869 SRR12542870

fastq-dump --split-files --gzip SRR12542859 SRR12542860 SRR12542861 SRR12542862 SRR12542863 SRR12542864 SRR12542865 SRR12542866 SRR12542867 SRR12542868 SRR12542869 SRR12542870
```

*__Session 5 - Terra.bio Part 1__*

__[Recording for Session 5 - 11 AM EDT](https://youtu.be/FH2JdQvgmUc)__

__[Recording for Session 5 - 2 PM EDT](https://youtu.be/fQ-V4PYIBEw)__

* [Terra.bio](https://app.terra.bio/) is a broweser interface to running [WDL](https://openwdl.org/) workflows on the [Google Cloud Platform](https://cloud.google.com/).


*__Session 6 - Terra.bio Part 2__*

__[Recording for Session 6 - 11 AM EDT](https://youtu.be/JZ_PsKKqW70)__

Instrutions for working with WDL files on the command line.

```
# install miniwdl (maybe about 1 minute)
pip install miniwdl

# test miniwdl (also about 1 minute)
miniwdl run_self_test

# describe refbased assembly parameters
miniwdl run https://raw.githubusercontent.com/broadinstitute/viral-pipelines/master/pipes/WDL/workflows/assemble_refbased.wdl

# go get some input files
gsutil -m cp gs://pathogen-public-dbs/refs/ARTIC_V3_nCoV-2019_NC_045512_primers3.bed .
gsutil -m cp gs://pathogen-public-dbs/refs/ref-sarscov2-NC_045512.2.fasta .

# fetch a bam from SRA (this takes about 1 minute or less)
miniwdl run https://raw.githubusercontent.com/broadinstitute/viral-pipelines/master/pipes/WDL/workflows/fetch_sra_to_bam.wdl Fetch_SRA_to_BAM.SRA_ID=SRR12542859

# assemble that sample (this takes 7 mins)
miniwdl run https://raw.githubusercontent.com/broadinstitute/viral-pipelines/master/pipes/WDL/workflows/assemble_refbased.wdl reads_unmapped_bams=/home/mtn-region/20200916_162418_fetch_sra_to_bam/out/reads_ubam/SRR12542859.bam reference_fasta=ref-sarscov2-NC_045512.2.fasta trim_coords_bed=ARTIC_V3_nCoV-2019_NC_045512_primers3.bed

# Optional: querying json files with jq (instead of searching the above by eye)
sudo apt-get install jq
jq -r '.["assemble_refbased.align_to_ref_merged_reads_aligned"]' _LAST/outputs.json
# returns 18914
jq -r '.["assemble_refbased.assembly_length_unambiguous"]' _LAST/outputs.json
# returns 14031
jq -r '.["assemble_refbased.assembly_mean_coverage"]' _LAST/outputs.json
# returns 57.09861886767214
jq -r '.["assemble_refbased.dist_to_ref_snps"]' _LAST/outputs.json
# returns 12
jq -r '.["assemble_refbased.dist_to_ref_indels"]' _LAST/outputs.json
# returns 0
# all of the above values are identical to what Terra reports!


# serially run it on all 12 samples (total runtime is about 2 hours on a 1-core VM)
for srr in SRR12542859 SRR12542860 SRR12542861 SRR12542862 SRR12542863 SRR12542864 SRR12542865 SRR12542866 SRR12542867 SRR12542868 SRR12542869 SRR12542870; do
   BAMFILE=$(miniwdl run https://raw.githubusercontent.com/broadinstitute/viral-pipelines/master/pipes/WDL/workflows/fetch_sra_to_bam.wdl Fetch_SRA_to_BAM.SRA_ID=$srr | jq -r '.outputs["fetch_sra_to_bam.reads_ubam"]')
   miniwdl run https://raw.githubusercontent.com/broadinstitute/viral-pipelines/master/pipes/WDL/workflows/assemble_refbased.wdl reads_unmapped_bams=$BAMFILE reference_fasta=ref-sarscov2-NC_045512.2.fasta trim_coords_bed=ARTIC_V3_nCoV-2019_NC_045512_primers3.bed
done

## other notes about parallelization
# Times listed above are for a 1-core VM.
# With more CPU available, certain steps (e.g. minimap2) will auto parallelize and complete faster, but the overall speed will not increase linearly.
# Also, with more CPU available, miniwdl will parallelize certain concurrent steps for a single assembly
# If you have a big (30+ CPU) machine, you can replace the bash for loop with a GNU parallel invocation in order to parallelize across samples
# miniwdl can submit its work across a Docker Swarm, if you set that up on your back end, but ultimately, will not have complex ways of parallelizing work across large amounts of resources. You should be switching to Cromwell (or Terra) when you get to that scale.

```

*__Session 7 - QC and Data Sharing: GISAID__*

__[Recording for Session 7 - 11 AM EDT](https://youtu.be/j6HbxxEGjRs)__

__[Recording for Session 7 - 2 PM EDT](https://youtu.be/BH8NfGgqgBQ)__

* [GISAID](https://www.gisaid.org/)

>The GISAID Initiative promotes the rapid sharing of data from all influenza viruses and the coronavirus causing COVID-19. This includes genetic sequence and related clinical and epidemiological data associated with human viruses, and geographical as well as species-specific data associated with avian and other animal viruses, to help researchers understand how viruses evolve and spread during epidemics and pandemics.
>
>GISAID does so by overcoming disincentive hurdles and restrictions, which discourage or prevented sharing of virological data prior to formal publication.
>
>The Initiative ensures that open access to data in GISAID is provided free-of-charge to all individuals that agreed to identify themselves and agreed to uphold the GISAID sharing mechanism governed through its Database Access Agreement.
>
>All bonafide users with GISAID access credentials agreed to the basic premise of upholding a scientific etiquette, by acknowledging the Originating laboratories providing the specimens, and the Submitting laboratories generating sequence and other metadata, ensuring fair exploitation of results derived from the data, and that all users agree that no restrictions shall be attached to data submitted to GISAID, to promote collaboration among researchers on the basis of open sharing of data and respect for all rights and interests.

*__Session 8 - QC and Data Sharing: NCBI SRA__*

__[Recording for Session 8 - 11 AM EDT](https://youtu.be/Vjfp_mqSo8Q)__

__[Recording for Session 8 - 2 PM EDT](https://youtu.be/Heca0kXzd0E)__

*__Session 9 - QC and Data Sharing: NCBI Genbank__*

__[Recording for Session 9 - 11 AM EDT](https://youtu.be/CZkTZnFZx5s)__

__[Recording for Session 9 - 2 PM EDT](https://youtu.be/fQea5ELWocE)__
