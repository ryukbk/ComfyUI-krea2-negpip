# ComfyUI Krea 2 NegPip

ComfyUI custom node that adds NegPip-style negative prompt weighting support for Krea 2 workflows.

Use prompt weights such as `(word:-1.2)` to suppress specific concepts in Krea 2 prompts.

## Installation

Clone or copy this repository into your ComfyUI `custom_nodes` directory:

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/blue-pen5805/ComfyUI-krea2-negpip.git
```

Restart ComfyUI after installation.

## Usage

1. Load a Krea 2 model and Krea 2 CLIP as usual.
2. Add the **Apply Krea2 NegPip** node.
3. Connect both the `MODEL` and `CLIP` through this node before text encoding and sampling.
4. Use negative prompt weights in the prompt, for example:

```text
a portrait photo, (blurry:-1.0), (low quality:-1.2)
```

The node returns a patched `MODEL` and `CLIP`. Use those outputs for the rest of the workflow.

## Inputs

- `model`: Krea 2 model.
- `clip`: Krea 2 CLIP loaded with `CLIPLoader` type `krea2`.
- `value_strength`: Strength of the negative prompt effect. Default: `1.0`.
- `patch_txtfusion_refiners`: Optional stronger effect path. Default: `false`.
- `debug`: Print diagnostic information to the console.
- `block_start`: First transformer block to affect. Default: `0`.
- `block_end`: Last transformer block to affect. Default: `27`.
- `block_stride`: Affect every Nth block in the selected range. Default: `1`.

## Notes

- This node is intended for Krea 2 model layouts only.
- Negative weights are parsed from ComfyUI prompt weighting syntax, for example `(token:-1.0)`.
- Positive and non-unit weights are still applied to the text conditioning magnitude.
- After updating this node, restart ComfyUI and re-run text encoding.
- Prompts with image placeholders or custom embeddings are supported conservatively. Negative weights after image embeddings may not always be applied.

## Credits

This project is inspired by and references the original NegPip implementation:

- [hako-mikan/sd-webui-negpip](https://github.com/hako-mikan/sd-webui-negpip)
