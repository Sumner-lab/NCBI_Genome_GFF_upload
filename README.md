# NCBI eukaryotic genome and annotation upload

This page is to simplify the upload of data to NCBI. 

Uploading the genome (in fasta) and annotation in GFF (or GTF).

**Prerequisites:**
1. 


Steps. 

1. Download `table2asn` executable from NCBI : https://ftp.ncbi.nlm.nih.gov/asn1-converters/by_program/table2asn. For me this didn't work with the mac one, so I used the linux one and did it through myriad.
Which includes:
2. Filling in the submission form: https://submit.ncbi.nlm.nih.gov/genbank/template/submission/
3. Getting your genome fasta file in the correct format: https://www.ncbi.nlm.nih.gov/genbank/table2asn/#fsa
4. Creating a table format from your GFF or GTF file : https://www.ncbi.nlm.nih.gov/genbank/table2asn/#tbl
5. Run the script: `table2asn -M n -J -c w -euk -t template.sbt  -gaps-min 10 -l paired-ends -j "[organism=Polybia occidentalis] -i fasta_file -f gff_file -o output_file.sqn -Z`
where all before template.sbt is the same. "template.sbt" should be in your currect directory (you got this from step 2).  Gaps default 10 is fine. -l is for evidence of linkage between reads, so for mate pair experiment disicgn, we use paired-ends option. The -j option needs the correct Genus and species name (in our case Polybia). -i is for our genome fasta file, -f is for our gff3 file. The output is stored in name specified after the -o flag. -Z is required for working directory (I think).


B1. Start following these instructions: https://www.ncbi.nlm.nih.gov/genbank/eukaryotic_genome_submission/
