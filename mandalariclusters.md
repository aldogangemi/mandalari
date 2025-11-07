Analysis of how the texts and authors (patients) can be clustered using diagnoses, occupations, and semantic frames.

##  Conceptual Clustering Strategy

### Clustering Authors (Patients)

Authors can be clustered by directly combining their metadata (diagnosis and occupation) with the aggregated semantic frames from all the documents they've written.

**Features for Clustering Authors:**

1.  **Diagnosis (via `:hasMainDiseaseCondition`):** This provides a clinical baseline.
    * *Examples:* `kg:Paranoid_Syndrome`, `kg:Schizophrenia`, `kg:Paranoia`, `kg:Hypomania`.
2.  **Occupation (via `:hasOccupation`):** This provides a socio-economic and professional context.
    * *Examples:* `kg:Military` (or `kg:Carabiniere`), `kg:Teacher`, `kg:Accountant`, `kg:Student`, `kg:Farmer`.
3.  **Aggregated Frames (via `:isAuthorOf` -> `:denotes`):** This creates a "semantic fingerprint" for each author, showing their recurring themes and preoccupations across all their writings.

---

####  Emergent Author Clusters

Based on these features, we predict several distinct author clusters:

**Cluster 1: The "Paranoid-Persecutory" Group**
    **Diagnosis:** `kg:Paranoid_Syndrome`, `kg:Paranoid_Delusion`, `kg:Persecutory_Delusion`.
    **Authors:** `kg:Pappalardo_Michele`, `kg:Baiardo_Luigi`, `kg:Di_Blasi_Antonino`, `kg:Astri_Norina`, `kg:De_Francesco_Francesco`.
    **Dominant Frames:** These authors consistently produce texts dominated by frames of external threat and conflict, such as **`:Persecution`**, **`:Conspiracy`**, **`:Poisoning`**, **`:Mistreatment`**, and **`:Technology_as_Persecution`**.

**Cluster 2: The "Grandiose-Mystical" Group**
    **Diagnosis:** `kg:Schizophrenia`, `kg:Paranoid_Schizophrenia`, `kg:Dementia_Praecox_with_Paranoid_variety`.
    **Authors:** `kg:Sanfilippo_Orazio`, `kg:Orso_Carmine_Giuseppe`, `kg:Graziano_Leonardo`, `kg:Crino_Giuseppe`.
    **Dominant Frames:** This group's writings are characterized by frames of an expanded, divine, or messianic self. Common frames include **`:Grandiose_Delusions`**, **`:Mystical_Religious_Delusions`**, **`:Mission`**, **`:Neologisms`**, and **`:Religious_Mania`**.

**Cluster 3: The "Authoritarian-Conflict" Group**
    **Occupation:** `kg:Military`, `kg:Carabiniere`, `kg:Prison_Guard` (e.g., `kg:C_Francesco`, `kg:Di_Blasi_Antonino`, `kg:DAmico_Onofrio`, `kg:Lo_Castro_Giuseppe`, `kg:Sgariglia_Bonaventura`).
    **Authors:** This cluster is defined by occupation. While their diagnoses vary, their writings show a fixation on themes of hierarchy, rules, and justice.
    **Dominant Frames:** They frequently use frames like **`:Appeal_to_Authority`** (especially `_military`), **`:Conflict_with_Authority`**, **`:Official_Report`**, and **`:Vindication_Justice`**.

**Cluster 4: The "Educated/Professional" Group**
    **Occupation:** `kg:Teacher`, `kg:Priest`, `kg:Accountant`, `kg:Court_Clerk` (e.g., `kg:Gabriele_Alfredo`, `kg:Ioppolo_Giovanni`, `kg:Raynieri_Giacomo`, `kg:Bellabarba_Giovan_Battista`).
    **Authors:** This group's texts often show higher formal structure or specific intellectual themes.
    **Dominant Frames:** Frames like **`:Philosophical_Reflection`**, **`:Poetic_Expression`**, **`:Logical_Philosophical_Reasoning`**, and **`:Legal_Bureaucratic_Document`** are more likely to appear.

---

### Clustering Texts

Texts can be clustered more directly. Each document is a single data point, and its features are the frames it contains, plus the metadata of its author.

**Features for Clustering Texts:**

1.  **Author's Diagnosis:** The diagnosis of the author (e.g., `kg:Paranoid_Syndrome` for `kg:doc_1`).
2.  **Author's Occupation:** The occupation of the author (e.g., `kg:Army_Officer` for `kg:doc_1`).
3.  **Vector of Frames:** A list or count of all frame instances (`dul:Situation`) associated with the document (e.g., `kg:doc_1` contains `:Betrayal`, `:Persecution`, `:Religious_Mystical_Delusions`).

---

#### Emergent Text Clusters

**Cluster 1: "Persecution & Torture Narratives"**
    **Content:** These texts are focused, detailed accounts of being tormented.
    **Key Frames:** `:Persecution`, `:Poisoning`, `:Mistreatment`, `:Torture`, `:Technology_as_Persecution`.
    **Example Texts:** `kg:doc_98` (Astri Norina: Eletrotecnica, raggio X), `kg:doc_63` (Baiardo Luigi: Villa dei supplizi), `kg:doc_99` (De Francesco: Tomba dei Giustizziati, potenti veleni), `kg:doc_125` (Trovato Gaetano: medicinali atti a squassarmi).

**Cluster 2: "Grandiose & Prophetic Manifestos"**
    **Content:** Texts where the author claims a special identity, power, or mission.
    **Key Frames:** `:Grandiose_Delusions`, `:Grandiose_Religious_Delusion`, `:Mission`, `:Neologisms`.
    **Example Texts:** `kg:doc_30-32` (Sanfilippo: Comandante papa Deu), `kg:doc_41-45` (Bellabarba: Giovanni Battista di Savoia), `kg:doc_251-257` (P. Domenico: Finale Ereditario Principe Tuttia), `kg:doc_1-8` (Pappalardo: Zevaco Zilio Michele P. Angelo Arvedi).

**Cluster 3: "Bureaucratic & Legal Appeals"**
    **Content:** Formal letters and petitions to authorities (doctors, military, legal) demanding release, justice, or money.
    **Key Frames:** `:Appeal_to_Authority`, `:Vindication_Justice`, `:Plea_for_Release`, `:Bureaucratic_Request`, `:Financial_Concerns`.
    **Example Texts:** `kg:doc_66-87` (D'Amico: A long series of formal requests and reports to military and legal authorities), `kg:doc_282-284` (Lo Castro: Official reports of on-duty conflicts), `kg:doc_90` (Di Blasi: Formal legal denunciation of his confinement).

**Cluster 4: "Creative & Poetic Works"**
    **Content:** Texts that are explicitly creative endeavors, such as poems, songs, or plays.
    **Key Frames:** `:Poetic_Expression`, `:Creative_Writing`, `:Fable_Storytelling`, `:Poetic_Expression_Songwriting`.
    **Example Texts:** `kg:doc_142-148` (Randazzo: A collection of dramatic dialogues and poems like "Bance e Filemone"), `kg:doc_226-231` (Bazza: Poems and songs like "Buona Strada e Buon Mare"), `kg:doc_126` (Sacca: "L'Inno degli Scugnizzi del Lavoro").

---

### Clustering Frames

Finally, we can cluster the situation *types* themselves based on the semantic roles they use (their properties) and the types of participants they involve. This helps identify "super-clusters" or families of frames.

**Features for Clustering Frames:**

1.  **Roles Used:** The object properties associated with the frame (e.g., `:hasAgent`, `:hasPatient`, `:hasAddressee`).
2.  **Inferred Participant Types:** The *kind* of entities filling those roles (e.g., "Family Members," "Authority Figures," "Supernatural Beings").

---

#### Emergent Frame Clusters

**Cluster A: "Conflict & Persecution" Frames**
    **Frame Types:** `:Persecution`, `:Conspiracy`, `:Mistreatment`, `:Poisoning`, `:Torture`, `:Betrayal`.
    **Common Roles:** These frames share a clear "antagonistic" structure. They are defined by the roles **`:hasAgent`** (the persecutor) and **`:hasPatient`** or **`:hasVictim`** (the person being harmed, usually the author).
    **Inferred Participants:** "Authority" (e.g., `kg:Direttore`, `kg:Manicomio_staff`), "Supernatural" (e.g., `kg:demoni`), or "Family/Social" (e.g., `kg:nipote`, `kg:ex_partito_socialista_riformista`).

**Cluster B: "Grandiose Self" Frames**
    **Frame Types:** `:Grandiose_Delusions`, `:Grandiose_Religious_Delusion`, `:Mission`, `:Prophecy_Revelation`.
    **Common Roles:** These frames are "introspective" or "proclamatory." They are defined by the **`:hasExperiencer`** or **`:hasProtagonist`** role (the author) and often a **`:hasTheme`** role (the subject of the grandiosity, e.g., `kg:Re_Davide`, "Principe Ruggeri").
    **Inferred Participants:** "Self," "Divine/Historical Figures."

**Cluster C: "Communication & Appeal" Frames**
    **Frame Types:** `:Appeal_to_Authority`, `:Bureaucratic_Request`, `:Plea_for_Release`, `:Vindication_Justice`, `:Complaint`.
    **Common Roles:** These frames are "transactional." They are defined by their social roles: **`:hasRequester`** or **`:hasProtagonist`** (the author) and an **`:hasAddressee`** (the person being appealed to).
    **Inferred Participants:** "Self" and "Authority Figures" (e.g., `kg:Signor_Prefetto`, `kg:Comando_del_75_reggimento_fanteria`, `kg:Illmo_sig_Direttore`).

**Cluster D: "Interpersonal & Family" Frames**
    **Frame Types:** `:Family_Conflict`, `:Marital_Conflict`, `:Family_Appeal`, `:Love_Betrayal`, `:Abandonment`.
    **Common Roles:** These frames are "relational." They are defined by roles like **`:hasProtagonist`** (the author), **`:hasAntagonist`** (the family member in conflict), and **`:hasAddressee`** (the family member being written to, e.g., "Cara Moglie", "Caro_padre").
    **Inferred Participants:** "Family Members."

---

Analysis by clustering the authors and texts, but using only the quantitative creativity data from the allcreativitydata.tsv.

Text Clusters: Distribution of Creativity
Analyzed the distribution of the combined creativity score (CreatWaas_minmax) across all 372 texts to see how creativity is clustered across the entire collection.

The distribution shows a wide range of creative output. While a large number of texts have low-to-mid-range creativity scores (scores between 0.5 and 0.7), there is a significant "long tail" of texts that demonstrate exceptionally high creativity (scores > 0.8). This suggests that while most writing is conventional, a distinct cluster of texts represents powerful creative and authorial efforts.

Author Clusters: Top Creative & Authorial Patients
Clustered the authors by calculating the mean aggregate scores for all documents they wrote. This reveals distinct groups of authors: those who are "most creative" (highest CreatWaas_minmax) and those who have the "most authorial control" (highest Authoriality_WAAS_minmax).

Summary table, author_creativity_summary.csv:

Top 10 Most Creative Authors
This cluster is led by authors who produce highly novel, semantically divergent, and elaborated worlds.
S. Francesco (Mean CreatWaas_minmax: 0.827)
Sacca Antonino (Mean CreatWaas_minmax: 0.804)
Mastroeni Nicola (Mean CreatWaas_minmax: 0.764)
S. FRANZ (Mean CreatWaas_minmax: 0.732)
Graziano Leonardo (Mean CreatWaas_minmax: 0.732)
Ioppolo Giovanni (Mean CreatWaas_minmax: 0.732)
SINOPOLI LETTERIO (Mean CreatWaas_minmax: 0.731)
Randazzo Vito (Mean CreatWaas_minmax: 0.731)
D. GUGLIELMO (Mean CreatWaas_minmax: 0.725)
Scuderi Rosario (Mean CreatWaas_minmax: 0.706)
Top 10 Most "Authorial" Authors (Highest Control)
This cluster represents authors with the highest "Weighted Authorial Adherence Score" (WAAS), indicating texts that are systematic, coherent, and rhetorically aware (i.e., well-structured and written for an audience).
Randazzo Vito (Mean Authoriality_WAAS_minmax: 0.875)
Sacca Antonino (Mean Authoriality_WAAS_minmax: 0.831)
Scuderi Rosario (Mean Authoriality_WAAS_minmax: 0.825)
Galuppi Giovanni (Mean Authoriality_WAAS_minmax: 0.797)
Portale Salvatore (Mean Authoriality_WAAS_minmax: 0.778)
Cavoli Antonino (Mean Authoriality_WAAS_minmax: 0.741)
Gambino Domenico (Mean Authoriality_WAAS_minmax: 0.734)
Bazza Vincenzo (Mean Authoriality_WAAS_minmax: 0.733)
D. Leonardo (Mean Authoriality_WAAS_minmax: 0.707)
O. Angelo (Mean Authoriality_WAAS_minmax: 0.682)
Interestingly, Randazzo Vito, Sacca Antonino, and Scuderi Rosario appear in the top of both lists, suggesting they are a cluster of authors who combine high creative novelty with exceptionally strong authorial control.

Deeper Analysis: Component Score Profiles
To understand why these authors are clustered differently, we analyzed their component authoriality scores. Two different "profiles" for creativity and authorial control emerged:

Profile 1: The Visionary (S. Francesco)
S. Francesco is the most creative author. His authoriality profile shows:
Authoriality_Systematicity: 0.9 (Very High)
Authoriality_RhetoricalAwareness: 0.8 (High)
Authoriality_MetaphoricalControl: 0.7 (High)
Authoriality_LiteralBelief: 0.8 (Very High)
Authoriality_PrivateExpression: 0.4 (Low-Mid)
Authoriality_Fragmentation: 0.1 (Very Low)
Interpretation: S. Francesco's creativity comes from being a "visionary." His writing is systematic, persuasive, and metaphorically rich, but he also shows a very high level of literal belief in his fantastic claims (his texts, 264 and 265, are detailed astrological biographies presented as fact ). His authorial control is strong, but it is in service of a deeply believed, private cosmology.

Profile 2: The Classic Author (Randazzo Vito)
Randazzo Vito is the most "authorial" author. His profile is a stark contrast:
Authoriality_Systematicity: 0.9 (Very High)
Authoriality_RhetoricalAwareness: 0.8 (High)
Authoriality_MetaphoricalControl: 0.79 (Very High)
Authoriality_LiteralBelief: 0.21 (Very Low)
Authoriality_PrivateExpression: 0.1 (Very Low)
Authoriality_Fragmentation: 0.1 (Very Low)
Interpretation: Randazzo Vito is a "classic author" or "artist." His texts (142-148) are conventional poems and dramatic dialogues . His score for LiteralBelief is extremely low because he is not literally reporting his reality; he is consciously crafting art. His PrivateExpression is also very low because his work is intended for a public audience. He has maximum authorial control because he is not lost in a private, literally-believed delusion. He is in full command of his metaphors.

In summary, we see two main clusters of highly-rated authors:
Visionaries (like S. Francesco): High creativity derived from a systematic, metaphor-rich, and literally-believed private world.
Artists (like Randazzo Vito): High creativity derived from a systematic, metaphor-rich, and consciously-crafted public work, where they do not literally believe the content.

---

Manual cross-referencing of "top-tier" authors from the creativity data with their associated texts and frames in the knowledge graph:

These authors are not a single group. As seen in previous analyses, two different types of creative production emerge:

1.  **The "Visionaries" (High Creativity):** These authors score high on creativity because they build systematic, novel, and elaborate *private worlds*. Their authoriality profile is marked by **high `LiteralBelief`**, meaning they are not crafting metaphors but are describing what they believe to be true.
2.  **The "Classic Artists" (High Authoriality):** These authors score high on authorial control because they master *public, conventional forms* (like poetry and drama). Their profile is marked by **low `LiteralBelief`**, as they are consciously crafting art for an audience, not reporting a literal reality.

Correlation of key authors to their frame profiles:


### 1. The "Visionaries" (High Creativity, High Literal Belief)

This cluster's high creativity scores are driven by the "Grandiose Self" frame profile (Cluster B). They are building and explaining their own complex, private cosmologies.

**Author: S. Francesco**
    **Creativity Profile:** The #1 most creative author (Mean `CreatWaas_minmax`: 0.827). His profile is systematic and rhetorical but defined by very high `LiteralBelief` (0.8) .
    **Frame Profile:** His texts (`doc_264`, `doc_265`) are exclusively linked to the **`:Mystical_Astrological_Prediction`** frame .
    **Correlation:** His creativity score directly reflects his frame profile. He is a "Visionary" who systematically constructed a detailed astrological/prophetic model and presented it as literal fact .

**Author: Mastroeni Nicola**
    **Creativity Profile:** The #3 most creative author (Mean `CreatWaas_minmax`: 0.764) .
    **Frame Profile:** His texts (`doc_219`, `doc_220`) are dominated by the **"Grandiose Self"** cluster (Cluster B). He uses frames like **`:Mystical_Occult_Beliefs`** and **`:Religious_Mania`** , culminating in the frame **`:Grandiose_Delusions`** where he explicitly names himself a "Professor of Occult Sciences" .
    **Correlation:** His high creativity score comes from this systematic "Grandiose Self" profile. He then *uses* this identity in a highly creative, rhetorical act in `doc_221` : he leverages the **"Communication & Appeal"** cluster (Cluster C) by "confessing" to a crime (`:Confession` ) as a novel, paradoxical ploy to get arrested and prove his sanity (`:Vindication_Justice` ).

### 2. The "Classic Artists" (High Authoriality, Low Literal Belief)

This cluster's high authoriality scores are driven by their mastery of conventional, public creative forms (Text Cluster 4). Their high "metaphorical control" and low "literal belief" scores are a perfect match for their frame profiles.

**Author: Randazzo Vito**
    **Creativity Profile:** The #1 most "authorial" author (Mean `Authoriality_WAAS_minmax`: 0.875). His profile is defined by very high control and very low `LiteralBelief` (0.21) .
    **Frame Profile:** His texts are almost *exclusively* linked to the **"Creative & Poetic Works"** text cluster. His frames include **`:Creative_Writing`** (for his plays `doc_142`, `doc_145`, `doc_146`, `doc_147`, `doc_357`) and **`:Poetic_Expression`** (for his poems `doc_143`, `doc_144`, `doc_148`) .
    **Correlation:** The quantitative data and qualitative frames align perfectly. He is the most "authorial" because he is a *literal artist*. He is not reporting delusions; he is writing plays and poems with high formal control, hence his low `LiteralBelief` score.

**Author: Scuderi Rosario**
    **Creativity Profile:** The #3 most "authorial" author (Mean `Authoriality_WAAS_minmax`: 0.825) .
    **Frame Profile:** Like Randazzo, his texts map to the **"Creative & Poetic Works"** cluster. His frames are **`:Political_Praise`** (for his patriotic odes `doc_136`, `doc_137`) and **`:War`** / **`:Family_Conflict`** (for his short story `doc_138`) .
    **Correlation:** His high authorial control score is explained by his mastery of conventional genres (odes, novellas). He is a "Classic Artist" demonstrating high rhetorical skill and control over his metaphors.

### 3. The "Hybrid" Author (Sacca Antonino)

Sacca Antonino is unique because he scores at the top of *both* lists: #2 Most Creative and #2 Most Authorial. His frame profile clearly explains why.

**Author: Sacca Antonino**
    **Creativity Profile:** A rare blend of high creativity (`CreatWaas_minmax`: 0.804) and high control (`Authoriality_WAAS_minmax`: 0.831) .
    **Frame Profile:** He is a master of *both* clusters.
        **"Classic Artist" Frames:** In `doc_126` and `doc_128` , he uses purely artistic frames like **`:Political_Satire`** ("L'Inno degli Scugnizzi del Lavoro") and **`:Fantastical_Mythological_Journey`** ("Un viaggio all'Olimpo") . These are works of high metaphorical control.
        **"Visionary" Frames:** In `doc_127` , he switches to a manifesto of the **"Conflict & Persecution"** cluster (Cluster A), using frames like **`:Anti_fascism`**, **`:Anti_monarchy`**, **`:Persecution`** ("luogo di tortura scientifica"), and **`:Political_Rebellion_Threat`** ("demoliremo il fascismo... Piazzeremo madamo ghigliottina") . These are presented with 100% literal belief.
    **Correlation:** Sacca Antonino's "hybrid" quantitative profile is a direct reflection of his unique ability to operate as both a **"Classic Artist"** and a **"Visionary"**, switching between conventionally creative public art and highly systematic, literally-believed paranoid manifestos.