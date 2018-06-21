## Intel Optimized GATK4 Germline SNPs and Indels Variant Calling Workflow. 

### WORKFLOWS AND JSONS
This repository contains a few different files - each tuned for certain requirements. 

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
The datasets for the WGS workflow can be obtained from: https://console.cloud.google.com/storage/browser/broad-public-datasets/NA12878/unmapped/. 

Contact Broad/Intel for access to the WES data needed for this workflow.

The other reference files and resource files can be downloaded from: 
<table width="0"><caption><strong><em>Datasets Recommended for Setup and Testing this workflow</em></strong></caption>
	<tbody>
		<tr style="height: 22px;">
			<td style="height: 22px;" colspan="2" width="396">Data Type&nbsp;</td>
			<td style="height: 22px;" width="247">Filename&nbsp;</td>
			<td style="height: 22px;" width="278">File Path</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 232px;" rowspan="12" width="198">Reference<br />Genome</td>
			<td style="height: 22px;" width="198">ref_dict&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.dict</td>
			<td style="height: 395.6px;" rowspan="23" width="278"><a href="https://console.cloud.google.com/storage/browser/broad-references/hg38/v0">https://console.cloud.google.com/storage/browser/broad-references/hg38/v0</a></td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_fasta&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_fasta_index&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.fai</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_alt&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.64.alt</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_sa&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.64.sa</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_amb&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.64.amb</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_bwt&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.64.bwt</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_ann&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.64.ann</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">ref_pac&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.fasta.64.pac</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">contamination_sites_ud</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.contam.UD</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">contamination_sites_bed</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.contam.bed</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">contamination_sites_mu</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.contam.mu</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 163.6px;" rowspan="8" width="198">Resource<br />Files</td>
			<td style="height: 22px;" width="198">dbSNP_vcf&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.dbsnp138.vcf</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">dbSNP_vcf_index&nbsp;</td>
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.dbsnp138.vcf.idx</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">known_snps_sites_vcf</td>
			<td style="height: 22px;" width="247">Mills_and_1000G_gold_standard.indels.hg38.vcf.gz</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">known_snps_sites_vcf_index</td>
			<td style="height: 22px;" width="247">Mills_and_1000G_gold_standard.indels.hg38.vcf.gz.tbi</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 44px;" rowspan="2" width="198">known_indels_sites_VCFs</td>
			<td style="height: 22px;" width="247">Mills_and_1000G_gold_standard.indels.hg38.vcf.gz</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.known_indels.vcf.gz</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 44px;" rowspan="2" width="198">known_indels_sites_indices</td>
			<td style="height: 22px;" width="247">Mills_and_1000G_gold_standard.indels.hg38.vcf.gz.tbi</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="247">Homo_sapiens_assembly38.known_indels.vcf.gz.tbi</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 66px;" rowspan="3" width="198">Interval<br />Files</td>
			<td style="height: 22px;" width="198">wgs_calling_interval_list&nbsp;</td>
			<td style="height: 22px;" width="247">wgs_calling_regions.hg38.interval_list <sup>*SEE NOTE BELOW </sup></td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">wgs_coverage_interval_list&nbsp;</td>
			<td style="height: 22px;" width="247">wgs_coverage_regions.hg38.interval_list</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="198">wgs_evaluation_interval_list&nbsp;</td>
			<td style="height: 22px;" width="247">wgs_evaluation_regions.hg38.interval_list</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 66px;" rowspan="3" width="198">Small Test<br />Input<br />Datasets</td>
			<td style="height: 66px;" rowspan="3" width="198">flowcell_unmapped_bams</td>
			<td style="height: 22px;" width="247">H06HDADXX130110.1.ATCACGAT.20k_reads.bam&nbsp;</td>
			<td style="height: 66px;" rowspan="3" width="278">
				<p><a href="https://console.cloud.google.com/storage/browser/genomics-public-data/test-data/dna/wgs/hiseq2500/NA12878/">https://console.cloud.google.com/storage/browser/genomics-public-data/test-data/dna/wgs/hiseq2500/NA12878/</a></p>
			</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="247">H06HDADXX130110.2.ATCACGAT.20k_reads.bam</td>
		</tr>
		<tr style="height: 22px;">
			<td style="height: 22px;" width="247">H06JUADXX130110.1.ATCACGAT.20k_reads.bam</td>
		</tr>
	</tbody>
</table>

**NOTE:** The Exome Interval file ```whole_exome_illumina_coding_v1.Homo_sapiens_assembly38.targets.interval_list``` is hosted at https://console.cloud.google.com/storage/browser/gatk-test-data/intervals/. 

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
