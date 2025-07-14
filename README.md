# Duplicate-Detection-in-Music-Metadata

## Overview  
This project addresses the problem of semantic duplication in large-scale music databases. Albums like _"Taylor Swift - Red"_ and _"Taylr Swift - RED (Deluxe)"_ may represent the same release but appear as different entries. Our goal was to develop a deduplication system to automatically detect such cases using string similarity metrics and rule-based logic.

---

## Research Questions  
1. How can we automatically detect and flag duplicate music album entries with inconsistent metadata?  
2. How well does our model perform compared to the ground truth duplicates?

---

## Dataset  
- **Primary file**: `cddb_discs.xml`  
- **Ground truth**: `cddb_9763_dups.xml`

### Key Challenges:
- Misspellings in artist/album names  
- Inconsistent casing and punctuation  
- Reordered or incomplete tracklists  
- Varying schema fields (`id` vs. `cid`)

---

## Methodology  
1. **XML Parsing** using `xml.dom.minidom`  
2. **Preprocessing**:  
   - Lowercasing and punctuation removal  
   - Fallback handling for `id`/`cid` fields  
3. **Similarity Scoring**:  
   - **Jaro-Winkler** for artist & title  
   - **Jaccard similarity** for unordered tracklists  
4. **Composite Score**:  
   - 40% artist + 40% album title + 20% track list  
5. **Classification**:  
   - Pairs with a similarity score > 0.65 were flagged as duplicates  
6. **Evaluation**:  
   - Used `scikit-learn` to compute Precision, Recall, F1

---

## Results  

| Metric            | Value |
|-------------------|-------|
| Precision         | 0.993 |
| Recall            | 0.933 |
| F1 Score          | 0.962 |
| Accuracy          | 0.927 |
| Predicted Matches | 280   |
| Ground Truth Pairs| 298   |

The model prioritized high precision, minimizing false positives.

---

## Technologies Used  
- **Languages**: Python  
- **Libraries**:  
  - `Jellyfish` (Jaro-Winkler)  
  - `scikit-learn` (evaluation metrics)  
  - `xml.dom.minidom` (XML parsing)  
- **Concepts**:  
  - Entity Resolution  
  - Schema Matching  
  - String Similarity  
  - Weighted Scoring

---

## Lessons Learned  
- Careful threshold tuning is essential; we iteratively adjusted to find 0.65 as the best trade-off.  
- Evaluation metrics like precision, recall, and F1 helped guide model improvements.  

## Report  
Refer to the full report for a more detailed explanation: [`report.pdf`](./report.pdf)

