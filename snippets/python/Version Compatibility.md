# Specific Imports

## [[Typing]]

using [[typing-extensions]]

### Literal

```python
import sys
if sys.version_info.minor >= 8:  
    from typing import Literal  
else:  
    from typing_extensions import Literal
```