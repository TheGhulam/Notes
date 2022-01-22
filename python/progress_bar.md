# tqdm	

### Setup
```python
pip install tqdm
pip install ipywidgets
jupyter nbextension enable --py widgetsnbextension
jupyter labextension install @jupyter-widgets/jupyterlab-manager

# To activate tqdm in a notebook, add a cell with:
%%capture
from tqdm import tqdm_notebook as tqdm
tqdm().pandas()
```

### Using tqdm
You can get a progress bar for any iterable by wrapping it with tqdm(). For example,

```python
my_list = list(range(100))
for x in tqdm(my_list):
    pass
```
will give you a (very fast) progress bar. You also use tqdm more explicitly,

```python
my_list = list(range(100))
with tqdm(total=len(my_list)) as pbar:
    for x in my_list:
        pbar.update(1)
```
There’s also a pandas integration,

```python
df.progress_apply(lambda x: pass)
```
For more on using tqdm, including things like nested progress bars, check out their [documentation](https://github.com/tqdm/tqdm).
