# mambax (work in progress)

## Initial discussion thread

https://github.com/mamba-org/mamba/issues/1707

## Concept

[pipx](https://github.com/pypa/pipx) is a Python tool which transparently sets up a venv dedicated to running the Python console scripts of a particular Python package (especially from PyPI).

[condax](https://github.com/mariusvniekerk/condax) is a Python tool which transparently sets up a Conda env dedicated to running the executables of a particular Conda package.

mambax would be like condax, but without Python and instead leveraging Micromamba (possibly downloading and installing it in case it's not already installed), thus remaining lightweight and avoiding the Python dependency. The killer feature: this would turn Conda-Forge into a general software repository suitable for lightweight Python-free package deployments, usable by people with no knowledge of or interest in Conda environments.

The particular use case which sparked this idea is [s3fs-fuse](https://github.com/conda-forge/s3fs-fuse-feedstock) which I have been building for myself and others as a Debian package (see [Motivation and Alternatives](https://github.com/maresb/docker-build-s3fs#motivation)) since before I got involved with Conda-Forge. I feel like Conda-Forge should in theory be able to replace my work to build this Debian package, but what got me thinking more seriously in this direction was [this comment](https://github.com/maresb/docker-build-s3fs/issues/8#issuecomment-1137061651) I received:

> I read your way to install it through mamba, but as a non-conda/mamba user, it just feel so much easier to just install a deb package...
>
> Thanks for your time anyway

For the generic person who simply wants to install some particular program, they aren't going to want to be bothered (at least at first) with setting up a Conda environment. For such potential users, it could be as simple as

```bash
wget https://.../mambax
./mambax install whatever
```

Such a simple workflow would hopefully make adoption easy. I could envision that open-source developers of non-Python packages could use Conda-Forge + mambax as their primary method for distributing their binaries, similarly to how Micromamba is currently being built and distributed, but allowing for non-static binaries with dependencies.
