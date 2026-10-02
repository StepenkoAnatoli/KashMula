---
url: https://huggingface.co/deepseek-ai/DeepSeek-OCR-2
retrieved: 2026-10-02
command: firecrawl scrape https://huggingface.co/deepseek-ai/DeepSeek-OCR-2 --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: deepseek-ai/DeepSeek-OCR-2 · Hugging Face
---
![DeepSeek AI](https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/logo.svg?raw=true)

* * *

[![Homepage](https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/badge.svg?raw=true)](https://www.deepseek.com/)[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-DeepSeek%20AI-ffc107?color=ffc107&logoColor=white)](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2)

[![Discord](https://img.shields.io/badge/Discord-DeepSeek%20AI-7289da?logo=discord&logoColor=white&color=7289da)](https://discord.gg/Tc7c45Zzu5)[![Twitter Follow](https://img.shields.io/badge/Twitter-deepseek_ai-white?logo=x&logoColor=white)](https://twitter.com/deepseek_ai)

[**🌟 Github**](https://github.com/deepseek-ai/DeepSeek-OCR-2) \|
[**📥 Model Download**](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2) \|
[**📄 Paper Link**](https://github.com/deepseek-ai/DeepSeek-OCR-2/blob/main/DeepSeek_OCR2_paper.pdf) \|
[**📄 Arxiv Paper Link**](https://arxiv.org/abs/2601.20552) \|

## [DeepSeek-OCR 2: Visual Causal Flow](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2)

![](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2/resolve/main/assets/fig1.png)

[Explore more human-like visual encoding.](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2)

## Usage

Inference using Huggingface transformers on NVIDIA GPUs. Requirements tested on python 3.12.9 + CUDA11.8：

```
torch==2.6.0
transformers==4.46.3
tokenizers==0.20.3
einops
addict
easydict
pip install flash-attn==2.7.3 --no-build-isolation
```

```python
from transformers import AutoModel, AutoTokenizer
import torch
import os
os.environ["CUDA_VISIBLE_DEVICES"] = '0'
model_name = 'deepseek-ai/DeepSeek-OCR-2'

tokenizer = AutoTokenizer.from_pretrained(model_name, trust_remote_code=True)
model = AutoModel.from_pretrained(model_name, _attn_implementation='flash_attention_2', trust_remote_code=True, use_safetensors=True)
model = model.eval().cuda().to(torch.bfloat16)

# prompt = "<image>\nFree OCR. "
prompt = "<image>\n<|grounding|>Convert the document to markdown. "
image_file = 'your_image.jpg'
output_path = 'your/output/dir'

res = model.infer(tokenizer, prompt=prompt, image_file=image_file, output_path = output_path, base_size = 1024, image_size = 768, crop_mode=True, save_results = True)
```

## vLLM

Refer to [🌟GitHub](https://github.com/deepseek-ai/DeepSeek-OCR-2/) for guidance on model inference acceleration and PDF processing, etc.

## Support-Modes

- Dynamic resolution
  - Default: (0-6)×768×768 + 1×1024×1024 — (0-6)×144 + 256 visual tokens ✅

## Main Prompts

```python
# document: <image>\n<|grounding|>Convert the document to markdown.
# without layouts: <image>\nFree OCR.
```

## Acknowledgement

We would like to thank [DeepSeek-OCR](https://github.com/deepseek-ai/DeepSeek-OCR/), [Vary](https://github.com/Ucas-HaoranWei/Vary/), [GOT-OCR2.0](https://github.com/Ucas-HaoranWei/GOT-OCR2.0/), [MinerU](https://github.com/opendatalab/MinerU), [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) for their valuable models and ideas.

We also appreciate the benchmark [OmniDocBench](https://github.com/opendatalab/OmniDocBench).

## Citation

```bibtex
@article{wei2025deepseek,
  title={DeepSeek-OCR: Contexts Optical Compression},
  author={Wei, Haoran and Sun, Yaofeng and Li, Yukun},
  journal={arXiv preprint arXiv:2510.18234},
  year={2025}
}
@article{wei2026deepseek,
  title={DeepSeek-OCR 2: Visual Causal Flow},
  author={Wei, Haoran and Sun, Yaofeng and Li, Yukun},
  journal={arXiv preprint arXiv:2601.20552},
  year={2026}
}
```

Downloads last month828,596

Safetensors

Model size

3B params

Tensor type

BF16

·

Files info

Inference Providers [NEW](https://huggingface.co/docs/inference-providers)

[Image-Text-to-Text](https://huggingface.co/tasks/image-text-to-text "Learn more about image-text-to-text")

This model isn't deployed by any Inference Provider. [🙋63Ask for provider support](https://huggingface.co/spaces/huggingface/InferenceSupport/discussions/7669)

## Model tree for deepseek-ai/DeepSeek-OCR-2

Adapters

[9 models](https://huggingface.co/models?other=base_model:adapter:deepseek-ai/DeepSeek-OCR-2)

Finetunes

[36 models](https://huggingface.co/models?other=base_model:finetune:deepseek-ai/DeepSeek-OCR-2)

Merges

[1 model](https://huggingface.co/models?other=base_model:merge:deepseek-ai/DeepSeek-OCR-2)

Quantizations

[Use with llama.cpp](https://huggingface.co/models?apps=llama.cpp&other=base_model:quantized:deepseek-ai/DeepSeek-OCR-2 "Use with llama.cpp")[Use with LM Studio](https://huggingface.co/models?apps=lmstudio&other=base_model:quantized:deepseek-ai/DeepSeek-OCR-2 "Use with LM Studio")[Use with Jan](https://huggingface.co/models?apps=jan&other=base_model:quantized:deepseek-ai/DeepSeek-OCR-2 "Use with Jan")[Use with Ollama](https://huggingface.co/models?apps=ollama&other=base_model:quantized:deepseek-ai/DeepSeek-OCR-2 "Use with Ollama")

[9 models](https://huggingface.co/models?other=base_model:quantized:deepseek-ai/DeepSeek-OCR-2)

## Spaces using deepseek-ai/DeepSeek-OCR-239

## Collection including deepseek-ai/DeepSeek-OCR-2

[2 items•Updated Feb 2• 37](https://huggingface.co/collections/deepseek-ai/deepseek-ocr)

## Papers for deepseek-ai/DeepSeek-OCR-2

[Paper • 2601.20552 •Published Jan 28• 75](https://huggingface.co/papers/2601.20552)[Paper • 2510.18234 •Published Oct 21, 2025• 96](https://huggingface.co/papers/2510.18234)

## Evaluation results

- [llamaindex/ParseBench](https://huggingface.co/datasets/llamaindex/ParseBench)[leaderboard](https://huggingface.co/datasets/llamaindex/ParseBench?eval_result=deepseek-ai/DeepSeek-OCR-2)
- Mean [View evaluation results](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2/discussions/28) [![](https://cdn-avatars.huggingface.co/v1/production/uploads/6980fe7cc9e5d7013d527b3a/F5Z_0zjcdl0cIKIq-MvTR.jpeg)\\
source](https://huggingface.co/datasets/llamaindex/ParseBench)




Pipeline name: deepseekocr2\_vllm

41.2 \*

- Text Content [View evaluation results](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2/discussions/28) [![](https://cdn-avatars.huggingface.co/v1/production/uploads/6980fe7cc9e5d7013d527b3a/F5Z_0zjcdl0cIKIq-MvTR.jpeg)\\
source](https://huggingface.co/datasets/llamaindex/ParseBench)




Pipeline name: deepseekocr2\_vllm

82 \*

- Text Formatting [View evaluation results](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2/discussions/28) [![](https://cdn-avatars.huggingface.co/v1/production/uploads/6980fe7cc9e5d7013d527b3a/F5Z_0zjcdl0cIKIq-MvTR.jpeg)\\
source](https://huggingface.co/datasets/llamaindex/ParseBench)




Pipeline name: deepseekocr2\_vllm

54 \*

- +3 more
- [allenai/olmOCR-bench](https://huggingface.co/datasets/allenai/olmOCR-bench)[leaderboard](https://huggingface.co/datasets/allenai/olmOCR-bench?eval_result=deepseek-ai/DeepSeek-OCR-2)
- Overall [View evaluation results](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2/discussions/18) [![](https://cdn-avatars.huggingface.co/v1/production/uploads/1608042047613-5f1158120c833276f61f1a84.jpeg)\\
source](https://x.com/staghado/status/2016161372938117205/photo/1)


76.3

- +6 more

Expand 1 benchmark

Inference providers allow you to run inference using different serverless providers.

StripeM-Inner

View evaluation results
shared by the community

Source: ParseBench
by boyang-runllama

Pipeline name: deepseekocr2\_vllm

View evaluation results
shared by the community

Source: ParseBench
by boyang-runllama

Pipeline name: deepseekocr2\_vllm

View evaluation results
shared by the community

Source: ParseBench
by boyang-runllama

Pipeline name: deepseekocr2\_vllm

View evaluation results
shared by the community

Source: Tweet by @staghado
by nielsr
