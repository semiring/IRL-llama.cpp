This is an appalling hack of llama.cpp to see if we can create in situ Frankenmerges at the computation graph building level. 

Layers are specifed in the environment variable $LLAMA_CHUNKS as a string of floats of the form:
"first_chunk_begin, first_chunk_end, 2nd_chunk_begin, 2nd_chunk_end, ..."; 

e.g.,

```
export LLAMA_CHUNKS="0.0,0.6,0.2,0.8,0.6,1.0"
```

creates a Frankenmodel that has the first 60% of the model layers, followed by a block starting
at the layer 20% through, and ending at the layer 80% of the way through, and then a final block
from 60% to 100%.

Note layers are always addressed as a fraction of the number of layers in the model (0.0 - 1.0).
