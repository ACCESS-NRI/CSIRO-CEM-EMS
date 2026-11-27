![Dynamic YAML Badge](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fgithub.com%2FACCESS-NRI%2CSIRO-CEM-EMS%2Fraw%2Fmain%2Fspack.yaml&query=%24.spack.repos.access_spack_packages.tag&label=ACCESS-NRI%2Faccess-spack-packages) ![Dynamic YAML Badge](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fgithub.com%2FACCESS-NRI%2FCSIRO-CEM-EMS%2Fraw%2Fmain%2Fspack.yaml&query=%24.spack.definitions%5B*%5D._spack-version%5B0%5D&label=ACCESS-NRI%2Fspack) ![Dynamic JSON Badge](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fgithub.com%2FACCESS-NRI%2Fbuild-cd%2Fraw%2FHEAD%2Fconfig%2Fsettings.json&query=%24.deployment.Gadi.Release.%5B'1.1'%5D.spack-config&label=ACCESS-NRI%2Fspack-config%20(Gadi))

# EMS

## Features
* Hydrodynamic models for [structured](model/hd) and [unstructured](model/hd-us) grids
* [Sediment transport, resuspension and deposition](model/lib/sediments)
* [Spectrally-resolved semi-empirical optical model](model/lib/ecology)
* [Biogeochemical (nutrients, plankton, carbon chemistry) and benthic (seagrass, corals) processes](model/lib/ecology)

## Background
The CSIRO Coastal Environmental Modelling (CEM) team develops, maintains and uses the EMS software that allows investigation of the physical, sediment and biogeochemical processes in marine environments. This is achieved by a ‘driver’ hydrodynamic code into which are linked various libraries to perform sediment transport and biogeochemistry, all supported by a core library. The ‘driver’ may be any model that manages the tracers required for sediments and biogeochemistry. The sediment and biogeochemical libraries are stand-alone modules that are linked to the driver via an interface, and in principle may be linked to any hydrodynamic code. Currently the ‘drivers’ available are a full hydrodynamic mode, a transport model that uses offline data to advect and diffuse sediment /  biogeochemical variables, and a box model. The hydrodynamic code may further operate in reduced dimensions of 1D, 2D vertically averaged or 2D laterally averaged. A waves and tracer statistic library also exist; the latter allowing various operations to be performed during run-time on any tracers supported by the driver (e.g. means, fluxes, vertical integrals).

Additional software exists to generate the complex orthogonal curvilinear grids that are typically used for case studies. These grids allow variable resolution over the domain, useful for representing areas of interest with high resolution and less critical regions with coarser resolution. The curvilinear grid may also allow a dimensionality to be reduced from 3-D to 2-D within the same grid. This is useful when representing rivers or narrow estuaries, since the cross-river coordinate becomes very small in these areas and therefore becomes the defining grid size for setting the model time-step. Eliminating these small grid cells by making rivers or estuaries 2-D laterally averaged allows larger time-steps, hence a faster model. The curvilinear grids require dedicated software for visualizisation of model output, and the CEM supports several visualisation platforms to archive this. These software packages allow publication quality images and animations to be produced, and allow exploration of the data in 4 dimensions for analysis purposes.

See [more EMS info on the CEM website](https://research.csiro.au/cem/software/ems/)

## Documentation
Manuals for all modules [are available from this link](https://research.csiro.au/cem/software/ems/ems-documentation/)

## User registration
We strongly encourage all users of EMS to register their details with our group.

Please [use this form to do so](https://research.csiro.au/cem/software/ems/ems-user-registration/)

## Build

ACCESS-NRI is supporting the deployment of the EMS modelling suite for the community as part of the CoastRI NCRIS project. 

ACCESS-NRI uses [spack](https://spack.io), a build from source package manager designed for use with high performance computing.

Spack automatically builds all the components and their dependencies, producing model component executables. Spack already contains support for compiling thousands of common software packages. Spack packages for the components are defined in the [spack packages repository](https://github.com/ACCESS-NRI/spack_packages/).

This deployment of EMS is built and deployed automatically to `gadi` on NCI (see below). However it is possible to use spack to compile the model using the `spack.yaml` environment file in this repository. To do so follow the [instructions on for configuring spack on `gadi`](https://access-hive.org.au/getting_started/spack/).

Then clone this repository and run the following commands on `gadi`:

```bash
spack env create ems spack.yaml
spack env activate ems
spack install
```

to create a spack environment called `ems` and build all the components, the locations of which can be found using `spack find --paths`.

## Deployment

CSIRO-CEM-EMS is deployed automatically when a new version of the [`spack.yaml`](./spack.yaml) file is committed to `main` or a dedicated `backport/VERSION` branch. All the components are built using `spack` on `gadi` and installed under the [`vk83`](https://my.nci.org.au/mancini/project/vk83) project in `/g/data/vk83`. It is necessary to be a member of [`vk83`](https://my.nci.org.au/mancini/project/vk83) project to use ACCESS-NRI deployments of CSIRO-CEM-EMS.

The deployment process also creates a GitHub release with the same tag. All releases are available under the [Releases page](https://github.com/ACCESS-NRI/CSIRO-CEM-EMS/releases). Each release has a changelog and meta-data with detailed information about the build and deployment, including:

- paths on `gadi` to all executables built in the deployment process (`spack.location`)
- a `spack.lock` file, which is a complete build provenance document, listing all the components that were built and their dependencies, versions, compiler version, build flags and build architecture. It is also installable via spack similarly to the `spack.yaml`. 
- the environment `spack.yaml` file used for deployment

Additionally the deployment creates environment modulefiles, the [standard method for deploying software on `gadi`](https://opus.nci.org.au/display/Help/Environment+Modules). To view available CSIRO-CEM-EMS versions:

```bash
module use /g/data/vk83/modules
module avail csiro-cem-ems
```

For information on contributing your own fixes to the CSIRO-CEM-EMS `spack.yaml`, see the [Hive Docs article](https://docs.access-hive.org.au/models/run-a-model/create-a-prerelease/) on creating a prerelease.


## Running the tests

There are many tests available for each module. See [model/tests](model/tests) for a complete list.

## Authors

EMS is wrtten and maintained by the [Coastal Environmental Modelling team](https://research.csiro.au/cem/people/)

See also the list of [contributors](CONTRIBUTORS.md) who participated in this project.

## License

This project is licensed under the CSIRO open-source License - see the [LICENSE.md](LICENSE.md) file for details

## Website

Further information about the CSIRO CEM Team may be found by [visiting our website](https://research.csiro.au/cem).

## Contributing
Please contact us on ems@csiro.au for details

