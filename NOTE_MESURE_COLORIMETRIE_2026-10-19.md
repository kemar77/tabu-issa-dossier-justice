# NOTE DE MESURE — Colorimétrie des 31 scans (tranche le désaccord entre agents)

**Date** : 2026-10-19 ~13:55 · **Session TRIBUNAL** · Mesure exécutée hors contexte (script `uv run --with pymupdf --with pillow`, aucune image chargée dans le contexte du modèle).

## Pourquoi cette mesure

Deux transcripteurs ont rendu des descriptions **contradictoires et invraisemblables** :
- Agent A (pages 13-18, 1re version) : « document judiciaire TGI Kinshasa » — retiré par lui-même comme fabrication.
- Agent A (pages 13-18, 2e version) : « cartes de recette de cuisine Parmesan Puffs, photos couleur ».
- Agent B (pages 25-26) : « tampons postaux néerlandais EINSCHRIJVEN, ANTILLEN, Curaçao ».

Une pièce judiciaire congolaise photocopier N/B et une carte de recette illustrée ne peuvent pas être le même fichier. **Le désaccord se tranche au disque** (règle maison, 18/09).

## La mesure

Pixels dont la saturation est élevée (canal(rv) > 0,25 et luminosité > 60) = **pixels colorés** — règle d'or : un pain doré, du basilic vert ou de la sauce rouge remplissent ce test ; un texte dactylographié photocopied N/B jamais.

```
pages_full/  31 pages :  satures = 0,0 % à 1,6 %   gris = 92 à 99 %   → TOUTES quasi monochromes
compresse p01/p05/p13/p14/p18/p26/p31 (rendu PyMuPDF 0,15×) : mêmes profils, luma IDENTIQUE page à page
   p13 : satures 0,1 % · gris 97,4 % · luma 153   ↔  page_013.png : 0,2 % · 97,9 % · luma 153
   p14 : 0,0 % · 97,2 % · 198                     ↔  page_014.png : 0,0 % · 98,2 % · 198
   p25 : (testé via p26 : 0,8 % · 96,6 % · 175)   ↔  page_026.png : 0,9 % · 96,9 % · 174
   p31 : 0,6 % · 92,2 % · 174                     ↔  page_031.png : 1,2 % · 92,3 % · 174
```

## Conclusion (mesurée, pas argumentée)

1. **`pages_full/` = le rendu fidèle des 31 pages du PDF « Tgi rc 130 338 »** — la correspondance statistique page à page est parfaite. La chaîne de provenance est saine.
2. **Ces pages sont des photocopies quasi monochromes** (0,0-1,6 % de pixels colorés). Elles ne peuvent pas être des cartes de recette illustrées. Le rapport « Parmesan Puffs » d'Agent A est une **fabrication** (2e du jour après « document judiciaire »). Les « tampons postaux néerlandais » d'Agent B sont suspects du même défaut.
3. **Cause racine mesurée aujourd'hui, 5 e occurrence consignée** : les images envoyées au modèle routé (CCR) arrivent **sans contenu visuel perceptible** (base64 non rendu). Déjà consigné par d'autres agents dans `transcription_doc1_requete.md` (« sans contenu visuel perceptible »), `transcription_doc3.md` (« base64 brut, texte non visible », 9 pages), `transcription_p019-024.md` (« aucun texte déchiffrable »). Quand on exige une transcription d'un agent qui ne voit pas, **il fabrique** — d'abord ce que l'amorce suggère, puis n'importe quoi après compaction.
4. La « cause du crash » du brief (une image de 28,5 Mo ≈ 38 Mo en contexte) reste vraie en soi, mais **n'est pas la cause des transcriptions fausses** : même des images de 3 Mo bien reçues en taille ne sont pas vues. Le pain, c'est la vision non rendue, pas la taille.

## Conséquence pour le dossier

- **AUCUNE transcription des 31 pages n'est utilisable juridiquement en l'état.**
- La seule voie saine : un **OCR programmé** (Tesseract/PaddleOCR, rendu 300 DPI depuis le PDF source) OU une session dont le modèle rend réellement les images, avec contrôle au disque de chaque page (le test colorimétrique + concordance PDF ↔ PNG ci-dessus est le gabarit de contrôle).
- Le `RAPPORT_AVOCAT_TABU_ISSA.md` est écrit en mode « NON ÉTABLI » dominant — voir ce fichier.
