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

### Agenda Overview

*__Session 1 - Linux__* - Monday July 6th, 12 PM and 2 PM MDT   
*__Session 2 - Background on Viral Genomics and Coronaviruses__*  - Tuesday, July 7th, 12 PM and 2 PM MDT   
*__Session 3 - Sequencing Methods for SARS-CoV-2__* - Wednesday July 8th, 12 PM and 2 PM MDT   
*__Session 4 - StaPH-B Toolkit__* - Monday July 13th, 12 PM and 2 PM MDT   
*__Session 5 - UPHL BioNGS__* - Tuesday July 14th, 12 PM and 2 PM MDT   
*__Session 6 - Commercial Options__* - Wednesday July 15th, 12 PM and 2 PM MDT   
*__Session 7 - NGS Data Visualization for QC of Results__* - Monday July 20th, 12 PM and 2 PM MDT   
*__Session 8 - Data Sharing with GISAID and NCBI__* - Tuesday July 21st, 12 PM and 2 PM MDT   
*__Session 9 - Data Visualization in Nextstrain__* - Wednesday July 22nd, 12 PM and 2 PM MDT

Office hours will be offered each week on Thursday from 2 PM to 4 PM MDT, on Friday from 9 AM to 11 AM MDT, and by request.

### Expanded Agenda (will contain links, videos, code, as course progresses)  
##### Week 1

*__Session 1 - Linux__*

__[Recording for Session 1 - 12:00 PM MDT](https://youtu.be/R_SR7A8o6d8)__

__[Recording for Session 1 - 3:00 PM MDT](https://youtu.be/XbU_UmFSkf8)__

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

*__Session 2 - Background on Viral Genomics and Coronaviruses__*

__[Recording for Session 2 - 12 PM MDT](https://youtu.be/_UoIDdXmI2A)__

__[Recording for Session 2 - 3 PM MDT](https://youtu.be/YqAFqWWMDUM)__

__[Session 2 Slides](https://storage.googleapis.com/staphb-resources/staphb-org-files/training-webinar-slides/MTN-2020-Session2-CoronavirusGenomics.pdf)__

* Viral genomics primer
* Considerations of bacteria vs viral pathogens
* Coronavirus, the new flu.
* [Papers on Coronaviruses](https://paperpile.com/shared/dU0ZnG)

__REMINDER 7/7__ --> register for a [GISAID account](https://www.gisaid.org/registration/register/)

*__Session 3 - [Sequencing Methods for SARS-CoV-2](https://github.com/CDCgov/SARS-CoV-2_Sequencing)__*

__[Recording for Session 3 - 12 PM MDT](https://youtu.be/vwqvZcyLD_E)__

__[Recording for Session 3 - 3 PM MDT](https://youtu.be/cXHPWbMGR8g)__

* Metagenomics, enrichment, amplicon
* The [ARTIC](https://artic.network/ncov-2019) protocol
* [ARTIC + Illumina DNA Flex](https://www.protocols.io/file-manager/E2F61524120340C3B7C07A7C9E755CB0) at protocols.io.

##### Week 2

*__Session 4 - [StaPH-B Toolkit](https://github.com/StaPH-B/staphb_toolkit)__*

__[Recording for Session 4 - 12 PM MDT](https://youtu.be/h6l7tdNWXU4)__ (Watch the 3 PM instead)

__[Recording for Session 4 - 3 PM MDT](https://youtu.be/nrXgNtbghCs)__ (This is the better recording)

* Monroe pipeline
* pe_assembly
* cluster_analysis

[Documentation on Monroe](https://staph-b.github.io/staphb_toolkit/workflow_docs/monroe/)

Some commands to make today's session easier
```
tmux new -s session4

mkdir session4-1
cd session4-1
gsutil ls
gsutil ls gs://mtn-reads/
gsutil -m cp -r gs://mtn-reads/session4/* .
tar -xf reads.tar
mkdir reads
mv *.gz reads
rm reads.tar
staphb-wf monroe
staphb-wf monroe pe_assembly
staphb-wf monroe pe_assembly --primers V3 --output pe_assembly_1 --config 20-07-11_pe_assembly.config reads

staphb-wf monroe cluster_analysis
staphb-wf monroe cluster_analysis --output cluster_analysis_1 --config 20-07-11_cluster_analysis.config pe_assembly_1/assemblies/


```

*__Session 5 - UPHL BioNGS__*
* [Cecret SARS-CoV-2 pipeline](https://github.com/UPHL-BioNGS/Cecret)

__[Recording for Session 5 - 12 PM MDT](https://youtu.be/jWEyBGTq6W8)__

__[Recording for Session 5 - 3 PM MDT](https://youtu.be/Z-QL8s1BBK4)__

Data files

[session5_files.tar](https://storage.googleapis.com/staphb-resources/session5_files.tar)

[session5_files_2.tar](https://storage.googleapis.com/staphb-resources/session5_files_2.tar)

Some commands to make today's exercises easier
```
#see if you have a tmux session open
tmux ls

#create a new tmux session called session5
tmux new -s session5

#create new window in your tmux session
<create new window in tmux with Ctrl-b, c>

#copy over session files
gsutil -m cp -r gs://mtn-reads/session5/* .

#extract the session files
tar -xf session5_files_2.tar

#change dir into cecret_session5
cd cecret_session5

#check out covid_samples.txt
column -t covid_samples.txt | less -S

#copy new Cecret.nf to your Cecret folder
cp Cecret.nf ~/Cecret/

#check thatt Cecret.nf was updated
ll ~/Cecret

#launch Cecret - will take about 50 minutes with 10 specimens
~/nextflow run ~/Cecret/Cecret.nf -c cecret.docker.nextflow.google.config

#go up one directory to session5
cd ..

#unpack bakeshow data
tar -xf session5_files.tar

#move into bakeshow directory
cd cecret_bakeshow

#check out run_results.txt
column -t run_results.txt | less -S


```

*__Session 6 - Cecret and Monroe Continued__*

*__UPDATE:__* Most likely we will continue looking at Monroe and Cecret results

__[Recording for Session 6 - 12 PM MDT](https://youtu.be/RJecZ8vA1S8)__

__[Recording for Session 6 - 3 PM MDT](https://youtu.be/fwwtr2vYgaE)__

Not covered:
* [CLC Genomics Workbench](https://go.qiagen.com/QDI-COVID19)

##### Week 3

*__Session 7 - Data Sharing with GISAID and NCBI__*

__[Recording for Session 7 - 12 PM MDT](https://youtu.be/GgoQjLxYouA)__

__[Recording for Session 7 - 3 PM MDT](https://youtu.be/comk7G9ddvg)__

Topics update:
* Data sharing with [GISAID](https://www.gisaid.org/)

Topics not covered, future webinars:
* [CLC Genomics Workbench](https://go.qiagen.com/QDI-COVID19)
* [Mega-X](https://www.megasoftware.net/)
* [Integrated Genomics Viewer](http://software.broadinstitute.org/software/igv/) (IGV)

*__Session 8 - Data Sharing with GISAID and NCBI__*

__[Recording for Session 8 - 12 PM MDT](https://youtu.be/5S2lFWIloso)__

__[Recording for Session 8 - 3 PM MDT](https://youtu.be/qyomji9WpxY)__

Topics update:
* Data sharing with [SRA](https://www.ncbi.nlm.nih.gov/sra)

*__Session 9 - More Data Sharing__*

__[Recording for Session 9 - 12 PM MDT](https://youtu.be/lTejITeZgt0)__

__[Recording for Session 9 - 3 PM  MDT](https://youtu.be/tlUXLaP2au4)__

Topics update:
* Data sharing with [Genbank](https://www.ncbi.nlm.nih.gov/genbank/)

Topics not covered below, will have future webinars.
* Intro to [NextStrain](https://nextstrain.org/) for visualization
* Running on [herokuapp.com](https://auspice-us.herokuapp.com/)
* [Tutorial](https://nextstrain.github.io/ncov/)
* [NextStrain Clades](https://clades.nextstrain.org/)
