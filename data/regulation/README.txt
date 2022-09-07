# E. coli TRN

The E. coli TRN was constructed using both RegulonDB and Ecocyc. Ecocyc contains all binding information from RegulonDB, plus a few extra non-standard regulators (ppGpp, dksA, riboswitches, transcriptional attenuation, csrA, etc.). However, RegulonDB includes the confidence level for each regulatory interaction.

The final TRN is stored in the [TRN.csv](TRN.csv) file

## RegulonDB
The following files were downloaded from the [RegulonDB download page](http://regulondb.ccg.unam.mx/menu/download/datasets/index.jsp)
* GeneProductSet.txt
* network_sigma_gene.txt
* network_tf_gene.txt
* sRNABindingSiteSet.txt

## Ecocyc
The Ecocyc regulator table was created using Ecocyc's Smart Table. To create this table:
1. Go to Ecocyc Smart Tables
2. Get "Special Smart Table" -> All genes of E. coli K-12 substr. MG1655
3. Select "Add Transform Column" -> "Regulation - Direct regulators of genes"
4. Select "Regulation" column
5. Under "Operations", select "New" -> "SmartTable from Column"
6. Select the "Regulation" column
7. Select "Add Property Column" -> "Common-Name"
8. Select "Add Transform Column" -> "Genes of polypeptide, complex, or RNA"
9. Select the "Genes of polypeptide, complex, or RNA" column
10. "Add Property Column" -> "Common-Name"
11. Select "Matches" column
12. Under "Operations", select "Column" -> "Move" -> "Move Column Full Right"
13. Select "Add Property Column" -> "Common Name"
14. Select "Add Property Column" -> "Accession-1"
15. Under "Operations", select "Export" -> "to Spreadsheet File..." -> "Export smarttable"
