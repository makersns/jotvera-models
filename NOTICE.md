# Distribution notice

Jotvera packages previously released model data for local use. The package format, signature, compatibility profile and validation notes are distribution additions. No model training or modification of the MiniCPM GGUF weight tensors is claimed.

## MiniCPM-V 4.7 1B

- Upstream model and GGUF files: OpenBMB, https://huggingface.co/openbmb/MiniCPM-V-4.7-1B-gguf
- Fixed upstream revision: `e81247fa2eac0d99e43aeac55da199221959af15`
- Model files use the root, thinking-disabled GGUF variant provided by the upstream publisher.
- Original model card and supporting tokenizer, processor, configuration and template files are included in the package.
- OpenBMB license: Apache License 2.0, copied unchanged from commit `4dbbb6c58b6f8a004d6689028417296719f0831a`.
- big_vision license: Apache License 2.0, copied unchanged from commit `0127fb6b337ee2a27bf4e54dea79cff176527356`.
- Original notices and copyright statements remain in the accompanying files.

The public preview package is not endorsed by its upstream model authors. Compatibility and observed quality are reported by Jotvera for the stated package and profile. Local self-tests remain required; preview distribution does not establish production or device certification.

This repository contains public model-distribution material only. Application code is distributed separately.
