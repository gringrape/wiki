## pipenv
```bash
pip3 install pipenv
```

## create project
```bash
pipenv --python {version}
```

## install packages
```bash
cd {project}
pipenv install fastapi
pipenv install uvicorn
```

## start server
```python
# main.py
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return "Hello, World!"
```

```bash
uvicorn main:app --reload
```




