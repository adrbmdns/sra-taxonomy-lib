Upload the organism name under 50557 to big query name it as ```50557_subtree```. 

## 1. Get metadata table where the accession is sequenced from organisms under 50557

```sql
SELECT *
FROM `nih-sra-datastore.sra.metadata`
WHERE organism IN (SELECT organism FROM `big-query-insect-library.sra.50557_subtree`) 
```

Save it as ```metadata_acc_seq_from_50557```. 

## 2. Get tax analysis table where the tax id is 198112 and the total count greater than 1000

```sql
SELECT * 
FROM `nih-sra-datastore.sra_tax_analysis_tool.tax_analysis`
WHERE tax_id = 198112 and total_count > 1000 
```

Save it as ```tax_analysis_198112_1000```. 

## 3. Get the metadata table that the accession is sequenced from a organism under 50557 and the accession has more than 1000 counts of 198112

```sql
SELECT * 
FROM `big-query-insect-library.sra.metadata_acc_seq_from_50557`
WHERE acc IN (SELECT acc FROM `big-query-insect-library.sra.tax_analysis_198112_1000`)
```

Save it as ```metadata_50557_has_1000_198112```. 
