# mypy_mypyc-wheels
Automated building and storage of mypyc-compiled mypy binaries

![Build wheels status](https://github.com/KotlinIsland/mypy_mypyc-wheels/workflows/Build%20wheels/badge.svg)

## Things to know

Typically, you'll want to report issues on the main mypy repo (not many people
watch this repo)

If you're running into weird issues with a pull request, try updating the
`mypy_commit` file to the latest hash from the mypy repo.

If wheels aren't getting built, debug over at
https://github.com/KotlinIsland/mypy_mypyc-wheels/actions

You can use pip to install these wheels like so:
```bash
pip install --upgrade --pre --find-links https://github.com/KotlinIsland/mypy_mypyc-wheels/releases/ basedmypy
# If you need a specific version, specify the url as follows
pip install --upgrade --pre --find-links https://github.com/KotlinIsland/mypy_mypyc-wheels/releases/expanded_assets/v1.6.0+dev.8e2443a74c9fb1726dc2c730b5e469881d3c1acf basedmypy
```

The above options may not work (and have broken in the past) since they depend on Github's HTML
and pip doing the correct thing. If you're looking for a relatively bulletproof solution,
navigate to the appropriate release page, manually select the wheel you wish to install and copy
the URL of the correct wheel:
```bash
pip install https://github.com/KotlinIsland/mypy_mypyc-wheels/releases/download/v1.6.0+dev.8e2443a74c9fb1726dc2c730b5e469881d3c1acf/basedmypy-1.6.0+dev.8e2443a74c9fb1726dc2c730b5e469881d3c1acf-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
```

##  Building locally

With [pipx](https://pipx.pypa.io) installed, run:

```bash
git clone https://github.com/KotlinIsland/basedmypy.git --recurse-submodules
git -C basedmypy checkout $(cat mypy_commit)
pipx run cibuildwheel --config=cibuildwheel.toml basedmypy
```

Either add `--only=<identifier>` to build only one wheel, or set `CIBW_BUILD`
to some expression like `cp311-*` and include `--platform linux` (or some other
platform). Optionally pin cibuildwheel to the version specified in
`.github/workflows/build.yml`.
