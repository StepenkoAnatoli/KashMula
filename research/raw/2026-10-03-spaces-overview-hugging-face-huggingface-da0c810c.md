---
url: https://huggingface.co/docs/hub/spaces-overview
retrieved: 2026-10-03
command: firecrawl scrape https://huggingface.co/docs/hub/spaces-overview --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Spaces Overview · Hugging Face
---
Hub documentation

Spaces Overview

# Hub

🏡 View all docsAWS Trainium & InferentiaAccelerateArgillaAutoTrainBitsandbytesCLIChat UIDataset viewerDatasetsDeploying on AWSDiffusersDistilabelEvaluateGoogle CloudGoogle TPUsGradioHubHub Python LibraryHuggingface.jsInference Endpoints (dedicated)Inference ProvidersKernelsLeRobotLeaderboardsLightevalMicrosoft AzureOpenEnvOptimumPEFTReachy MiniSafetensorsSentence TransformersTRLTasksText Embeddings InferenceText Generation InferenceTokenizersTrackioTransformersTransformers.jsXetsmolagentstimm

Search documentation
`⌘K`

EN

[API docs](https://huggingface.co/spaces/huggingface/openapi) [606](https://github.com/huggingface/hub-docs)

![Hugging Face's logo](https://huggingface.co/front/assets/huggingface_logo-noborder.svg)

Join the Hugging Face community

and get access to the augmented documentation experience

Collaborate on models, datasets and Spaces

Faster examples with accelerated inference

Switch between documentation themes

[Sign Up](https://huggingface.co/join)

to get started

Copy page

# Spaces Overview

Hugging Face Spaces make it easy for you to create and deploy ML-powered demos in minutes. Watch the following video for a quick introduction to Spaces:

Build and Deploy a Machine Learning App in 2 Minutes - YouTube

Tap to unmute

[Build and Deploy a Machine Learning App in 2 Minutes](https://www.youtube.com/watch?v=3bSVKNKb_PY) [Hugging Face](https://www.youtube-nocookie.com/channel/UCHlNU7kIZhRgSbhHvFoy72w)

Hugging Face146K subscribers

[Watch on](https://www.youtube.com/watch?v=3bSVKNKb_PY)

In the following sections, you’ll learn the basics of creating a Space, configuring it, and deploying your code to it.

## Creating a new Space

**To make a new Space**, visit the [Spaces main page](https://huggingface.co/spaces) and click on **Create new Space**. Along with choosing a name for your Space, selecting an optional license, and setting your Space’s [visibility](https://huggingface.co/docs/hub/spaces-overview#space-visibility) (public, protected, or private), you’ll be prompted to choose the **SDK** for your Space. The Hub offers three SDK options: Gradio, Docker and static HTML. If you select “Gradio” as your SDK, you’ll be navigated to a new repo showing the following page:

> Static Spaces are free for everyone. Gradio and Docker Spaces run on compute and require a paid plan to create: [PRO](https://huggingface.co/pro) for personal accounts, [Team or Enterprise](https://huggingface.co/enterprise) for organizations. Free personal accounts in good standing can still host up to 2 Gradio Spaces running on [ZeroGPU](https://huggingface.co/docs/hub/spaces-zerogpu).

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/spaces-blank-space.png)![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/spaces-blank-space-dark.png)

Under the hood, Spaces stores your code inside a git repository, just like the model and dataset repositories. Thanks to this, the same tools we use for all the [other repositories on the Hub](https://huggingface.co/docs/hub/repositories) (`git` and `git-xet`) also work for Spaces. Follow the same flow as in [Getting Started with Repositories](https://huggingface.co/docs/hub/repositories-getting-started) to add files to your Space. Each time a new commit is pushed, the Space will automatically rebuild and restart.

For step-by-step tutorials to creating your first Space, see the guides below:

- [Creating a Gradio Space](https://huggingface.co/docs/hub/spaces-sdks-gradio)
- [Creating a Docker Space](https://huggingface.co/docs/hub/spaces-sdks-docker-first-demo)

## Space visibility

You can set a Space’s visibility from the **Settings** tab using the visibility dropdown. Spaces support three visibility levels: **public**, **protected**, and **private**.

> Protected visibility is part of [PRO](https://huggingface.co/pro) or [Team & Enterprise](https://huggingface.co/enterprise) plans.

|  | Public | Protected | Private |
| --- | --- | --- | --- |
| Source code on the Hub | Visible to everyone | Private (only owner/collaborators) | Private (only owner/collaborators) |
| App accessible via embed URL | Yes | Yes | No |
| App accessible via [custom domain](https://huggingface.co/docs/hub/spaces-custom-domain) | Yes | Yes | No |
| Clonable by others | Yes | No | No |

**Public** Spaces are fully open: anyone can view the source code, access the running app, and clone the repository.

**Protected** Spaces keep their source code private on the Hub — only the owner and collaborators can view or clone the repository. However, the running app is publicly accessible through its embed URL (`https://<space-subdomain>.hf.space`) or through a [custom domain](https://huggingface.co/docs/hub/spaces-custom-domain) when one is configured. This is especially useful for hosting websites or apps without publishing the source code.

**Private** Spaces are fully private: the source code and the running app are only accessible to the owner and collaborators. The Space will not appear in search results and other users will receive a `404` error when visiting its URL.

## Hardware resources

Each Spaces environment is limited to 16GB RAM, 2 CPU cores and 50GB of (not persistent) disk space by default. The default CPU Basic hardware has no hourly cost, but creating a Space that runs on compute (Gradio or Docker) requires a paid plan, while Static Spaces are free for everyone. You can upgrade to better hardware, including a variety of GPU accelerators, for a [competitive price](https://huggingface.co/pricing#spaces). To request an upgrade, please click the _Settings_ button in your Space and select your preferred hardware environment.

| **Hardware** | **CPU** | **Memory** | **GPU Memory** | **Hourly Price** |
| --- | --- | --- | --- | --- |
| CPU Basic | 2 vCPU | 16 GB |  | FREE |
| CPU Upgrade | 8 vCPU | 32 GB |  | $0.03 |
| Nvidia T4 - small | 4 vCPU | 15 GB | 16 GB | $0.40 |
| Nvidia T4 - medium | 8 vCPU | 30 GB | 16 GB | $0.60 |
| 1x Nvidia L4 | 8 vCPU | 30 GB | 24 GB | $0.80 |
| 4x Nvidia L4 | 48 vCPU | 186 GB | 96 GB | $3.80 |
| 1x Nvidia L40S | 8 vCPU | 62 GB | 48 GB | $1.80 |
| 4x Nvidia L40S | 48 vCPU | 382 GB | 192 GB | $8.30 |
| 8x Nvidia L40S | 192 vCPU | 1534 GB | 384 GB | $23.50 |
| Nvidia A10G - small | 4 vCPU | 15 GB | 24 GB | $1.00 |
| Nvidia A10G - large | 12 vCPU | 46 GB | 24 GB | $1.50 |
| 2x Nvidia A10G - large | 24 vCPU | 92 GB | 48 GB | $3.00 |
| 4x Nvidia A10G - large | 48 vCPU | 184 GB | 96 GB | $5.00 |
| Nvidia A100 - large | 12 vCPU | 142 GB | 80 GB | $2.50 |
| 4x Nvidia A100 | 48 vCPU | 568 GB | 320 GB | $10.00 |
| 8x Nvidia A100 | 96 vCPU | 1136 GB | 640 GB | $20.00 |

Note: Find more detailed and comprehensive pricing information on [our pricing page](https://huggingface.co/pricing).

Do you have an awesome Space but need help covering the hardware upgrade costs? We love helping out those with an innovative Space so please feel free to apply for a community GPU grant using the link in the _Settings_ tab of your Space and see if yours makes the cut!

Read more in our dedicated sections on [Spaces GPU Upgrades](https://huggingface.co/docs/hub/spaces-gpus) and [Spaces Disk Usage & Storage](https://huggingface.co/docs/hub/spaces-storage).

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/spaces-gpu-settings.png)![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/spaces-gpu-settings-dark.png)

## Managing secrets and environment variables

If your app requires environment variables (for instance, secret keys or tokens), do not hard-code them inside your app! Instead, go to the Settings page of your Space repository and add a new **variable** or **secret**. Use variables if you need to store non-sensitive configuration values and secrets for storing access tokens, API keys, or any sensitive value or credentials.

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/secrets-and-variables.png)![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/secrets-and-variables-dark.png)

You can use:

- **Variables** if you need to store non-sensitive configuration values. They are publicly accessible and viewable and will be automatically added to Spaces duplicated from yours.
- **Secrets** to store access tokens, API keys, or any sensitive values or credentials. They are private and their value cannot be read from the Space’s settings page once set. They won’t be added to Spaces duplicated from your repository.

Accessing secrets and variables is different depending on your Space SDK:

- For Static Spaces, both are available through client-side JavaScript in `window.huggingface.variables`
- For Docker Spaces, check out [environment management with Docker](https://huggingface.co/docs/hub/spaces-sdks-docker#secrets-and-variables-management)

For other Spaces, both are exposed to your app as environment variables. Here is a very simple example of accessing the previously declared `MODEL_REPO_ID` variable in Python (it would be the same for secrets):

Copied

```py
import os
print(os.getenv('MODEL_REPO_ID'))
```

Spaces owners are warned when our `Spaces Secrets Scanner` [finds hard-coded secrets](https://huggingface.co/docs/hub/security-secrets).

## Duplicating a Space

Duplicating a Space can be useful if you want to build a new demo using another demo as an initial template. Duplicated Spaces can also be useful if you want to have an individual Upgraded Space for your use with fast inference.

If you want to duplicate a Space, you can click the three dots at the top right of the space and click **Duplicate this Space**. Once you do this, you will be able to change the following attributes:

- Owner: The duplicated Space can be under your account or any organization in which you have write access
- Space name
- Visibility: The Space is private by default. Read more about visibility options [here](https://huggingface.co/docs/hub/repositories-settings#repository-visibility).
- Hardware: You can choose the hardware on which the Space will be running. Read more about hardware upgrades [here](https://huggingface.co/docs/hub/spaces-gpus).
- Storage: If the original repo uses a storage bucket, you will be prompted to configure storage. Read more about disk usage and storage [here](https://huggingface.co/docs/hub/spaces-storage).
- Secrets and variables: If the original repo has set some secrets and variables, you’ll be able to set them while duplicating the repo.

Some Spaces might have environment variables that you may need to set up. In these cases, the duplicate workflow will auto-populate the public Variables from the source Space, and give you a warning about setting up the Secrets. The duplicated Space will use CPU Basic hardware by default, but you can later upgrade if needed. Duplicating follows the same rules as creating a new Space: duplicating a Gradio or Docker Space requires a paid plan for the target account or organization (with the same [ZeroGPU free tier](https://huggingface.co/docs/hub/spaces-zerogpu) exception for personal accounts).

## Networking

If your Space needs to make any network requests, you can make requests through the standard HTTP and HTTPS ports (80 and 443) along with port 8080. Any requests going to other ports will be blocked.

## Lifecycle management

On free hardware, your Space will “go to sleep” and stop executing after a period of time if unused. If you wish for your Space to run indefinitely, consider [upgrading to paid hardware](https://huggingface.co/docs/hub/spaces-gpus). You can also manually pause your Space from the **Settings** tab. A paused Space stops executing until manually restarted by its owner.
Paused time is not billed.

## Built-in environment variables

In some cases, you might be interested in having programmatic access to the Space author or repository name. This feature is particularly useful when you expect users to duplicate your Space. To help with this, Spaces exposes different environment variables at runtime (see also [built-in environment variables in Jobs](https://huggingface.co/docs/hub/jobs-configuration#built-in-environment-variables)). Given a Space [`osanseviero/i-like-flan`](https://huggingface.co/spaces/osanseviero/i-like-flan):

- `ACCELERATOR`: The type of accelerator available (e.g., `t4-medium`, `a10g-small`), or `none` for CPU-only Spaces.
- `CPU_CORES`: 4
- `MEMORY`: 15Gi
- `SPACE_AUTHOR_NAME`: osanseviero
- `SPACE_REPO_NAME`: i-like-flan
- `SPACE_TITLE`: I Like Flan (specified in the README file)
- `SPACE_ID`: `osanseviero/i-like-flan`
- `SPACE_HOST`: `osanseviero-i-like-flan.hf.space`
- `SPACE_CREATOR_USER_ID`: `6032802e1f993496bc14d9e3` \- This is the ID of the user that originally created the Space. It’s useful if the Space is under an organization. You can get the user information with an API call to `https://huggingface.co/api/users/{SPACE_CREATOR_USER_ID}/overview`.
- `SPACE_SIGNING_SECRET`: a random secret unique to your Space, exposed as a secret. It stays the same across restarts, rebuilds, and replicas, so you can use it to sign things like cookies, OAuth state, or CSRF tokens. To use your own value instead, add a secret named `SPACE_SIGNING_SECRET` in your Space settings.

In case [OAuth](https://huggingface.co/docs/hub/spaces-oauth) is enabled for your Space, the following variables will also be available:

- `OAUTH_CLIENT_ID`: the client ID of your OAuth app (public)
- `OAUTH_CLIENT_SECRET`: the client secret of your OAuth app
- `OAUTH_SCOPES`: scopes accessible by your OAuth app. Currently, this is always `"openid profile"`.
- `OPENID_PROVIDER_URL`: The URL of the OpenID provider. The OpenID metadata will be available at [`{OPENID_PROVIDER_URL}/.well-known/openid-configuration`](https://huggingface.co/.well-known/openid-configuration).

## Clone the Repository

You can easily clone your Space repo locally. Start by clicking on the dropdown menu in the top right of your Space page:

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/SpacesCloneRepo2.png)![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/SpacesCloneRepo1.png)

Select “Clone repository”, and then you’ll be able to follow the instructions to clone the Space repo to your local machine using HTTPS or SSH.

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/HttpsClone2.png)![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/HttpsClone1.png)

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/SSHClone2.png)![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/SSHClone1.png)

## Linking Models and Datasets on the Hub

You can showcase all the models and datasets that your Space links to by adding their identifier in your Space’s README metadata. To do so, you can define them under the `models` and `datasets` keys. In addition to listing the artefacts in the README file, you can also record them in any `.py`, `.ini` or `.html` file as well. We’ll parse it auto-magically!

Here’s an example linking two models from a space:

Copied

```
title: My lovely space
emoji: 🤗
colorFrom: blue
colorTo: green
sdk: docker
pinned: false
models:
- reach-vb/musicgen-large-fp16-endpoint
- reach-vb/wav2vec2-large-xls-r-1B-common_voice7-lt-ft
```

[Update on GitHub](https://github.com/huggingface/hub-docs/blob/main/docs/hub/spaces-overview.md)

[←Spaces](https://huggingface.co/docs/hub/spaces) [Handling Spaces Dependencies→](https://huggingface.co/docs/hub/spaces-dependencies)
