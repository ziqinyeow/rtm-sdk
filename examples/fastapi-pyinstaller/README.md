# FastAPI + Juxtapose to .exe using Pyinstaller

## How to compile the sidecar

```bash
git clone https://github.com/ziqinyeow/juxtapose
cd juxtapose
pip install .
pip install uninstall juxtapose ultralytics yapf
pip install pyinstaller fastapi uvicorn[standard] python-multipart juxtematics

# mac
pyinstaller -c -F --clean --name sidecar --specpath dist --distpath dist examples/fastapi-pyinstaller/server.py

# windows
pyinstaller -c -F --clean --hidden-import=cv2 --hidden-import=supervision --hidden-import=addict --hidden-import=chex --hidden-import=lap --hidden-import=optax --hidden-import=einshape --hidden-import=haiku --hidden-import=mediapy --name sidecar --specpath dist --distpath dist examples/fastapi-pyinstaller/server.py
```

## How to run the exe

Double click or run terminal `./dist/sidecar`.

<div align="center">
  <p>
    <a align="center" href="" target="_blank">
      <img
        width="850"
        src="https://raw.githubusercontent.com/ziqinyeow/juxtapose/main/asset/fastapi-pyinstaller-demo.png"
      >
    </a>
  </p>
</div>

It takes some time to load, open for PR to optimize this with `pyinstaller --one dir` or `cython`.

## Reason to git clone ultralytics & yapf

Once compiled using pyinstaller to `.exe` file, you will defo face error of couldn't import files.

1. ultralytics - DEFAULT.yaml file - to resolve this (modify in [utils file](./ultralytics//utils/__init__.py)) to self import the yaml.
2. yapf - GRAMMAR.txt and PATTERNGRAMMAR.txt - to resolve this (modify in [grammar file](./yapf_third_party/_ylib2to3//pgen2/grammar.py)) to self import the grammar txt file.