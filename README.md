# Sarek pipeline orchestration for the GOAL Consortium

This repository contains documentation and scripts to help clinical labs deploy the [nf-core Sarek pipeline](https://nf-co.re/sarek).

## Quick Start

If you don't have `nextflow` and `singularity`, see section below. If you do, use them to test Sarek on its included test data:
```bash
nextflow run -bg -profile test,singularity -work-dir nf_work -revision 2.7.1 nf-core/sarek --tools Mutect2 --outdir test_results
```

## Install Nextflow and Singularity

[mamba](https://github.com/mamba-org/mamba) is a fast alternative to [conda](https://docs.conda.io), a package manager that can download and install specific versions of software in isolated environments, very useful in data-science projects. `mambaforge` is a variant of [miniforge](https://github.com/conda-forge/miniforge) that installs `mamba` configured with [conda-forge](https://conda-forge.org/) as the default source of packaged software.

These instructions show you how to install `mamba`, and then use it to install [nextflow](https://www.nextflow.io/) and [singularity](https://sylabs.io/singularity) for executing popular bioinformatics pipelines. Unfortunately, `singularity` is not available on Windows or macOS. So, this guide will only target Linux environments. If you have to use Windows 10, then try [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10). If you have to use macOS, then try a [Virtual Machine](https://sylabs.io/guides/3.0/user-guide/installation.html#singularity-vagrant-box).

Download the `mambaforge` installer for Linux environments:
```bash
curl -L https://github.com/conda-forge/miniforge/releases/download/4.10.3-7/Mambaforge-Linux-x86_64.sh -o mambaforge.sh
```

Install `mamba` into a folder named `mambaforge` under your home directory, and delete the installer:
```bash
sh mambaforge.sh -bfp $HOME/mambaforge && rm -f mambaforge.sh
```

Add the following to your `~/.bashrc` file to activate the base environment whenever you login:
```bash
# Add mambaforge to PATH if found, and load the base environment
if [ -f "$HOME/mambaforge/etc/profile.d/conda.sh" ]; then
    . $HOME/mambaforge/etc/profile.d/conda.sh
    conda activate
fi
```

Logout and login to activate the base environment, install necessary packages, and cleanup cached packages:
```bash
mamba install -y -c bioconda git==2.33.1 openjdk==11.0.8 nextflow==21.10.0 singularity==3.8.4
mamba clean -ay
```
