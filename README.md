# Liver_beam_path

Title: Liver VMAT Arc Range Optimizer (DICOM RT Structure)

Repository layout

content: Put your sample RT Structure Set DICOM here (e.g., RSphantom.dcm﻿).

Beam_arrange_for_Liver.ipynb: Main notebook implementing ROI extraction, 2D intersection geometry, angle-interval merging, arc-range evaluation, and visualization.

Requirements

Python 3.x

Packages: numpy, pandas, matplotlib, scipy, pydicom

Input: An RT Structure Set DICOM containing named ROIs for PTV, External (or BODY), and Liver.

Quick start

Place your RT Structure Set DICOM under content and note its filename (e.g., RSphantom.dcm﻿).

Open Beam_arrange_for_Liver.ipynb and set the DICOM read path to your file, e.g., "content/RSphantom.dcm"﻿.

Optionally define organ_forbidden to exclude case-specific angle intervals (e.g., [{"SpinalCord": (125, 150)﻿, "Stomach": [(0, 50)]}]).

Adjust rotation_ranges (e.g., [translate:]) and min_arc_length, then run all cells to compute candidate arcs and generate angle–distance plots.

Using your own DICOM (ROI names)

Specify exact ROI names exactly as they appear in the Structure Set:

PTV ROI name: PTV﻿, or a clinic-specific label such as PTV1﻿, PTV2﻿, etc.

External body ROI name: External﻿ (or BODY﻿, depending on your TPS).

Liver ROI name: Liver﻿ (e.g., Liver﻿ or Liver_Whole﻿, depending on your clinic).

If your case uses multiple targets:

You can switch from PTV1﻿ to PTV2﻿ by setting the PTV selector variable (or the ROI name parameter) to "PTV2"﻿ without other code changes.

The algorithm accepts any PTV label as long as it matches the ROIName string in your DICOM.

Example edits in the notebook

DICOM path: set to your file under content, e.g., "content/RSphantom.dcm"﻿.

ROI verification: use the provided snippet to print available ROI names before optimization and confirm that PTV1﻿ or PTV2﻿, Liver﻿, and External﻿/BODY﻿ exist.

Forbidden angles: populate organ_forbidden with clinic-specific intervals, e.g., [{"Collision": (50, 125)﻿, "Kidney_R": [(90, 170)], "Kidney_L": [(90, 170)]}].

Key parameters

min_arc_length: minimum continuous arc length in degrees (default 30).

max_external_distance, max_liver_distance: distance thresholds (mm) for filtering angles; relax in small steps if no valid arc is found.

rotation_ranges: candidate sweep angles (e.g., [translate:]).

Outputs

Console summary of minimum and average projected distances from the PTV center to Liver and External across gantry angles.

A ranked table of candidate rotation ranges with the best start/end angles and mean liver distance.

Plots of angle–distance profiles and a matrix view of chosen arcs across rotation ranges.

Troubleshooting

“Structure not found” or similar: print the available ROI names and ensure exact string matches for PTV﻿/PTV1﻿/PTV2﻿, External﻿/BODY﻿, and Liver﻿.

No valid arc: reduce the coverage of organ_forbidden, or relax max_external_distance and/or max_liver_distance incrementally, then re-run.

License and citation

Include your preferred open-source license.

If publishing academically, consider citing your repository and describing the ROI extraction, 2D intersection method, angle-interval merging, and arc optimization procedure.

Short English note to include prominently

Place a sample DICOM RT Structure Set under the content folder.

If you bring your own DICOM, specify the exact ROI names: use PTV﻿ (or PTV1﻿/PTV2﻿), External﻿ (or BODY﻿), and Liver﻿.

Switching targets is supported: you can set the PTV ROI name to "PTV2"﻿ instead of "PTV1"﻿ when needed.
