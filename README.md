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
Een volcano plot toonde een duidelijke scheiding tussen op- en neer gereguleerde genen. De topgenen met de hoogste log2 fold change omvatten onder andere SRGN, BCL2A1 en PTGFR, die bekend staan om hun rol in ontsteking. Vervolgens werden deze bevindingen gecontroleerd met een heatmap om te kijken of deze ook significant hoger tot expressie kwamen. Uit deze analyse kwam dat genen zoals BCL2A1, SRGN en CYTIP significant veel hoger tot expressie kwamen in de RA groep dan in de controle groep.

De KEGG-pathwayverrijking analyse toonde significante betrokkenheid van onder andere “Epstein Barr virus”, “Rheumatoid arthritis” en “MAPK signaling pathway” pathways. GO-analyse bevestigde de activering van biologische processen zoals “Lymphocyte differentiation”, “Lymphocyte mediated immunity” en “leukocyte mediated immunity”.

# Conclusie 
In dit onderzoek is de genexpressie vergeleken tussen patiënten met reumatoïde artritis (RA) en gezonde controles, met als doel het identificeren van genen die bijdragen aan de pathogenese van RA. Uit de analyse bleek dat meerdere genen significant verhoogd tot expressie kwamen bij RA-patiënten, met name genen betrokken bij immuunactivatie en ontstekingsroutes. Interessant is dat verschillende van deze genen ook verhoogd tot expressie komen tijdens een infectie met het Epstein-Barr virus (EBV). Dit suggereert een mogelijk verband tussen latente of doorgemaakte EBV-infectie en de activatie van immuungerelateerde genen die ook bij RA een rol spelen. In een onderzoek van Katarina B.(2018) blijkt dat er mogelijk een verbinding is tussen Epstein barr virus en RA, en dat dit mogelijk zelfs een oorzaak van RA kan zijn. Alhoewel er ook aangegeven werd dat er nog veel vervolg onderzoek gedaan moet worden.,

Een belangrijk verbeterpunt in dit onderzoek is de metadata. De leeftijdsverdeling tussen de RA-patiënten en controlepersonen verschilde aanzienlijk, wat een verstorende factor kan zijn bij interpretatie van genexpressie. Voor toekomstige studies is het aan te raden om de cohorten beter te matchen op leeftijd, geslacht en andere relevante klinische variabelen. Dit zou de betrouwbaarheid en reproduceerbaarheid van de resultaten verbeteren en bijdragen aan een beter begrip van de onderliggende moleculaire mechanismen bij RA.

