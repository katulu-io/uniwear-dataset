# Katulu Uniwear Dataset

![](./assets/uniwear_all_experiments.png)

A [tidy dataset](https://vita.had.co.nz/papers/tidy-data.pdf) for multi-material
tool wear, suitable for prognostic modeling.

As part of condition monitoring and predictive maintenance solutions, the
challenge in tool wear is focused on being able to predict the current wear and
forecast the remaining useful life.

A model for such solutions should be able to work for multiple tool types
and workpiece materials. This could be in an online setting whereby the model
is trained as data arrives or an offline setting where historical recordings are
used to build a model.

In this direction, the need for a multi-material dataset, both tool,
and workpiece, is required to develop robust
models. To fulfill this purpose, we prepare and merge two public
milling datasets for easy use in machine learning tasks,
downsampled and smoothed.

## Data Bundles

Under the `data` directory, you find the following data bundles:

- NUAA: `nuaa_orthogonal_bundle_high_resolution.csv` : ~15 Hz smoothed bundle of NUAA orthogonal experiments.
- PHM2010: `phm2010_bundle_high_resolution.csv` : ~25 Hz smoothed bundle of NUAA orthogonal experiments.
- Uniwear: `uniwear.csv` : ~2 Hz aligned intersection of nuaa & phm2010.

### NUAA

The tool wear dataset comes from NUAA Ideahouse, released on
[IEEE's dataport](https://ieee-dataport.org/open-access/tool-wear-dataset-nuaaideahouse).

Orthogonal experiments are part of the dataset that contains different variations: 3 factors and 3 levels (`W1-W9`), with the following parameters/factors fixed per experiment :

- `fz` feed per tooth (mm/rev) (`feed_per_tooth` ) `[0.045, 0.05, 0.055]`
- `n` spindle speed (rev/min) (`spindle_speed` ) `[1750, 1800, 1850]`

We only bundle these so-called orthogonal experiments. Experiments use titanium workpiece (TC4) and solid carbide cutting tool
(such as Tungsten carbide).

`data/nuaa_orthogonal_bundle_high_resolution.csv` contains 9 experiments with raw data sampled at ~15 Hz. This is still downsampled from the original dataset but high resolution compare to extracted features in uniwear (see Uniwear dataset). We distinguish experiments with `experiment_tag` column.

Apart from `timestamp` in seconds and `tool_wear` in mm, the following signals
appear in the dataset, column names as follows :

- axial_force
- bending_moment_x
- bending_moment_y
- torsion
- vibration1
- vibration2
- spindle_power
- spindle_current
- vibration_x
- vibration_y
- force_z

Experiment fixed variations are also given in the data set for information, column names are as follows:

- feed_per_tooth
- spindle_speed
- axial_cutting_depth

Experiment and dataset tags are also provided.

- experiment_tag
- dataset_tag

### PHM2010

[PHM2010](https://phmsociety.org/phm_competition/2010-phm-society-conference-data-challenge/)
was a data challenge given by PHM society in 2010. We bundle 3 of the cutting
experiments c1, c4, and c6. Stainless steel (HRC52) workpiece is used
with the cutting tool being tungsten carbide. Release in [IEEE dataport](https://ieee-dataport.org/documents/2010-phm-society-conference-data-challenge) as well. Sensor signals.

- force_x
- force_y
- force_z
- vibration_x
- vibration_y
- vibration_z
- acoustic_emission_rms

Dataset is distinguised with 'dataset_tag', here is 'phm2010'.

### Uniwear

We have merged two datasets NUAA (`W1`-`W9` recordings) and
PHM2010 (`c1`, `c4`, and `c6` recordings) and align their timestamps,
i.e., ~2 Hz sampling and smoothed. We use overlapping signal types
on the following columns:

- force_x
- force_y
- force_z
- vibration_x
- vibration_y
- vibration_z

Label column is `tool_wear` in `mm`.

Other important columns

- timestamp : seconds since cutting.
- dataset_tag : nuaa or phm2010.
- experiment_tag : W1-W9, c1, c4, c6.

## Directories

- [data](data): Contains all bundled datasets.
- [notebooks](notebooks) : Python notebook for plotting.

## License

The bundled datasets are licensed under [Creative Commons Attribution 4.0 International License ![License: CC BY 4.0](https://i.creativecommons.org/l/by/4.0/80x15.png)](https://creativecommons.org/licenses/by/4.0/).
The rest is licensed under [GPLv3](LICENSE).
