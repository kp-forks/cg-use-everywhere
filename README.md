# UE Nodes

UE nodes are "Use Everywhere". Put a UE node into your workflow, connect its input, and every node with an unconnected input of the same type will act as if connected to it. 

CLIP, IMAGE, MODEL, VAE, or LATENT (want something else? Edit `__init__.py` line 3.)

| Model, clip, vae, latent and image are all being automagically connected. | Drop this image into ComfyUI to get a working workflow. |
|-|-|
|![workflow](docs/workflow.png)|![portrait](docs/portrait.png)|

## Caution

It's possible to create a loop with UE, and that currently isn't detected. If you get a RecursionError that's probably what you've done. Remember, *every* unconnected input gets connected to the UE output, even optional ones...

## How does it work?

Read the javascript - it's less than thirty lines long! Basically it hijacks the output of the ComfyUI app.graphToPrompt method, and scans through all the nodes twice - once to find any UE nodes, and the second time to find any unconnected inputs and, if there's a UE of the right type, connects them up (but only in the prompt that is about to be sent to the backend).
