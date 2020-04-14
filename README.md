## Intel Optimized GATK4 Germline SNPs and Indels Variant Calling Workflow. 

### WORKFLOWS AND JSONS
This repository contains a few different files - each tuned for certain requirements. 

├── Throughput\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WGS Throughput JSON file \
├── Latency\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WGS Latency JSON file \
├── Exome\_2T\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WES Throughput JSON file \
├── Exome\_56T\_PairedSingleSampleWf\_optimized.inputs.json *&rarr;* WES Latency JSON file \
├── PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl *&rarr;* WGS WDL optimized for on-prem \
├── Exome\_PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl *&rarr;* WES WDL optimized for on-prem

Modify the following lines in the WDL files to reflect the paths where datasets reside in your cluster: 
 - [PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/PairedSingleSampleWf_noqc_nocram_optimized.wdl#L1267)
 - [PairedSingleSampleWf\_noqc\_nocram\_withcleanup\_optimized.wdl](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/PairedSingleSampleWf_noqc_nocram_withcleanup_optimized.wdl#L1313)
 - [Exome\_PairedSingleSampleWf\_noqc\_nocram\_optimized.wdl](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/Exome_PairedSingleSampleWf_noqc_nocram_optimized.wdl#L1265)

In the JSON files, modify the paths to the datasets and tools where they reside in your cluster. \
Example: modify [Latency\_PairedSingleSampleWf\_optimized.inputs.json](https://github.com/gatk-workflows/intel-gatk4-germline-snps-indels/blob/master/Thoughput_PairedSingleSampleWf_optimized.inputs.json#L69) for tools directory.

### DATASETS
The datasets used for the WGS workflow turning can be obtained from: https://console.cloud.google.com/storage/browser/broad-public-datasets/NA12878/unmapped/. 

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
For on-prem, the workflow uses non-dockerized tools:

GATK Version can be download from here:  https://github.com/broadinstitute/gatk/releases \
SAMTools can be downloaded from here: http://www.htslib.org/download/ \
Picard tool can be downloaded here: https://broadinstitute.github.io/picard/ 

