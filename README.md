# Robot calibration pose coverage data

Measurement-level replication data and numerical reanalysis code for
*Pose coverage and held-out image validation for multi-camera robot calibration*.
The manuscript is unpublished; this repository does not imply journal acceptance.

Repository: https://github.com/jensenzhou47/robot-calibration-pose-coverage-data

## Contents and scope

Download `Industrial_Robot_measurement_replication_v1.zip` and extract it. The `measurement_replication/` directory contains:

| Item | Contents |
| --- | --- |
| `inputs/*.npz` | 64 camera-session panels with pose/frame membership, reconstructed corners, transforms and recorded camera parameters |
| `panels.json` | Panel metadata and target definitions |
| `expected_full_results.csv` | Reference numerical outcomes and failure information |
| `subset_membership_and_results.csv` | Saved subset membership and numerical outcomes |
| `reanalyse.py`, `code/` | Numerical reanalysis and original numerical core functions |
| `requirements.txt` | Pinned Python dependencies |
| `replication_results/` | Saved comparison results from the existing study |
| `SHA256SUMS`, `MANIFEST_SHA256.csv` | File integrity records |

The 64 panels comprise 36 main panels, 23 ancillary panels and five late-available
head captures, with 11,019 frame observations and 1,504,352 reconstructed corners.
Frames and corners are repeated measurements, not independent hardware trials.
The observations are reconstructed measurements, not true extrinsic reference
transforms. Pose grouping, validation membership and saved subsets are retained.

Direct device/network identifiers, source paths, host keys, original run names and
absolute acquisition timestamps are excluded. Original images and the detector
source remain in the private study archive; this package supports numerical
reanalysis and does not support raw-image redetection or external accuracy claims.

## Reproduce

Tested with Python 3.12.3 and the pinned dependencies in `requirements.txt`.
From the extracted `measurement_replication/` directory, run:

```sh
python -m pip install -r requirements.txt
python reanalyse.py --objectives
```

This checks the full-set Park, archived-Park, pose-refined and pixel-refined fits
and the saved ten-pose farthest subsets. A smaller check is `python reanalyse.py`.
To repeat all saved subsets as well as the objectives, run:

```sh
python reanalyse.py --all-subsets --objectives
```

The all-subset analysis takes longer. Results are written under
`measurement_replication/replication_results/`, replacing the bundled reference
copies in that extracted working directory. Keep the downloaded ZIP as an
unaltered reference. The analysis itself does not connect to any robot or network.

`frame_G` maps camera support to robot base and `frame_C` maps target to camera;
translations are in metres. `train_G/C` and `held_G/C` are pose-group means.
Object points are in metres and image points are in pixels. `corner_frame_index`
links corners to frames; recorded `K` and the five `D` coefficients are fixed.
Translation closure is reported in millimetres and rotation closure in degrees.
Pixel RMS weights frames within poses and poses within each split equally.
All fitting uses training observations only.

## Version and integrity

Version 1 republishes the existing round-5 measurement bundle with updated access
documentation and manifests. All 64 NPZ files, numerical code, panel metadata,
saved subsets and reference results are byte-identical to that existing bundle.
The journal plain-text supplementary files contain the same numerical observations.
Check the downloaded ZIP against the repository's `SHA256SUMS` before extraction.

## Citation and permissions

Please identify this dataset by the manuscript title above, repository URL and
the exact commit used. No DOI has been assigned. No additional redistribution
licence is granted here; the author retains rights and may specify a licence
separately. Third-party software remains subject to its own terms and method
citations are provided in the manuscript.
