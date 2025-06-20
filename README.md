# Casus-RA-Transcriptomics

# Inhoud en structuur
* data/raw/ – Data na het sequencen
* data/processed/ - Verwerkte data met scripts, gebruikt voor verdere analyses
* Scripts/ - Script gebruikt voor genereren van resultaten
* Resultaten/ - Figuren en tabellen
* README.md/ - Tekst voor hier genereren
* data_stewardship/ - Aantonen dat ik de compenties beheer
  
# Inleiding
Reumatoïde artritis (RA) is een chronische auto-immuunziekte die wordt gekenmerkt door aanhoudende ontstekingen in de synoviale gewrichten, leidend tot progressieve weefselschade, pijn en functieverlies (McInnes & Schett, 2011). De prevalentie van RA ligt wereldwijd tussen de 0,5% en 1%, waarbij vrouwen vaker getroffen worden dan mannen (Smolen et al., 2016). Hoewel de exacte oorzaak van RA niet volledig begrepen is, blijkt uit onderzoek dat zowel genetische factoren als epigenetische en transcriptionele regulatie een belangrijke rol spelen in het ontstaan en het verloop van de ziekte (Firestein & McInnes, 2017).

Genen die betrokken zijn bij ontstekingsprocessen en immuunroutes, zoals TNF, IL6, STAT1 en CXCL10, vertonen vaak een verhoogde expressie bij RA-patiënten in vergelijking met gezonde individuen (Wang et al., 2018). Deze genen dragen bij aan de activering van immuuncellen en het in stand houden van het ontstekingsproces. Door middel van transcriptoomanalyse kunnen zulke verschillen in genexpressie in kaart worden gebracht, wat inzichten kan opleveren in de onderliggende moleculaire mechanismen van RA.

Het doel van dit onderzoek is om met behulp van RNA-sequencing data en bioinformatica-analyse in RStudio de genexpressie te vergelijken tussen RA-patiënten en gezonde controles.

# Methoden
Voor deze studie werden RNA-seq datasets van vier reumatoïde artritis (RA) patiënten en vier gezonde controles gebruikt. De sequenties (paired-end) werden gealigned op het humane referentiegenoom GRCh38.p14 (GCF_000001405.40) met behulp van de align() functie van het Bioconductor-pakket Rsubread. Voorafgaand aan de alignments werd een referentie-index gegenereerd met buildindex(). De resulterende BAM-bestanden werden gesorteerd en geïndexeerd via Rsamtools.

Genexpressie telling werd verkregen met featureCounts(), gebruikmakend van een bijbehorend GTF-annotatiebestand. De rauwe tellingen werden verwerkt met DESeq2 voor normalisatie en differentiële expressie-analyse. Genen met een aangepaste p-waarde < 0.05 en een absolute log2 fold change > 1 werden als significant beschouwd. Visualisatie van resultaten gebeurde onder andere via een volcano plot (EnhancedVolcano) en een heatmap van de top 50 variantste genen (pheatmap).

Voor interpretatie werden significante genen omgezet naar Entrez-ID's (org.Hs.eg.db), gevolgd door verrijkings analyses met clusterProfiler voor KEGG- en GO-termen. Voor de visualisatie werden dotplots en barplots van de verrijkte pathways gemaakt. De Pathview-tool werd gebruikt voor het mappen van differentieel tot expressie gebrachte genen op specifieke KEGG-pathways.

# Resultaten
Een volcano plot toonde een duidelijke scheiding tussen op- en neer gereguleerde genen. De topgenen met de hoogste log2 fold change omvatten onder andere SRGN, BCL2A1 en PTGFR, die bekend staan om hun rol in ontsteking. Vervolgens werden deze bevindingen gecontroleerd met een heatmap om te kijken of deze ook significant hoger tot expressie kwamen. Uit deze analyse kwam dat genen zoals BCL2A1, SRGN en CYTIP significant veel hoger tot expressie kwamen in de RA groep dan in de controle groep.

De KEGG-pathwayverrijking analyse toonde significante betrokkenheid van onder andere “Epstein Barr virus”, “Rheumatoid arthritis” en “MAPK signaling pathway” pathways. GO-analyse bevestigde de activering van biologische processen zoals “Lymphocyte differentiation”, “Lymphocyte mediated immunity” en “leukocyte mediated immunity”.

# Conclusie 
In dit onderzoek is de genexpressie vergeleken tussen patiënten met reumatoïde artritis (RA) en gezonde controles, met als doel het identificeren van genen die bijdragen aan de pathogenese van RA. Uit de analyse bleek dat meerdere genen significant verhoogd tot expressie kwamen bij RA-patiënten, met name genen betrokken bij immuunactivatie en ontstekingsroutes. Interessant is dat verschillende van deze genen ook verhoogd tot expressie komen tijdens een infectie met het Epstein-Barr virus (EBV). Dit suggereert een mogelijk verband tussen latente of doorgemaakte EBV-infectie en de activatie van immuungerelateerde genen die ook bij RA een rol spelen. In een onderzoek van Barukčić et al.(2018) blijkt dat er mogelijk een verbinding is tussen Epstein barr virus en RA, en dat dit mogelijk zelfs een oorzaak van RA kan zijn. Alhoewel er ook aangegeven in dit onderzoek dat er nog veel vervolg onderzoek gedaan moet worden.,

Een belangrijk verbeterpunt in dit onderzoek is de metadata. De leeftijdsverdeling tussen de RA-patiënten en controlepersonen verschilde aanzienlijk, wat een verstorende factor kan zijn bij interpretatie van genexpressie. Voor toekomstige studies is het aan te raden om de patienten beter te matchen op leeftijd, geslacht en andere relevante klinische variabelen. Dit zou de betrouwbaarheid en reproduceerbaarheid van de resultaten verbeteren en bijdragen aan een beter begrip van de onderliggende moleculaire mechanismen bij RA.

