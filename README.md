# alzheimers-glymphatic-clearance
# Glymphatic Transport Impedance Predicts Cognitive Collapse

**Author:** Benjamin Goodluck Otuya
**Institution:** Department of Human Physiology, Ahmadu Bello University
**Publication Context:** Code repository for the manuscript: *Glymphatic transport impedance predicts cognitive collapse: A coupled fluidic evaluation of the Alzheimer's disease continuum.*

---

## 1. Overview
This repository contains the mathematical models and Python survival pipelines used to evaluate Alzheimer's disease progression as a failure of the brain's physical clearance architecture. Rather than treating cerebrospinal fluid (CSF) and peripheral plasma biomarkers in isolation, this pipeline models the blood-brain barrier (BBB) as a coupled fluidic system to derive a patient-specific glymphatic transport coefficient ($\kappa$).

## 2. The Physics of Glymphatic Impedance
Maintaining homeostatic clearance across a semi-permeable membrane requires a cooperative relationship between an active biological driver and a structurally intact physical boundary. We model this via a **"Pump and Pipes"** framework:
* **The Pump (sTREM2):** Active microglial phagocytosis pushing neurotoxic aggregates out of the parenchyma.
* **The Pipes (CLDN5):** Endothelial tight junctions sealing the brain capillaries to preserve the directional pressure gradient required for glymphatic bulk flow.

## 3. Mathematical Derivation of $\kappa$
Following the irreversible mass-transport formulations established by Kedem and Katchalsky, the net solute flux ($J_s$) across a membrane relies on the concentration gradient and active filtration rate. 

We define the transport coefficient ($\kappa_{Tau}$) as the log-transformed partition ratio of peripheral plasma p-tau217 to central CSF p-tau181. Because a healthy system actively clears tau into the periphery, a higher concentration in the plasma relative to the CSF indicates high clearance efficiency.

$$ \kappa_{Tau} = \ln \left( \frac{[Plasma\ p-tau217]}{[CSF\ p-tau181]} \right) $$

To construct a standardized comparative scale for the Cox proportional hazards model, these raw values are subsequently z-scored ($\kappa_{Tau,Z}$). A positive score indicates active clearance; a negative score indicates severe physical transport impedance (clogged central drains). 

Our piecewise bifurcation analysis isolated the critical clinical tipping point at exactly $\kappa_c = -0.004$, beyond which systemic failure triggers exponential cognitive decline.

## 4. ADNI Data Use & Reproducibility
To comply with the Alzheimer's Disease Neuroimaging Initiative (ADNI) Data Use Agreement, **no raw patient clinical or biofluid datasets are hosted in this repository.** 

To reproduce these survival models:
1. Apply for data access at [adni.loni.usc.edu](https://adni.loni.usc.edu/).
2. Download the matched UPENN CSF (Roche Elecsys) and Plasma (Quanterix Simoa) biomarker files, alongside the ADNIMERGE core clinical file.
3. Run the temporal alignment and data cleaning protocols outlined in `1_Data_Alignment.py`.
4. Execute the Cox proportional hazards and bifurcation algorithms in `2_Survival_Bifurcation.py`.
