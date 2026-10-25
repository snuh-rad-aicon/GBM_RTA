# Multiparametric MRI Tumor Habitats and Telomerase Activity in Glioblastoma

Research code accompanying:

**Tumor habitat analysis using multiparametric MRI as a noninvasive correlate of longitudinal changes in telomerase activity in recurrent IDH-wildtype glioblastoma**

Seong Yun Jeong, Junhyeok Lee, Yunseo Choi, Minseo Choi, Hyeon Jong Yu, Hye Jin Kim, Chongwon Pae, Seung Hong Choi, Sung-Hye Park, Chul-Kee Park, and Kyu Sung Choi.

*Scientific Reports*. 2026;16:16051. Published April 3, 2026.

[Article](https://doi.org/10.1038/s41598-026-47185-3) · [PubMed](https://pubmed.ncbi.nlm.nih.gov/41933148/) · [Full text](https://pmc.ncbi.nlm.nih.gov/articles/PMC13199401/)

## Overview

This repository accompanies a study examining MRI correlates of telomerase activity at diagnosis and recurrence in 20 patients with IDH-wildtype glioblastoma. Tissue telomerase activity was measured using a TRAP assay. Paired habitat-volume analyses included 19 patients with available recurrence perfusion imaging.

The study integrates diffusion and perfusion MRI, tumor habitat mapping, radiomics, and survival analysis. Its findings are exploratory associations and require independent validation.

## Analysis framework

Population-level k-means clustering of normalized apparent diffusion coefficient (ADC) and relative cerebral blood volume (rCBV) values defines three habitats:

| Habitat | ADC | rCBV |
| --- | --- | --- |
| Hypovascular cellular | Low | Low |
| Hypervascular cellular | Low | High |
| Nonviable | High | Low |

Habitat volumes are evaluated within contrast-enhancing (CE) and non-enhancing (NE) regions. NE masks encompass surrounding T2/FLAIR hyperintensity and may contain both infiltrative tumor and edema. Habitat names represent imaging-based physiological interpretations.

Radiomics uses ADC, rCBV, contrast-enhanced T1-weighted, and FLAIR images, with a bin width of 5. Analyses assess associations with longitudinal telomerase activity, tumor-volume changes, and progression-free survival.

## Software used in the publication

| Component | Software |
| --- | --- |
| Clustering | scikit-learn 1.6.0 |
| Radiomics | PyRadiomics 3.0.1 |
| Survival analysis | lifelines 0.30.0 |
| Statistical analysis | statsmodels 0.14.4; SciPy 1.14.1 |
| ROC analysis in R | pROC 1.18.5 |
| Image processing | FSL; SynthStrip; Nordic ICE |

These are publication-reported tools, rather than a verified installation specification for this code release. Consult the article for preprocessing and statistical methods.

## Main notebook

The main analysis notebook is `GBM_RTA_main_upload.ipynb`.

## Installation and usage

The notebook imports pandas, NumPy, SciPy, statsmodels, scikit-learn, seaborn, matplotlib, tqdm, ANTsPy (`antspyx`), and lifelines. Reading XLSX files requires an Excel engine such as openpyxl. Use Jupyter with a Python kernel. These dependencies were identified from imports; the environment has not been tested.

FSL's `fslstats` executable must be on `PATH`. MRI preprocessing and PyRadiomics extraction are upstream steps; this notebook reads prepared images and radiomics CSV files.

1. Set `GBM_RTA_ROOT` to your authorized private data directory.
2. Supply `excel_csv/clinical_metadata.xlsx` beneath that root. Adapt the Korean workbook column mapping to your approved de-identified schema.
3. Supply images under `data/only_initial/<study_code>/1/` (initial) and `2/` (recurrence). Use consistent numeric study codes instead of medical record numbers; the analysis converts indices to integers.
4. Supply radiomics CSV files at the `rad_root` path specified in the notebook.
5. Open `GBM_RTA_main_upload.ipynb` in Jupyter and review cells before sequential execution.

Each time point expects `flair_vox.nii.gz`, `rCBV_vox.nii.gz`, `adc_vox.nii.gz`, `t1ce_vox.nii.gz`, corresponding `_rad.nii.gz` maps, and `NE_tumor_mask.nii.gz`, `CE_tumor_mask.nii.gz`, and `WT_tumor_mask.nii.gz`. Clinical fields cover study code, demographics, TA1/TA2, RTA group, molecular markers, treatment/resection variables, survival durations, and event status.

The public copy omits saved outputs and the hardcoded individual-case visualization. It has not been run against the unavailable private inputs; numerical correctness and agreement with the publication have not been independently validated.

## Data availability

The study XLSX files and participant-level clinical data are not included in this repository to protect patient confidentiality. Running analyses that depend on these files requires separately authorized data access and the corresponding input schema. The notebook alone does not reproduce the study results without those inputs.

Before publishing a notebook, clear all saved outputs, execution counts, embedded attachments, and unnecessary metadata, and review source cells for patient identifiers, dates, private file paths, and credentials. Excluding XLSX files alone does not establish that a notebook is de-identified.

## Citation

Please cite the accompanying publication when using this work:

```bibtex
@article{Jeong2026TumorHabitat,
  author = {Jeong, Seong Yun and Lee, Junhyeok and Choi, Yunseo and Choi, Minseo and Yu, Hyeon Jong and Kim, Hye Jin and Pae, Chongwon and Choi, Seung Hong and Park, Sung-Hye and Park, Chul-Kee and Choi, Kyu Sung},
  title = {Tumor habitat analysis using multiparametric MRI as a noninvasive correlate of longitudinal changes in telomerase activity in recurrent {IDH}-wildtype glioblastoma},
  journal = {Scientific Reports},
  year = {2026},
  volume = {16},
  pages = {16051},
  doi = {10.1038/s41598-026-47185-3},
  url = {https://doi.org/10.1038/s41598-026-47185-3}
}
```

## License

<!-- Add a code LICENSE file and identify its terms here before release. The publication's license does not automatically determine the code license. -->

The software license will be specified in this repository's LICENSE file.

## Contact

For scientific correspondence, please contact **Kyu Sung Choi** or **Chul-Kee Park** through the contact details provided in the publication.

For research use only.
