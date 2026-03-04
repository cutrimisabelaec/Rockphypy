# Rockphypy - Rock Physics Screening from Well Logs (Colab)

This repository contains a **Google Colab** workflow that uses **Rockphypy** to perform **rock physics screening** (Vp vs porosity trends and elastic bounds) from **LAS well log data**. The workflow follows the Rockphypy *rock physics screening* example and adapts it to log-derived inputs (Vp, porosity, Vsh).

---

## What this code does

1. Mounts Google Drive in Colab and accesses a `.las` file
2. Converts LAS curves to a `pandas.DataFrame`
3. Computes basic petrophysical estimates from logs:
   - **Density porosity** (`PHI_DENS`) from `RHOB`
   - **Total porosity estimate** (`PHIT_ND`) as the average of `PHI_DENS` and `NPHI`
   - **Shale volume from GR** (`VSH_GR`) is computed from GR using the linear GR index `Vsh = (GR - GR_sand) / (GR_shale - GR_sand)`, where `GR_sand` is the clean-sand baseline and `GR_shale` is the shale baseline.
4. Computes **Vp (m/s)** from sonic **DT** using the DT unit stored in the LAS
5. Uses `rockphypy.QI` to:
   - Compute **elastic screening bounds** with `QI.screening(...)`
   - Create a `QI` object from log-derived **Vp**, **phi**, and **Vsh**
   - Plot the screening template and data with `screening_plot(...)`

---

## Input data requirements (LAS curves)

Your LAS should contain (names can vary depending on the dataset):

* `RHOB` - Bulk density (g/cm³)
* `NPHI` - Neutron porosity (v/v)
* `GR` - Gamma Ray (API)
* `DT` (usually µs/ft)

> If the sonic curve is not `DT` (e.g., `DTC` / `DTCO`), you may need to adjust the code that reads the unit and computes Vp.

---

## Outputs

* Screening template (elastic bounds) and measured data points:

  * **Vp vs porosity** screening plot with points colored by sand volume (Vsand = 1 - Vsh).
    
    
<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/6085e099-34ed-4366-afb9-a92870c8a4a1" />

---

 ## Requirements

- Python 3
- Libraries:
  - `rockphypy`
  - `lasio`
  - `numpy`
  - `pandas`
  - `matplotlib`

---

**REFERENCES**

Avseth, P., Lehocki, I., Kjøsnes, Ø., & Sandstad, O. (2021). Data‐driven rock physics analysis of North Sea tertiary reservoir sands. Geophysical Prospecting, 69(3), 608-621.

https://rockphypy.readthedocs.io/en/latest/advanced_examples/rock_physics_screening.html#sphx-glr-advanced-examples-rock-physics-screening-py

---

BENEDICTUS, T. Determination of Petrophysical Properties from Well Logs of the Offshore Terschelling Basin and Southern Central North Sea Graben Region (Ncp-2a) of the Netherlands. TNO report, 2007.

---

FANCHI, J, R. Integrated Reservoir Asset Management Principles and Best Practices. Gulf Professional Publishing, 2010. https://doi.org/10.1016/B978-0-12-382088-4.00007-4.

---

NOUPA, R. K. et al. Well Log Lithological Analysis and Petrophysical Parameters Calculation of Miocene to Recent Formation Reservoirs in Well P10, Offshore, Northern Rio Del Rey Basin (Southwest Cameroon, Gulf of Guinea). Earth Science Research, 2022.

---


RIDER, M. The Geological Interpretation of Well Logs. Rider-French Consulting, 2002.
