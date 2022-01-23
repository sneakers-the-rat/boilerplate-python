And general web interaction


# Downloading Files

## With [[requests]] and [[tqdm]]
[reference](https://gist.github.com/yanqd0/c13ed29e29432e3cf3e7c38467f42f51)

```python
import requests  
from pathlib import Path  
from tqdm import tqdm

def download(url:str, file_name:typing.Union[Path,str]) -> bool:
    """
    Download a file with a progress bar

    Returns:
        bool: ``True`` if nothing happened and its probs good, ``False`` otherwise

    References:
        https://gist.github.com/yanqd0/c13ed29e29432e3cf3e7c38467f42f51
    """
    try:
        response = requests.get(url, stream=True)
        size = int(response.headers.get('content-length', 0))
        with open(file_name, 'wb') as ofile, tqdm(
                    desc=file_name,
                    total=size,
                    unit='iB',
                    unit_scale=True,
                    unit_divisor=1024,
                ) as pbar:
            for data in response.iter_content(chunk_size=1024):
                size = ofile.write(data)
                pbar.update(size)
        return True
    except:
        return False
```

