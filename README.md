# Dataset organization

Data for this project are stored in a database of plain text files organized as follows:
- The database root contains the following:
    - Folders for each project, named according to `project_code`
    - `species.csvy` -- Information about species
    - `instruments.yml` -- Information about instruments
    - `traits.yml` -- Information about traits and units
- Each project folder contains the following:
    - `metadata.csvy` -- Metadata about the spectra, which contains the following:
        * A YAML header with the following metadata (`*` indicates required data):
        * CSV data with the following columns (again, `*` indicates required columns):
            - `*observation_id`
            - `*year`
            - `*site_code`
            - `*plot_code`
            - `canopy_position` -- Relative position in canopy. Bottom (B), Middle (M), or Top (T)
            - `sun_shade` -- Whether leaves are sunlit (sun) or shaded (shade)
            - `needle_old_new` -- Whether needles are old (O) or new (new)
            - `needle_age` -- Needle age, in years
            - `sample_prep` -- Whether the sample is on a fresh leaf, dry leaf, or powder
    - `spectra/` -- Directory containing spectra
- Each `spectra` folder contains `<observation_id>.csvy` files
    - Each `observation_id` corresponds to observations made on a single leaf at a particular point in time, so each spectra within a file is treated as a single observation in the context of PROSPECT inversion.
    - The `spectra_type` field indicates the type of spectra; one of:
        * `R` - Reflectance
        * `T` - Transmittance
        * `PA` - Pseudo-absorbance (log10(1/R))
        * `CRR` - Continuum-removed reflectance
    - The data itself is CSV with a `wavelengths` column of wavelengths and remaining column names corresponding to observation IDs (which should all be the same)
