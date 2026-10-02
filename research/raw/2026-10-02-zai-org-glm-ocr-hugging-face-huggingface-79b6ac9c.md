---
url: https://huggingface.co/zai-org/GLM-OCR
retrieved: 2026-10-02
command: firecrawl scrape https://huggingface.co/zai-org/GLM-OCR --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: zai-org/GLM-OCR · Hugging Face
---
# GLM-OCR

![](https://raw.githubusercontent.com/zai-org/GLM-OCR/refs/heads/main/resources/logo.svg)

👋 Join our [WeChat](https://raw.githubusercontent.com/zai-org/GLM-OCR/refs/heads/main/resources/wechat.jpg) and [Discord](https://discord.gg/QR7SARHRxK) community


📍 Use GLM-OCR's [API](https://docs.z.ai/guides/vlm/glm-ocr)

👉 [GLM-OCR SDK](https://github.com/zai-org/GLM-OCR) Recommended


📖 [Technical Report](https://arxiv.org/abs/2603.10910)

## Introduction

GLM-OCR is a multimodal OCR model for complex document understanding, built on the GLM-V encoder–decoder architecture. It introduces Multi-Token Prediction (MTP) loss and stable full-task reinforcement learning to improve training efficiency, recognition accuracy, and generalization. The model integrates the CogViT visual encoder pre-trained on large-scale image–text data, a lightweight cross-modal connector with efficient token downsampling, and a GLM-0.5B language decoder. Combined with a two-stage pipeline of layout analysis and parallel recognition based on PP-DocLayout-V3, GLM-OCR delivers robust and high-quality OCR performance across diverse document layouts.

**Key Features**

- **State-of-the-Art Performance**: Achieves a score of 94.62 on OmniDocBench V1.5, ranking #1 overall, and delivers state-of-the-art results across major document understanding benchmarks, including formula recognition, table recognition, and information extraction.

- **Optimized for Real-World Scenarios**: Designed and optimized for practical business use cases, maintaining robust performance on complex tables, code-heavy documents, seals, and other challenging real-world layouts.

- **Efficient Inference**: With only 0.9B parameters, GLM-OCR supports deployment via vLLM, SGLang, and Ollama, significantly reducing inference latency and compute cost, making it ideal for high-concurrency services and edge deployments.

- **Easy to Use**: Fully open-sourced and equipped with a comprehensive [SDK](https://github.com/zai-org/GLM-OCR) and inference toolchain, offering simple installation, one-line invocation, and smooth integration into existing production pipelines.


## Performance

- Document Parsing & Information Extraction

![image](https://raw.githubusercontent.com/zai-org/GLM-OCR/refs/heads/main/resources/docparse.png)

- Real-World Scenarios Performance

![image](https://raw.githubusercontent.com/zai-org/GLM-OCR/refs/heads/main/resources/realworld.png)

- Speed Test

For speed, we compared different OCR methods under identical hardware and testing conditions (single replica, single concurrency), evaluating their performance in parsing and exporting Markdown files from both image and PDF inputs. Results show GLM-OCR achieves a throughput of 1.86 pages/second for PDF documents and 0.67 images/second for images, significantly outperforming comparable models.

![image](https://raw.githubusercontent.com/zai-org/GLM-OCR/refs/heads/main/resources/speed.png)

## Usage

### Official SDK

For document parsing tasks, we strongly recommend using our [official SDK](https://github.com/zai-org/GLM-OCR).
Compared with model-only inference, the SDK integrates PP-DocLayoutV3 and provides a complete, easy-to-use pipeline for document parsing, including layout analysis and structured output generation. This significantly reduces the engineering overhead required to build end-to-end document intelligence systems.

Note that the SDK is currently designed for document parsing tasks only. For information extraction tasks, please refer to the following section and run inference directly with the model.

### Serve GLM-OCR Locally

GLM-OCR supports deployment with the following frameworks. Feel free to try them out:

- [SGLang](https://github.com/sgl-project/sglang) — see [cookbook](https://cookbook.sglang.io/autoregressive/GLM/GLM-OCR)
- [vLLM](https://github.com/vllm-project/vllm) — see [recipes](https://recipes.vllm.ai/zai-org/GLM-OCR)
- [Transformers](https://github.com/huggingface/transformers) — see [transformers docs](https://github.com/huggingface/transformers/blob/main/docs/source/en/model_doc/glm_ocr.md)

### Prompt Limited

GLM-OCR currently supports two types of prompt scenarios:

1. **Document Parsing** – extract raw content from documents. Supported tasks include:

```python
{
    "text": "Text Recognition:",
    "formula": "Formula Recognition:",
    "table": "Table Recognition:"
}
```

2. **Information Extraction** – extract structured information from documents. Prompts must follow a strict JSON schema. For example, to extract personal ID information:

```python
请按下列JSON格式输出图中信息:
{
    "id_number": "",
    "last_name": "",
    "first_name": "",
    "date_of_birth": "",
    "address": {
        "street": "",
        "city": "",
        "state": "",
        "zip_code": ""
    },
    "dates": {
        "issue_date": "",
        "expiration_date": ""
    },
    "sex": ""
}
```

⚠️ Note: When using information extraction, the output must strictly adhere to the defined JSON schema to ensure downstream processing compatibility.

## Acknowledgement

This project is inspired by the excellent work of the following projects and communities:

- [PP-DocLayout-V3](https://huggingface.co/PaddlePaddle/PP-DocLayoutV3)
- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)
- [MinerU](https://github.com/opendatalab/MinerU)

## License

The GLM-OCR model is released under the MIT License.

The complete OCR pipeline integrates [PP-DocLayoutV3](https://huggingface.co/PaddlePaddle/PP-DocLayoutV3) for document layout analysis, which is licensed under the Apache License 2.0. Users should comply with both licenses when using this project.

## Citation

If you find GLM-OCR useful in your research, please cite our technical report:

```bibtex
@misc{duan2026glmocrtechnicalreport,
      title={GLM-OCR Technical Report},
      author={Shuaiqi Duan and Yadong Xue and Weihan Wang and Zhe Su and Huan Liu and Sheng Yang and Guobing Gan and Guo Wang and Zihan Wang and Shengdong Yan and Dexin Jin and Yuxuan Zhang and Guohong Wen and Yanfeng Wang and Yutao Zhang and Xiaohan Zhang and Wenyi Hong and Yukuo Cen and Da Yin and Bin Chen and Wenmeng Yu and Xiaotao Gu and Jie Tang},
      year={2026},
      eprint={2603.10910},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2603.10910},
}
```

Downloads last month1,819,908

Safetensors

Model size

1B params

Tensor type

BF16

·

Chat template

Files info

Inference Providers [NEW](https://huggingface.co/docs/inference-providers)

[Image-to-Text](https://huggingface.co/tasks/image-to-text "Learn more about image-to-text")

This model isn't deployed by any Inference Provider. [🙋44Ask for provider support](https://huggingface.co/spaces/huggingface/InferenceSupport/discussions/7799)

## Model tree for zai-org/GLM-OCR

Adapters

[12 models](https://huggingface.co/models?other=base_model:adapter:zai-org/GLM-OCR)

Finetunes

[29 models](https://huggingface.co/models?other=base_model:finetune:zai-org/GLM-OCR)

Quantizations

[35 models](https://huggingface.co/models?other=base_model:quantized:zai-org/GLM-OCR)

## Spaces using zai-org/GLM-OCR100

## Paper for zai-org/GLM-OCR

[Paper • 2603.10910 •Published Mar 11• 10](https://huggingface.co/papers/2603.10910)

## Evaluation results

- [allenai/olmOCR-bench](https://huggingface.co/datasets/allenai/olmOCR-bench)[leaderboard](https://huggingface.co/datasets/allenai/olmOCR-bench?eval_result=zai-org/GLM-OCR)
- Overall [View evaluation results](https://huggingface.co/zai-org/GLM-OCR/blob/main/.eval_results/olmocrbench.yaml)




Excluding Headers & Footers category. Using ZAI API.

75.2 \*

- Arxiv Math [View evaluation results](https://huggingface.co/zai-org/GLM-OCR/blob/main/.eval_results/olmocrbench.yaml)


80.7

- Old Scans Math [View evaluation results](https://huggingface.co/zai-org/GLM-OCR/blob/main/.eval_results/olmocrbench.yaml)


68.3

- +6 more
- [llamaindex/ParseBench](https://huggingface.co/datasets/llamaindex/ParseBench)[leaderboard](https://huggingface.co/datasets/llamaindex/ParseBench?eval_result=zai-org/GLM-OCR)
- Mean [View evaluation results](https://huggingface.co/zai-org/GLM-OCR/discussions/53) [![](https://cdn-avatars.huggingface.co/v1/production/uploads/6980fe7cc9e5d7013d527b3a/F5Z_0zjcdl0cIKIq-MvTR.jpeg)\\
source](https://huggingface.co/datasets/llamaindex/ParseBench)




Pipeline name: glmocr\_pipeline

29.6 \*

- +5 more

Expand 2 benchmarks

Inference providers allow you to run inference using different serverless providers.

View evaluation results

Excluding Headers & Footers category. Using ZAI API.

View evaluation results

View evaluation results

View evaluation results
shared by the community

Source: ParseBench
by boyang-runllama

Pipeline name: glmocr\_pipeline

StripeM-Inner
