---
url: https://huggingface.co/ZhengPeng7/BiRefNet
retrieved: 2026-10-02
command: firecrawl scrape https://huggingface.co/ZhengPeng7/BiRefNet --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: ZhengPeng7/BiRefNet · Hugging Face
---
# Bilateral Reference for High-Resolution Dichotomous Image Segmentation

[**Peng Zheng**](https://scholar.google.com/citations?user=TZRzWOsAAAAJ) 1,4,5,6,
[**Dehong Gao**](https://scholar.google.com/citations?user=0uPb8MMAAAAJ) 2,
[**Deng-Ping Fan**](https://scholar.google.com/citations?user=kakwJ5QAAAAJ) 1\*,
[**Li Liu**](https://scholar.google.com/citations?user=9cMQrVsAAAAJ) 3,
[**Jorma Laaksonen**](https://scholar.google.com/citations?user=qQP6WXIAAAAJ) 4,
[**Wanli Ouyang**](https://scholar.google.com/citations?user=pw_0Z_UAAAAJ) 5,
[**Nicu Sebe**](https://scholar.google.com/citations?user=stFCYOAAAAAJ) 6

1 Nankai University  2 Northwestern Polytechnical University  3 National University of Defense Technology  4 Aalto University  5 Shanghai AI Laboratory  6 University of Trento

[![](https://img.shields.io/badge/Journal-Paper-red)](https://www.sciopen.com/article/pdf/10.26599/AIR.2024.9150038.pdf)[![](https://img.shields.io/badge/arXiv-BiRefNet-red)](https://arxiv.org/pdf/2401.03407)[![](https://img.shields.io/badge/%E4%B8%AD%E6%96%87%E7%89%88-BiRefNet-red)](https://drive.google.com/file/d/1aBnJ_R9lbnC2dm8dqD0-pzP2Cu-U1Xpt/view?usp=drive_link)[![](https://img.shields.io/badge/Page-BiRefNet-red)](https://www.birefnet.top/)[![](https://img.shields.io/badge/Drive-Stuff-green)](https://drive.google.com/drive/folders/1s2Xe0cjq-2ctnJBR24563yMSCOu4CcxM)[![](https://img.shields.io/badge/License-MIT-yellow)](https://huggingface.co/ZhengPeng7/LICENSE)[![](https://img.shields.io/badge/%F0%9F%A4%97%20HF%20Spaces-BiRefNet-blue)](https://huggingface.co/spaces/ZhengPeng7/BiRefNet_demo)[![](https://img.shields.io/badge/%F0%9F%A4%97%20HF%20Models-BiRefNet-blue)](https://huggingface.co/ZhengPeng7/BiRefNet)[![](https://img.shields.io/badge/Single_Image_Inference-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/drive/14Dqg7oeBkFEtchaHLNpig2BcdkZEogba?usp=drive_link)[![](https://img.shields.io/badge/Inference_&_Evaluation-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/drive/1MaEiBfJ4xIaZZn0DqKrhydHB8X97hNXl#scrollTo=DJ4meUYjia6S)

| _DIS-Sample\_1_ | _DIS-Sample\_2_ |
| :-: | :-: |
| ![](https://drive.google.com/thumbnail?id=1ItXaA26iYnE8XQ_GgNLy71MOWePoS2-g&sz=w400) | ![](https://drive.google.com/thumbnail?id=1Z-esCujQF_uEa_YJjkibc3NUrW4aR_d4&sz=w400) |

This repo is the official implementation of " [**Bilateral Reference for High-Resolution Dichotomous Image Segmentation**](https://arxiv.org/pdf/2401.03407.pdf)" ( _**CAAI AIR 2024**_).

Visit our GitHub repo: [https://github.com/ZhengPeng7/BiRefNet](https://github.com/ZhengPeng7/BiRefNet) for more details -- **codes**, **docs**, and **model zoo**!

## How to use

### 0\. Install Packages:

```
pip install -qr https://raw.githubusercontent.com/ZhengPeng7/BiRefNet/main/requirements.txt
```

### 1\. Load BiRefNet:

#### Use codes + weights from HuggingFace

> Only use the weights on HuggingFace -- Pro: No need to download BiRefNet codes manually; Con: Codes on HuggingFace might not be latest version (I'll try to keep them always latest).

```python
# Load BiRefNet with weights
from transformers import AutoModelForImageSegmentation
birefnet = AutoModelForImageSegmentation.from_pretrained('ZhengPeng7/BiRefNet', trust_remote_code=True)
```

#### Use codes from GitHub + weights from HuggingFace

> Only use the weights on HuggingFace -- Pro: codes are always latest; Con: Need to clone the BiRefNet repo from my GitHub.

```shell
# Download codes
git clone https://github.com/ZhengPeng7/BiRefNet.git
cd BiRefNet
```

```python
# Use codes locally
from models.birefnet import BiRefNet

# Load weights from Hugging Face Models
birefnet = BiRefNet.from_pretrained('ZhengPeng7/BiRefNet')
```

#### Use codes from GitHub + weights from local space

> Only use the weights and codes both locally.

```python
# Use codes and weights locally
import torch
from utils import check_state_dict

birefnet = BiRefNet(bb_pretrained=False)
state_dict = torch.load(PATH_TO_WEIGHT, map_location='cpu')
state_dict = check_state_dict(state_dict)
birefnet.load_state_dict(state_dict)
```

#### Use the loaded BiRefNet for inference

```python
# Imports
from PIL import Image
import matplotlib.pyplot as plt
import torch
from torchvision import transforms
from models.birefnet import BiRefNet

birefnet = ... # -- BiRefNet should be loaded with codes above, either way.
torch.set_float32_matmul_precision(['high', 'highest'][0])
birefnet.to('cuda')
birefnet.eval()
birefnet.half()

def extract_object(birefnet, imagepath):
    # Data settings
    image_size = (1024, 1024)
    transform_image = transforms.Compose([\
        transforms.Resize(image_size),\
        transforms.ToTensor(),\
        transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])\
    ])

    image = Image.open(imagepath)
    input_images = transform_image(image).unsqueeze(0).to('cuda').half()

    # Prediction
    with torch.no_grad():
        preds = birefnet(input_images)[-1].sigmoid().cpu()
    pred = preds[0].squeeze()
    pred_pil = transforms.ToPILImage()(pred)
    mask = pred_pil.resize(image.size)
    image.putalpha(mask)
    return image, mask

# Visualization
plt.axis("off")
plt.imshow(extract_object(birefnet, imagepath='PATH-TO-YOUR_IMAGE.jpg')[0])
plt.show()
```

### 2\. Use inference endpoint locally:

> You may need to click the _deploy_ and set up the endpoint by yourself, which would make some costs.

```
import requests
import base64
from io import BytesIO
from PIL import Image

YOUR_HF_TOKEN = 'xxx'
API_URL = "xxx"
headers = {
    "Authorization": "Bearer {}".format(YOUR_HF_TOKEN)
}

def base64_to_bytes(base64_string):
    # Remove the data URI prefix if present
    if "data:image" in base64_string:
        base64_string = base64_string.split(",")[1]

    # Decode the Base64 string into bytes
    image_bytes = base64.b64decode(base64_string)
    return image_bytes

def bytes_to_base64(image_bytes):
    # Create a BytesIO object to handle the image data
    image_stream = BytesIO(image_bytes)

    # Open the image using Pillow (PIL)
    image = Image.open(image_stream)
    return image

def query(payload):
    response = requests.post(API_URL, headers=headers, json=payload)
    return response.json()

output = query({
    "inputs": "https://hips.hearstapps.com/hmg-prod/images/gettyimages-1229892983-square.jpg",
    "parameters": {}
})

output_image = bytes_to_base64(base64_to_bytes(output))
output_image
```

> This BiRefNet for standard dichotomous image segmentation (DIS) is trained on **DIS-TR** and validated on **DIS-TEs and DIS-VD**.

## This repo holds the official model weights of " [Bilateral Reference for High-Resolution Dichotomous Image Segmentation](https://arxiv.org/pdf/2401.03407)" ( _CAAI AIR 2024_).

This repo contains the weights of BiRefNet proposed in our paper, which has achieved the SOTA performance on three tasks (DIS, HRSOD, and COD).

Go to my GitHub page for BiRefNet codes and the latest updates: [https://github.com/ZhengPeng7/BiRefNet](https://github.com/ZhengPeng7/BiRefNet) :)

#### Try our online demos for inference:

- Online **Image Inference** on Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14Dqg7oeBkFEtchaHLNpig2BcdkZEogba?usp=drive_link)
- **Online Inference with GUI on Hugging Face** with adjustable resolutions: [![Hugging Face Spaces](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/ZhengPeng7/BiRefNet_demo)
- **Inference and evaluation** of your given weights: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1MaEiBfJ4xIaZZn0DqKrhydHB8X97hNXl#scrollTo=DJ4meUYjia6S)![](https://drive.google.com/thumbnail?id=12XmDhKtO1o2fEvBu4OE4ULVB2BK0ecWi&sz=w1080)

## Acknowledgement:

- Many thanks to @Freepik for their generous support on GPU resources for training higher resolution BiRefNet models and more of my explorations.
- Many thanks to @fal for their generous support on GPU resources for training better general BiRefNet models.
- Many thanks to @not-lain for his help on the better deployment of our BiRefNet model on HuggingFace.

## Citation

```
@article{zheng2024birefnet,
  title={Bilateral Reference for High-Resolution Dichotomous Image Segmentation},
  author={Zheng, Peng and Gao, Dehong and Fan, Deng-Ping and Liu, Li and Laaksonen, Jorma and Ouyang, Wanli and Sebe, Nicu},
  journal={CAAI Artificial Intelligence Research},
  volume = {3},
  pages = {9150038},
  year={2024}
}
```

Downloads last month770,845

Safetensors

Model size

0.2B params

Tensor type

I64

·

F16

·

Files info

Inference Providers [NEW](https://huggingface.co/docs/inference-providers)

[Image Segmentation](https://huggingface.co/tasks/image-segmentation "Learn more about image-segmentation")

This model isn't deployed by any Inference Provider. [🙋6Ask for provider support](https://huggingface.co/spaces/huggingface/InferenceSupport/discussions/186)

## Model tree for ZhengPeng7/BiRefNet

Finetunes

[6 models](https://huggingface.co/models?other=base_model:finetune:ZhengPeng7/BiRefNet)

Quantizations

[5 models](https://huggingface.co/models?other=base_model:quantized:ZhengPeng7/BiRefNet)

## Spaces using ZhengPeng7/BiRefNet100

## Collection including ZhengPeng7/BiRefNet

[A collection of my BiRefNet models -- different tasks, different scales.•18 items•Updated Nov 9, 2025• 11](https://huggingface.co/collections/ZhengPeng7/birefnet)

## Paper for ZhengPeng7/BiRefNet

[Paper • 2401.03407 •Published Jan 7, 2024• 4](https://huggingface.co/papers/2401.03407)
