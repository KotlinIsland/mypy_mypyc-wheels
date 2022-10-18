# mypy_mypyc-wheels
Automated building and storage of mypyc-compiled mypy binaries

![Build wheels status](https://github.com/mypyc/mypy_mypyc-wheels/workflows/Build%20wheels/badge.svg)

## Things to know

Typically, you'll want to report issues on the main mypy repo (not many people
watch this repo)

If you're running into weird issues with a pull request, try updating the
`mypy_commit` file to the latest hash from the mypy repo.

If wheels aren't getting built, debug over at
https://github.com/mypyc/mypy_mypyc-wheels/actions

You can use pip to install from the latest set of wheels like so:
```bash
pip install --upgrade --find-links https://github.com/mypyc/mypy_mypyc-wheels/releases mypy
```
If you need a specific version then you will likely have to manually download the wheel file you wish to install, then
install using pip like so:
```bash
pip install mypy-0.990+dev.d528bf2e79cf263653b9a6e70e80ce8a033cc01a-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
```

##  Building locally

With [pipx](https://pipx.pypa.io) installed, run:

```bash
COMMIT=$(cat mypy_commit)
git clone https://github.com/python/mypy.git --recurse-submodules
(cd mypy && git checkout $COMMIT)
pipx run cibuildwheel --config=cibuildwheel.toml mypy
```

Optionally add `--only=<identifier>` to build only one wheel, or set
`CIBW_BUILD` to some expression like `cp311-*` and include `--platform linux`
(or some other platform). Optionally pin cibuildwheel to the version specified
in `.github/workflows/build.yml`.
