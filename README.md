# NCBI eukaryotic genome and annotation upload

This page is to simplify the upload of data to NCBI. 

Uploading the genome (in fasta) and annotation in GFF (or GTF).

**Prerequisites:**
a. Cisco, make sure you have access to the RDS, if this is where the raw data are stored.

Steps. 
1a. Create a Bioproject for your Genome and annotation: https://submit.ncbi.nlm.nih.gov/subs/bioproject/
- Make sure to say publish at latest year possible. You need to click on year and choose 2026 or beyond, further possible.
- For these steps, you need to have information about the species, isolate and grant info.
- At biosample page, skip this and continue, we add the bisample after.

1b. Then create a Biosample for the genome indivudal or pool that constituted the materiel the genome was made with. https://submit.ncbi.nlm.nih.gov/subs/biosample
- For this we need information about the exact sample that was used to make the genome. E.g was it a haploid male, etc.

2a. Download `table2asn` executable from NCBI : https://ftp.ncbi.nlm.nih.gov/asn1-converters/by_program/table2asn. For me this didn't work with the mac one, so I used the linux one and did it through myriad.
Which includes:

2b. Filling in the NCBI Genbank submission form: https://submit.ncbi.nlm.nih.gov/genbank/template/submission/

3. Getting your genome fasta file in the correct format: https://www.ncbi.nlm.nih.gov/genbank/table2asn/#fsa

4. Creating a table format from your GFF or GTF file : https://www.ncbi.nlm.nih.gov/genbank/table2asn/#tbl

5. Run the script: `table2asn -M n -J -c w -euk -t template.sbt  -gaps-min 10 -l paired-ends -j "[organism=Polybia occidentalis] -i fasta_file -f gff_file -o output_file.sqn -Z`
where all before template.sbt is the same. "template.sbt" should be in your currect directory (you got this from step 2).  Gaps default 10 is fine. -l is for evidence of linkage between reads, so for mate pair experiment disicgn, we use paired-ends option. The -j option needs the correct Genus and species name (in our case Polybia). -i is for our genome fasta file, -f is for our gff3 file. The output is stored in name specified after the -o flag. -Z is required for working directory (I think).


Use GAG 

1a. Check your GFF is valid :  http://genometools.org/cgi-bin/gff3validator.cgi
1b. Download GAG from : https://genomeannotation.github.io/GAG/

2. Run  the script: `~/Downloads/genomeannotation-GAG-997e384/gag.py --fasta P.occidentalis.RM_bactfilt.min500.euk.noNs.fasta --gff P.occidentalis.evm.consensus.annotation.v2a.gff3 --out gag_output --fix_terminal_ns`

3. Now we have a genome compatible with NCBI. So we can upload it in the browser.

B1. Start following these instructions: https://www.ncbi.nlm.nih.gov/genbank/eukaryotic_genome_submission/

