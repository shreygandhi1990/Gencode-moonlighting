# Gencode-moonlighting

## Data download
1. The annotated human transcriptome data was downlaoded from the [GENCODE](http://www.gencodegenes.org/) consortia through their ftp site (ftp://ftp.sanger.ac.uk/pub/gencode/Gencode_human)
2. The downloaded data was in form of gene transfer format (GTF) format.
3. The files which were publically available for download was for versions V1 to V24. Note -  V3a was not publically available.

![test] (https://github.com/vinodscaria/Gencode-moonlighting/blob/master/images/Picture1.png "About")

## Data Pre-processing
1. From the individual GTF files which were downloaded, we extracted all the transcripts, and made a list of unique transcript IDs assigned under the “transcript_id” identifier and their corresponding “havana_transcript” identifier if present. Uptil V3d the havana IDs were used as the main identifiers and thus we took them as such. Note - For V1, no gene or transcript information were available. Hence, we  had to extract this information from the exonic coordinates present in the GTF file. We compiled the list of transcript biotype assigned to these unique transcripts which were extracted from GTF files (Compiled with all versions.txt)
2. For all ENSTs we removed numbers after the dot.
3. From the file,  we replaced 218 ENST IDs with their respective ENSTR 
4. Removing redundancies by replacing OTTHUMT (Havana Ids) with ENST (Ensembl Ids)
	* 77,193 had single ENST prefixed (converted)
	* 1,982 OTTHUT prefixed  IDs had more than one ENST IDs in the same version (OTTHUMT prefixed IDs were duplicated by assigning them both the Ensembl prefixed IDs while keeping their biotypes intact) 
	* 3,188 OTTHUT prefixed IDs having more than one ENST prefixed IDs assigned to them across versions (ENST IDs duplicated and assigned biotypes of both the OTTHUMT IDs)
	* 3,272  as OTTHUMT as no ENST existed for them
5. Labeled transcript biotype as “NA” when no biotype was assigned in any particular version.  

## Processed Complete File 
1. The complete file which we compiled consisted for 2,51,614 transcript ids (Masterfile.txt.)
2. We further assigned number codes to the biotypes present in the Masterfile. (Masterfile converted to codes.txt)
3. We plotted the distribution of biotypes across all the GENCODE versions using RAW app.

## Biotype wise data processing (Mention commands)
1. Extracted the assigned biotypes for each transcript id across versions. Assigned “NA” to transcripts having no biotype.
2. 1,14,114 protein coding transcripts extracted across 28 versions (had PC biotype anytime in their lifetime)
3. Identified 23 sub-classes of lncRNAs which are listed in Table 2 
4. Renamed transcripts having anyone of the 23 biotype as lncRNA in our study
5. 1,20,864  lncRNA transcripts extracted across 28 versions (had lncRNA biotype anytime in their lifetime)
6. Compiled the total transcripts having PC and lncRNA biotype for further processing


## To check how many transcripts were added or deleted in each version of GENCODE (Mention commands)
1. To check number of added transcripts
           * If a biotype for a particular transcript was labelled as “NA” in Version n (Vn) and the same transcript had an assigned biotype (X)  in next Version (Vn+1), then we considered that the transcript has been added in next version. Table 3
2. To check number of deleted transcripts
           * If a biotype for a particular transcript was assigned (X) in Version n (Vn) and the same transcript was labeled as “NA”  in next Version (Vn+1), then we considered that the transcript has been deleted in next version. Table 3

## To check the consistency of biotype for a transcript (Mention commands)
1. If a transcript has the same biotype across all versions of GENCODE, hence we can say that it is consistent
2. 19,520 lncRNA  and 32,458 protein coding transcripts had same across all GENCODE classes
3. the ones which did have were denoted to have moonlighting annotations (Table 4 and 5) 

## Switching of transcripts across versions (Mention commands/script)
1. If the biotype of a transcript in version n (Vn) is not equal to the biotype of same transcript in next version (Vn+1), then it was labelled as having moonlighting annotation.  (Table 6)
