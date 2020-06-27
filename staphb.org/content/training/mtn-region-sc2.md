---
title: "MTN Region SARS-CoV-2 Training"
date: 2020-06-26T16:48:54Z
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

### Agenda (subject to change based on student interests)

##### Week 1

__Session 1 - Linux__   
*   Linux basics
*   Connecting to Basespace
*   Connecting to cloud resources

__Session 2 - Background on Viral Genomics and Coronaviruses__   
*   Viral genomics primer
*   Considerations of bacteria vs viral pathogens
*   Coronavirus, the new flu.

__Session 3 - [Sequencing Methods for SARS-CoV-2](https://github.com/CDCgov/SARS-CoV-2_Sequencing)__
*   Metagenomics, enrichment, amplicon
*   The [ARTIC](https://artic.network/ncov-2019) protocol
*   [ARTIC + Illumina DNA Flex](https://www.protocols.io/file-manager/E2F61524120340C3B7C07A7C9E755CB0)

##### Week 2

__Session 4 - [StaPH-B Toolkit](https://github.com/StaPH-B/staphb_toolkit)__
*   Monroe pipeline
*   pe_assembly
*   cluster_analysis

__Session 5 - UPHL BioNGS__
*   [Cecret SARS-CoV-2 pipeline](https://github.com/UPHL-BioNGS/Cecret)

__Session 6 - Commercial Options__
*   [CLC Genomics Workbench](https://go.qiagen.com/QDI-COVID19)

##### Week 3

__Session 7 - NGS Data Visualization for QC of Results__
*   [CLC Genomics Workbench](https://go.qiagen.com/QDI-COVID19)
*   [Mega-X](https://www.megasoftware.net/)
*   [Integrated Genomics Viewer](http://software.broadinstitute.org/software/igv/) (IGV)

__Session 8 - Data Sharing with GISAID and NCBI__
*   [GISAID](https://www.gisaid.org/) vs [Genbank](https://www.ncbi.nlm.nih.gov/genbank/) vs [SRA](https://www.ncbi.nlm.nih.gov/sra)
*   Walkthrough of each process

__Session 9 - Genomic and Meta Data Visualization in Nextstrain__

*   Intro to [NextStrain](https://nextstrain.org/) for visualization
*   Running on [herokuapp.com](https://auspice-us.herokuapp.com/)
