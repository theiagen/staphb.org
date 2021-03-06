---
title: "AMR Detection Using NGS"
date: 2020-02-18T16:20:59Z
draft: false
---
##### Demystifying Webinar Series | February 2020 | AMR Detection Using NGS

For our February 2020 webinar, we discuss how bacterial species identification is conducted using NGS data. This webinar will examine the different algorithms and databases used for AMR detection, with an emphasis on CGE’s ResFinder and NCBI’s AMRFinderPlus. Upon completion of the webinar, attendees will 1) understand the algorithms behind AMR detection using NGS, 2) the difference between gene based and mutational resistance, and 3) the advantages and limitations of these methods compared to traditional phenotypic testing.

Webinar given to the MTN Region on February 26th, 2020

{{< youtube JibS7W2YW8k >}}

[Click here for slides for MTN Region webinar.](https://storage.googleapis.com/staphb-resources/staphb-org-files/training-webinar-slides/AMR_webinar_February_2020_MTN_Region.pdf)

[Click here for the webinar given to the NE Region.](https://www.youtube.com/watch?v=cuugt5F9Ef4)

##### Resources

A great reference that I read in preparation for this webinar was "Sequencing-based methods and resources to study antimicrobial resistance" from Nat Rev Genet. 2019 Jun;20(6):356-370. This reference can be found in the attached [Paperpile library](https://paperpile.com/shared/BbQJT2). The article discusses not only the background on the mechanisms of antimicrobial resistance, but does a thorough job of highlighting many of the resources currentlly availabe. I have adapted two tables from this article and repoduced them below. The first table here lists many of the reference databases used for sequence-based AMR detection:

<div>
<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQZ_h3SMvdq6sqEosa6MZEgIhifl162AYJT0A9Z1yTSQc_qi8n4EcnsQqtOTvX64EIWhTiOwtkOol7t/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false" width="100%" height="600"></iframe>
</div>

This second table highlights many of the sequencing-based tools for identifying genetic determinants of AMR:

<div>
<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTDNEPMs1o9L_vtvEbYWc9v--kqWIZLaSpm4OkygUdqbe4LtdCPnF4PjYrZUzLWTkkqqef5mLGMXT1e/pubhtml?widget=true&amp;headers=false" width="100%" height="600"></iframe>
</div>

One tool discussed during the webinar was [AMRFinderPlus](https://www.ncbi.nlm.nih.gov/pathogens/antimicrobial-resistance/AMRFinder/). This tool is used in the [NCBI Pathogen Detection Pipeline](https://www.ncbi.nlm.nih.gov/pathogens) and the results are displayed in the [NCBI Isolate Browser](https://www.ncbi.nlm.nih.gov/pathogens/isolates/#/search/). AMRFinderPluse uses data from the [Bacterial Antimicrobial Resistance Reference Gene Database](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA313047) to identify AMR determininants. This database contains over 5,000 genes. I have taken this refrence gene databaes and imported it into Tableau so we can have an interactive look at the contents of this database. The Tableau file is posted on Tableau Public and is embedded below:

<div>
<div class='tableauPlaceholder' id='viz1582044648633' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Re&#47;ReferenceGeneCatalog_2020-01-22_1&#47;Table&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='ReferenceGeneCatalog_2020-01-22_1&#47;Table' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Re&#47;ReferenceGeneCatalog_2020-01-22_1&#47;Table&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1582044648633');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
</div>

[ABRicate](https://github.com/tseemann/abricate) was another tool discussed which is common in many public health bioinfromatics workflows. ABRicate was designed to screen assembled contigs from NGS data against multiple databases of antimicribial reistance, virulence, and plasmid genes. ABRicate uses both the ResFinder and AMRFinderPluse databases above (but only nucleotide searches), as well as the following databases:
* [ARG-ANNOT](https://www.ncbi.nlm.nih.gov/pubmed/24145532)
* [CARD](https://card.mcmaster.ca/)
* [EcOH](https://github.com/katholt/srst2/tree/master/data)
* [PlasmidFinder](https://cge.cbs.dtu.dk/services/PlasmidFinder/)
* [VFDB](http://www.mgc.ac.cn/VFs/main.htm)
* [Ecoli_VF](https://github.com/phac-nml/ecoli_vf)

The [Center for Genomic Epidemiology](http://www.genomicepidemiology.org/) is home to serveral tools for genotyping and phenotyping human pathogens, including [ResFinder](https://cge.cbs.dtu.dk/services/ResFinder/).

##### References #####

References used for the preparation of the webinar and cited in the presentation can be found in this [Paperpile library](https://paperpile.com/shared/BbQJT2).
