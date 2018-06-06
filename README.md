## Intel Optimized GATK4 Germline SNPs and Indels Variant Calling Workflow. 

### WORKFLOWS AND JSONS
This repository contains a few different files - each tuned for certain requirements. 

PairedSingleSampleWf_noqc_nocram_optimized.wdl
PairedSingleSampleWf_noqc_nocram_withcleanup_optimized.wdl
Exome_PairedSingleSampleWf_noqc_nocram_optimized.wdl
56T_PairedSingleSampleWf_optimized.inputs.json
2T_PairedSingleSampleWf_optimized.inputs.json
Exome_56T_PairedSingleSampleWf_optimized.inputs.json
Exome_2T_PairedSingleSampleWf_optimized.inputs.json

├── 2T\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WGS Throughput JSON file \
├── 56T\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WGS Latency JSON file \
├── Exome\_2T\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WES Throughput JSON file \
├── Exome\_56T\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WES Latency JSON file \
├── PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl *&rarr;* WGS WDL optimized for on-prem \
├── PairedSingleSampleWf\_noqc\_nocram\_withcleanup\_optimized.wdl *&rarr;* WGS WDL optimized for on-prem with cleanup of output results (for throughput analysis) \
├── Exome\_PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl *&rarr;* WES WDL optimized for on-prem

Modify the following lines in the WDL files to reflect the paths where datasets reside in your cluster: 
 - [PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/PairedSingleSampleWf_noqc_nocram_optimized.wdl#L1267)
 - [PairedSingleSampleWf\_noqc\_nocram\_withcleanup\_optimized.wdl](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/PairedSingleSampleWf_noqc_nocram_withcleanup_optimized.wdl#L1313)
 - [Exome\_PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/Exome_PairedSingleSampleWf_noqc_nocram_optimized.wdl#L1265)

In the JSON files, modify the paths to the datasets and tools where they reside in your cluster. \
Example: modify [56T\_PairedSingleSampleWf\_optimized.inputs.json](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/56T_PairedSingleSampleWf_optimized.inputs.json#L69) for tools directory.

#### FPGA CHANGES
Assuming the environemnt has been setup to offload the pairhmm kernel of HaplotypeCaller to FPGA - the below changes must be enabled in the WDL/JSON files (based on the comments) to make use of the FPGA. 

a. In the WDL files, for task Haplotype Caller runtime section, uncomment the line:
require\_fpga: "yes"

b. In the JSON file, change the "PairedEndSingleSampleWorkflow.gatk\_gkl\_pairhmm\_implementation" to “EXPERIMENTAL\_FPGA\_LOGLESS\_CACHING” from “AVX\_LOGLESS\_CACHING”.

### DATASETS
Contact Intel/Broad for access to the WGS/WES data needed for this workflow.

### TOOLS
For on-prem, the workflow uses non-dockerized tools. To keep up with the exact 
versions released by Broad for their best practices workflow, we download the 
tools from the docker image to our shared file system. 

Run the command: 
```
docker run -v /path/to/shared_filesystem:/path/to/shared_filesystem -it broadinstitute/genomes-in-the-cloud:2.3.1-1504795437 /bin/bash
```

This command will pull the docker image (if it is not already there locally), 
and put you within the container from where you can copy the tools needed for 
the workflow. 

```
root@54754360159e:/usr/gitc# cp -r /usr/local/bin/samtools bwa picard.jar /path/to/shared_filesystem
root@54754360159e:/usr/gitc# exit
```

Similarly, copy the gatk4 folder from docker image: broadinstitute/gatk:4.0.0.0 
