# Isles Pony Identification Dataset

## Overview

The Isles Pony Identification Dataset contains everyday photographs of 122 individual ponies from **Élevage des Isles, Normandy, France**. It supports research on individual animal identification, image retrieval, transfer learning, unknown-identity rejection, and matching between head and full-body views.

The photographs were publicly posted on the establishment's social media and grouped by pony for this study. Élevage des Isles has authorized public dissemination of the photographs and their use for scientific research, with the aim of helping other researchers. We gratefully acknowledge the establishment for supporting the sharing and scientific reuse of this collection.

The collection contains no photographs of people, as confirmed by the corpus curator.

**Dataset creators:** Anonymous

**Contact:** Anonymous

**Dataset DOI:** [Anonymous]

**Version:** [1.0]

## Dataset inventory

The original collection contains 1,549 JPEG photographs. Experiments use an audited subset of 1,546 photographs after excluding one image from each of three perceptually similar pairs.

| Property | Original collection | Audited experimental subset |
|---|---:|---:|
| Pony identities | 122 | 122 |
| Photographs | 1,549 | 1,546 |
| Main-cohort identities | 115 | 115 |
| Main-cohort photographs | 1,505 | 1,502 |
| Sparse-cohort identities | 7 | 7 |
| Sparse-cohort photographs | 44 | 44 |
| Minimum photographs per pony | 5 | 5 |
| Median photographs per pony | 12 | 12 |
| Maximum photographs per pony | 22 | 22 |
| Head photographs | 197 | 196 |
| Full-body photographs | 1,139 | 1,137 |
| Partial-view photographs | 213 | 213 |
| Ponies with both head and full-body views | 83 | 83 |

The main cohort originally includes ponies with at least ten photographs each. One of these ponies has nine retained photographs after the audit exclusions and remains in the main cohort. The seven sparse identities have five to seven photographs each.

## Photograph organization and identity labels

Photographs are organized under two directories:

- `au_moins_10_photos/`: the 115 main-cohort ponies;
- `moins_de_10_photos/`: the seven sparse-cohort ponies.

Each subdirectory represents one pony and contains its photographs. Folder membership supplies the identity label. Preserve the directory names and original filenames when using the annotations and evaluation manifests.

Identity labels are photographic collection labels. They have not been independently verified against administrative identification records, transponders, or ownership documents.

## Human view annotations

`annotations_vues.csv` contains annotations for all 1,549 original photographs, including the three images excluded from the experimental subset. It is a **semicolon-separated CSV file**, encoded in UTF-8; readers should support a possible UTF-8 byte-order mark.

| Column | Description |
|---|---|
| `image_id` | Identifier assigned by the annotation application; not an experimental catalog index. |
| `relative_path` | Image path relative to the collection root. |
| `identity` | Pony folder name. |
| `group` | Main or sparse directory: `au_moins_10_photos` or `moins_de_10_photos`. |
| `sha256` | SHA-256 hash of the image file. |
| `view` | Human view label: `head`, `body`, or `partial`. |
| `updated_at` | Annotation save timestamp; not the photograph's capture date. |

View labels use the following definitions:

- **`head`**: the head alone, or the head and neck without the trunk;
- **`body`**: the full animal is visible;
- **`partial`**: an incomplete body or another partial view.

One annotator labeled the complete collection. No independent inter-annotator agreement study was conducted. These labels were collected after the initial identification experiments and used for descriptive view analyses. They were not used to train the identity projections or select their checkpoints. The original reference galleries were constructed without these labels; the complementary cross-region analysis subsequently uses them to select head/body references.

Use `relative_path` and, where needed, `sha256` to align annotations with images. Do not equate `image_id` with the catalog indices in the experimental manifests. A manifest may identify a pony using the combined group and folder path.

## Audit and experimental partitions

All 1,549 files were readable. The audit detected no exact byte-level or decoded-pixel duplicates. Perceptual hashing identified three similar-image pairs; one image from each pair was excluded before constructing the experimental manifests. This procedure does not rule out all near-duplicates or shared capture sessions.

The reproducibility package associated with the paper provides five fixed manifests, `seed_42.json` through `seed_46.json`. Each separates the 115 main identities into:

- 70 training identities;
- 20 validation identities;
- 25 test identities.

The roles are disjoint within a partition but can change across partitions. The seven sparse identities are reserved as additional unknown queries and are excluded from fitting and calibration.

Five photographs per identity are reserved as references. One- and three-reference galleries are nested subsets of those five references. The remaining photographs form a fixed query set; unused reserved references are not recycled as queries. The manifests record the catalog, hashes, exclusions, and applicable gallery/query episodes. Use the recorded exclusions rather than removing new images independently when reproducing the reported results.

## Scope and limitations

The photographs vary in visible body region, side, framing, setting, and apparent developmental stage or coat appearance. Age, season, side, and capture sessions are not annotated. No usable EXIF capture dates were available for enforcing chronological or session-separated splits. The data do not include manually drawn segmentation masks, bounding boxes, or landmarks.

The collection comes from one breeding establishment. Reference and query photographs can share acquisition contexts. Accordingly, these data support an exploratory within-collection benchmark; aggregate accuracy does not establish generalization across new sites, sessions, ages, or seasons. Identity-disjoint adaptation also does not establish absence of these images or animals from the pretraining data of external models.

The resource is intended for research and human-assisted identification. Photographic matching alone does not certify administrative identity or ownership. Remote verification during inspections is a prospective application requiring separate task-specific validation.

## Permission for scientific use and attribution

The photographs are shared with the kind permission of **Élevage des Isles, Normandy, France, for use in scientific research**. The establishment supports their dissemination to help other researchers develop and evaluate methods for individual animal identification.

This permission covers dissemination of the collection and scientific use of the photographs. It does not specify a general-purpose open license or authorize uses beyond scientific research. For other uses, contact the dataset creators to clarify the applicable permissions with Élevage des Isles.

Users are requested to acknowledge Élevage des Isles and cite this dataset in publications resulting from its use.

Suggested acknowledgement:

> We thank Élevage des Isles, Normandy, France, for authorizing the dissemination and scientific use of the photographs in the Isles Pony Identification Dataset.

