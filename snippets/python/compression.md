# .[[tar]].[[xz]] 
using the [[tarfile]] library
## Decompress

```python
from typing import Optional
from pathlib import Path
import tarfile

def extract_tarxz(
    infile:Path, 
    outfile:Optional[Path] = Path('.').resolve()
	):

    with tarfile.open(infile, 'r') as tf:  
        tf.extractall(outfile)
```