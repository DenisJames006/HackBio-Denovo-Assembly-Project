# **HackBio-De Novo Assembly Project**

## **Overview**
This project focuses on performing a **de novo genome assembly** using raw sequencing reads.  
The analysis was carried out on **Ubuntu**, following a stepwise approach covering **quality control**, read **trimming**, **assembly**, and **visualization**.  
The goal was to reconstruct the genome from paired-end data while documenting a reproducible workflow.

## **Objectives**
- **Assess** the quality of raw reads  
- **Trim** low-quality bases and adapters  
- **Assemble** the genome using **SPAdes**  
- **Visualize** the assembly graph using **Bandage**

## **Tools Used**
- **FastQC** – quality check of reads  
- **Trimmomatic** – read trimming  
- **SPAdes** – genome assembly  
- **Bandage** – assembly visualization  
- **MultiQC** – summary of QC reports

## **Workflow**

### **Quality Check**
```bash
fastqc SRR13554759_1.fastq.gz SRR13554759_2.fastq.gz -o qc_results/
multiqc qc_results

Trimming
trimmomatic PE SRR13554759_1.fastq.gz SRR13554759_2.fastq.gz \
  trim_results/SRR13554759_1.trim.fastq.gz trim_results/unpaired_1.fastq.gz \
  trim_results/SRR13554759_2.trim.fastq.gz trim_results/unpaired_2.fastq.gz \
  ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 MINLEN:50

Assembly
spades.py -1 trim_results/SRR13554759_1.trim.fastq.gz \
          -2 trim_results/SRR13554759_2.trim.fastq.gz \
          -o assembly_results

Visualization
Bandage GUI
(Open assembly_results/assembly_graph.gfa in Bandage to visualize the contigs and connections.)

Author
Denis O. James
📧 denisjames006@gmail.com
🌐 GitHub: DenisJames006
