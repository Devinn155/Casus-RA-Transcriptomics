# Casus-RA-Transcriptomics

# Inhoud en structuur
* data/raw/ – Data na het sequencen
* data/processed/ - Verwerkte data met scripts, gebruikt voor verdere analyses
* Scripts/ - Script gebruikt voor genereren van resultaten
* Resultaten/ - Figuren en tabellen
* README.md/ - Tekst voor hier genereren
* data_stewardship/ - Aantonen dat ik de compenties beheer
  
# Inleiding
Reumatoïde artritis (RA) is een type chronische autoimmuun ziekte dat wordt gekenmerkt door ontstekingen in de gewrichten en progressieve weefselschade. RA komt ongeveer bij 0,5% - 1,0% bij de bevolking voor. Dit omvat zowel veranderingen in DNA-sequenties als epigenetische en transcriptionele processen die de genexpressie beïnvloeden. Genen die betrokken zijn bij ontstekings- en immuunroutes, zoals TNF, IL6, STAT1 en CXCL10, vertonen vaak afwijkende expressiepatronen bij RA-patiënten.


Op basis van bovenstaande informatie is het volgende doel opgesteld: Het vergelijken van samples van patienten met RA en controle monsters om de verschillen in de gen expressie te vergelijken met behukp van een transcriptoom analyse in R studio.

# Methoden
Voor deze studie werden RNA-seq datasets van vier reumatoïde artritis (RA) patiënten en vier gezonde controles gebruikt. De sequenties (paired-end) werden gealigned op het humane referentiegenoom GRCh38.p14 (GCF_000001405.40) met behulp van de align() functie van het Bioconductor-pakket Rsubread. Voorafgaand aan de alignments werd een referentie-index gegenereerd met buildindex(). De resulterende BAM-bestanden werden gesorteerd en geïndexeerd via Rsamtools.

Genexpressie telling werd verkregen met featureCounts(), gebruikmakend van een bijbehorend GTF-annotatiebestand. De rauwe tellingen werden verwerkt met DESeq2 voor normalisatie en differentiële expressie-analyse. Genen met een aangepaste p-waarde < 0.05 en een absolute log2 fold change > 1 werden als significant beschouwd. Visualisatie van resultaten gebeurde onder andere via een volcano plot (EnhancedVolcano) en een heatmap van de top 50 variantste genen (pheatmap).

Voor interpretatie werden significante genen omgezet naar Entrez-ID's (org.Hs.eg.db), gevolgd door verrijkings analyses met clusterProfiler voor KEGG- en GO-termen. Voor de visualisatie werden dotplots en barplots van de verrijkte pathways gemaakt. De Pathview-tool werd gebruikt voor het mappen van differentieel tot expressie gebrachte genen op specifieke KEGG-pathways.

# Resultaten
Een volcano plot toonde een duidelijke scheiding tussen op- en neer gereguleerde genen. De topgenen met de hoogste log2 fold change omvatten onder andere SRGN, BCL2A1 en PTGFR, die bekend staan om hun rol in ontsteking. De heatmap van de 50 meest significant gedifferentieerd tot expressie gebrachte genen toonde een duidelijke clustering van RA- versus controlesamples.

KEGG-pathwayverrijking toonde significante betrokkenheid van onder andere “Cytokine-cytokine receptor interaction”, “Rheumatoid arthritis” en “TNF signaling pathway”. GO-analyse bevestigde de activering van biologische processen zoals “immune response”, “chemokine-mediated signaling pathway” en “leukocyte migration”.

# Conclusie 
