---
url: https://pypi.org/project/pydantic-ai/
retrieved: 2026-10-04
command: firecrawl scrape https://pypi.org/project/pydantic-ai/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: pydantic-ai · PyPI
---
[Skip to main content](https://pypi.org/project/pydantic-ai/#content) Switch to mobile version

Search PyPISearch

# pydantic-ai 2.54.0

AI Agent Framework, the Pydantic way

pip install pydantic-aiCopy PIP instructions

[![Pydantic AI](https://pypi-camo.freetls.fastly.net/4c88229f43429d40a44fd2064724c2190d197edb/68747470733a2f2f707964616e7469632e6465762f646f63732f61692f696d672f707964616e7469632d61692d6c696768742e737667)](https://pydantic.dev/docs/ai/)

### How Python does AI

[![CI](https://pypi-camo.freetls.fastly.net/30d12dc5a47963aef82cecc37674cb0e4827bc18/68747470733a2f2f6769746875622e636f6d2f707964616e7469632f707964616e7469632d61692f616374696f6e732f776f726b666c6f77732f63692e796d6c2f62616467652e7376673f6576656e743d70757368)](https://github.com/pydantic/pydantic-ai/actions/workflows/ci.yml?query=branch%3Amain)![Coverage](https://pypi-camo.freetls.fastly.net/2bdee873cc103def8843888436f081cc6be1dcdb/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f636f7665726167652d3130302532352d627269676874677265656e2e737667)[![PyPI](https://pypi-camo.freetls.fastly.net/ffef25a7730c4f1e10e5549ac368ffc81bab4e3e/68747470733a2f2f696d672e736869656c64732e696f2f707970692f762f707964616e7469632d61692e737667)](https://pypi.python.org/pypi/pydantic-ai)[![versions](https://pypi-camo.freetls.fastly.net/41dc246b9e3ff6fd770ab40f85848515532a59cc/68747470733a2f2f696d672e736869656c64732e696f2f707970692f707976657273696f6e732f707964616e7469632d61692e737667)](https://github.com/pydantic/pydantic-ai)[![license](https://pypi-camo.freetls.fastly.net/64540c5276748aaca8c3f110b789853f3f8a0473/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f707964616e7469632f707964616e7469632d61692e7376673f76)](https://github.com/pydantic/pydantic-ai/blob/main/LICENSE)[![Join Slack](https://pypi-camo.freetls.fastly.net/0de40529952c66b1024dbaec0c3682bb656ea275/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f536c61636b2d4a6f696e253230536c61636b2d3441313534423f6c6f676f3d736c61636b)](https://logfire.pydantic.dev/docs/join-slack/)

Agents, realtime voice, image generation, embeddings. Every model, every interface, typed end to end.

* * *

**Pydantic AI** is the Python AI SDK: a typed, [extensible](https://pydantic.dev/docs/ai/guides/extensibility/) agent loop with [every model](https://pydantic.dev/docs/ai/models/overview/) a string swap away. The same agent [runs everywhere you need it](https://pydantic.dev/docs/ai/overview/interfaces/): behind a [web frontend](https://pydantic.dev/docs/ai/integrations/ui/overview/), in the [terminal](https://pydantic.dev/docs/ai/integrations/cli/), on a [voice call](https://pydantic.dev/docs/ai/realtime/overview/), on a [durable background queue](https://pydantic.dev/docs/ai/capabilities/durable_execution/overview/), in [GitHub Actions](https://pydantic.dev/docs/ai/harness/gh-aw/), or as a plain object you call [`run()`](https://pydantic.dev/docs/ai/core-concepts/agent/#running-agents) on. [Image generation](https://pydantic.dev/docs/ai/guides/image-generation/) and [embeddings](https://pydantic.dev/docs/ai/guides/embeddings/) come in the same box; [Pydantic Graph](https://pydantic.dev/docs/ai/graph/graph/) and [Pydantic Evals](https://pydantic.dev/docs/ai/evals/evals/) are separate packages, for typed control flow and for testing agent behavior the way pytest tests code.

**[Pydantic AI Harness](https://pydantic.dev/docs/ai/harness/)** has everything an agent needs for complex, long-running work, snapped on as [capabilities](https://pydantic.dev/docs/ai/capabilities/overview/), from [memory](https://pydantic.dev/docs/ai/harness/memory/), [guardrails](https://pydantic.dev/docs/ai/harness/guardrails/), and [sub-agents](https://pydantic.dev/docs/ai/harness/subagents/) to [planning](https://pydantic.dev/docs/ai/harness/planning/), [context management](https://pydantic.dev/docs/ai/harness/compaction/), and [persistence](https://pydantic.dev/docs/ai/core-concepts/persistence/), up to a complete [coding agent](https://pydantic.dev/docs/ai/harness/coder/).

[Pydantic Logfire](https://pydantic.dev/logfire?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai) is the AI observability platform that sees your whole app, not just the LLM calls, and the [Pydantic AI Gateway](https://pydantic.dev/ai-gateway?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai) is one key for every model with real-time cost monitoring and budget control; the Gateway self-hosts if you would rather, and our [instrumentation](https://pydantic.dev/docs/ai/integrations/logfire/) is plain OpenTelemetry, so any backend you already run works. Underneath both, [genai-prices](https://github.com/pydantic/genai-prices) keeps model pricing current, and [Monty](https://github.com/pydantic/monty) is the sandboxed Python interpreter that runs model-written code.

View the complete documentation at [pydantic.dev/docs/ai](https://pydantic.dev/docs/ai/).

## What are you building?

From simple typed data extraction to complex, long-running multi-agent collaboration, Pydantic AI and [Pydantic AI Harness](https://pydantic.dev/docs/ai/harness/) have got you covered.

### Coding agent

A complete coding agent in your terminal: workspace-rooted [file access](https://pydantic.dev/docs/ai/harness/filesystem/), allowlisted [shell](https://pydantic.dev/docs/ai/harness/shell/), [repo orientation](https://pydantic.dev/docs/ai/harness/repo-context/), [planning](https://pydantic.dev/docs/ai/harness/planning/), and [context management](https://pydantic.dev/docs/ai/harness/compaction/) that survives long sessions. Here with [web search](https://pydantic.dev/docs/ai/capabilities/web-search/) and a second-opinion [advisor](https://pydantic.dev/docs/ai/harness/advisor/) snapped on alongside:

```
uv add pydantic-ai pydantic-ai-harness
```

```
from pydantic_ai import Agent
from pydantic_ai.capabilities import WebSearch
from pydantic_ai_harness import Advisor, Coder

agent = Agent(
    'anthropic:claude-fable-5-1',
    capabilities=[\
        Coder(),  # files, shell, repo context, sub-agents, context management\
        WebSearch(),  # look up docs and error messages on the web\
        Advisor('openai:gpt-6-sol'),  # a second opinion from another model when stuck\
    ],
)
agent.to_cli_sync()
```

[`Coder`](https://pydantic.dev/docs/ai/harness/coder/) is a regular [combined capability](https://pydantic.dev/docs/ai/capabilities/custom/#composition-and-middleware-semantics), not a black box: use it whole, or use the blocks it bundles directly; the two are equivalent:

```
capabilities = [\
    FileSystem('.'), Shell(cwd='.'), RepoContext(), SubAgents(...),\
    ClearToolResults(), WarnNearLimits(), ToolOutputLimits(), RepairToolArguments(),\
]
```

Run the file and you're chatting with the agent in your terminal. To try it before writing any code, run the exported [`coder_agent`](https://pydantic.dev/docs/ai/harness/coder/) with [`clai`](https://pydantic.dev/docs/ai/integrations/cli/#custom-agents) (the Pydantic AI CLI), via [`uvx`](https://docs.astral.sh/uv/guides/tools/):

```
uvx --with pydantic-ai-harness clai -a pydantic_ai_harness.coder:coder_agent -m anthropic:claude-fable-5
```

**Build this →** [Coder](https://pydantic.dev/docs/ai/harness/coder/), from the [Harness](https://pydantic.dev/docs/ai/harness/)

**Run it on GitHub →** [GitHub Agentic Workflows](https://pydantic.dev/docs/ai/harness/gh-aw/), on issues, pull requests or a schedule

### Data extraction

Give the agent an [output type](https://pydantic.dev/docs/ai/core-concepts/output/) and [tools](https://pydantic.dev/docs/ai/tools-toolsets/tools/), and every run comes back validated and typed:

```
uv add pydantic-ai
```

```
from typing import Literal

from pydantic import BaseModel, Field

from pydantic_ai import Agent, RunContext

class Sentiment(BaseModel):
    label: Literal['positive', 'negative', 'neutral']
    score: float = Field(ge=-1, le=1)

agent = Agent('openai:gpt-6-sol', output_type=Sentiment)

@agent.tool
def recent_reviews(ctx: RunContext, product: str) -> list[str]:
    """Fetch recent review snippets for a product."""
    return ['The new release fixed everything I complained about!']

result = agent.run_sync('How are people feeling about the Extract app?')
print(result.output)
#> label='positive' score=0.9
```

The [`@agent.tool`](https://pydantic.dev/docs/ai/tools-toolsets/tools/) function receives a [`RunContext`](https://pydantic.dev/docs/ai/core-concepts/dependencies/) that carries your dependencies in; the rest of its signature and its docstring become the tool schema, arguments are validated before your code runs, and the run is guaranteed to return a `Sentiment`, so your IDE, type checker, and the LLM all agree on the returned type.

**Build this →** [Agents](https://pydantic.dev/docs/ai/core-concepts/agent/), [Function Tools](https://pydantic.dev/docs/ai/tools-toolsets/tools/), and [Structured Output](https://pydantic.dev/docs/ai/core-concepts/output/)

### Durable workflow

Attach [`TemporalDurability`](https://pydantic.dev/docs/ai/capabilities/durable_execution/temporal/) and the same agent runs inside a [Temporal](https://pydantic.dev/docs/ai/capabilities/durable_execution/temporal/) workflow under [durable execution](https://pydantic.dev/docs/ai/capabilities/durable_execution/overview/): every model and tool call becomes a durable activity, so a run working through a background queue survives restarts, failures, and long waits:

```
uv add "pydantic-ai[temporal]"
```

```
from temporalio import workflow

from pydantic_ai import Agent
from pydantic_ai.capabilities import WebFetch, WebSearch
from pydantic_ai.durable_exec.temporal import PydanticAIWorkflow, TemporalDurability

agent = Agent(
    'openai:gpt-6-sol',
    instructions='Research the topic and write a structured brief.',
    name='researcher',
    capabilities=[WebSearch(), WebFetch(), TemporalDurability()],
)

@workflow.defn
class ResearchWorkflow(PydanticAIWorkflow):
    __pydantic_ai_agents__ = [agent]

    @workflow.run
    async def run(self, topic: str) -> str:
        result = await agent.run(f'Write a brief on: {topic}')
        return result.output
```

[DBOS](https://pydantic.dev/docs/ai/capabilities/durable_execution/dbos/) and [Prefect](https://pydantic.dev/docs/ai/capabilities/durable_execution/prefect/) attach the same way, first-party and co-maintained, with [Restate, AWS Lambda, Kitaru, Airflow, and Absurd](https://pydantic.dev/docs/ai/capabilities/durable_execution/overview/) integrations besides.

**Build this →** [Durable Execution](https://pydantic.dev/docs/ai/capabilities/durable_execution/overview/)

### Realtime voice

Put the same agent on a live voice session, [tools](https://pydantic.dev/docs/ai/realtime/tools/) and [capabilities](https://pydantic.dev/docs/ai/realtime/capabilities/) included:

```
uv add "pydantic-ai[openai-realtime]"
```

```
import asyncio

from pydantic_ai import Agent
from pydantic_ai.capabilities import MCP

agent = Agent(
    instructions='You are a helpful voice assistant.',
    capabilities=[MCP('https://internal.example.com/mcp')],  # capabilities work in voice too
)

@agent.tool_plain
def order_status(order_id: str) -> str:
    """Look up the status of an order."""
    return f'Order {order_id}: shipped, arriving Thursday.'

async with agent.realtime('openai:gpt-realtime-2.1').session() as session:
    microphone = asyncio.create_task(session.send_audio(microphone_chunks()))  # your microphone → the model
    speaker = asyncio.create_task(play_audio(session.stream_audio()))  # model audio → your speaker
    async for part in session.stream_transcripts():
        print(f'{part.speaker}: {part.transcript}')
```

The model calls your tools mid-conversation while it keeps talking, and every session is [instrumented](https://pydantic.dev/docs/ai/integrations/logfire/); voice is just another frontend, on OpenAI Realtime, Gemini Live, Azure, and xAI Grok Voice.

**Build this →** [Realtime Voice](https://pydantic.dev/docs/ai/realtime/overview/)

### Image generation

Generate an image with a dedicated image model, no agent run required:

```
uv add pydantic-ai
```

```
from pathlib import Path

from pydantic_ai import ImageGenerator

generator = ImageGenerator('openai:gpt-image-2')
result = generator.generate_sync('A minimalist logo for a coffee shop called Extract.')
Path('logo.png').write_bytes(result.image.data)
```

That [standalone image API](https://pydantic.dev/docs/ai/guides/image-generation/) is for when your application decides; when an agent run decides, there is [provider-native generation](https://pydantic.dev/docs/ai/tools-toolsets/native-tools/#image-generation-tool) with `output_type=BinaryImage` for a typed image [output](https://pydantic.dev/docs/ai/core-concepts/output/#image-output), and the [`ImageGeneration` capability](https://pydantic.dev/docs/ai/capabilities/image-generation/) with its fallbacks for models that generate no images of their own.

**Build this →** [Image Generation](https://pydantic.dev/docs/ai/guides/image-generation/)

### See your first run in Logfire

> **Tip:** Add two lines before any of these agents runs, and every model call and tool call shows up in [Pydantic Logfire](https://pydantic.dev/logfire?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai). Logfire has a [free tier](https://pydantic.dev/pricing/) that needs no credit card, and you can sign up with just a GitHub account. Run `uvx logfire auth` and `uvx logfire projects new` once first, or point your coding agent at the [Logfire setup skill](https://pydantic.dev/ai-setup.md) to do it for you. The [Logfire guide](https://pydantic.dev/docs/ai/integrations/logfire/#using-logfire) has the details, and [any OpenTelemetry backend](https://pydantic.dev/docs/ai/integrations/logfire/#using-opentelemetry) works instead.
>
> ```
> import logfire
>
> logfire.configure()
> logfire.instrument_pydantic_ai()
> ```

## Why Pydantic AI

- **Any model, one Python API.** [Virtually every model and provider](https://pydantic.dev/docs/ai/models/overview/) (OpenAI, Anthropic, Google, Bedrock, Azure AI Foundry, Groq, Mistral, xAI, Ollama, and dozens more), swappable with a string, or through the [Pydantic AI Gateway](https://pydantic.dev/docs/ai/overview/gateway/): one key for all of them, with failover and cost monitoring built in. No flagship feature is locked to one vendor.

- **Typed end to end.** [Structured outputs](https://pydantic.dev/docs/ai/core-concepts/output/), typed [dependency injection](https://pydantic.dev/docs/ai/core-concepts/dependencies/), [typed tools](https://pydantic.dev/docs/ai/tools-toolsets/tools/): your IDE, type checker, and coding agent all know what your agent returns, moving whole classes of errors from runtime to write-time. When plain control flow isn't enough, [Pydantic Graph](https://pydantic.dev/docs/ai/graph/graph/) brings the same typing to graph-based workflows.

- **Measured, not vibes.** OpenTelemetry-native [instrumentation](https://pydantic.dev/docs/ai/integrations/logfire/) works with any OTel backend; one line lights up [Pydantic Logfire](https://pydantic.dev/logfire/llm-observability?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai) for real-time debugging, tracing, and cost tracking backed by [genai-prices](https://github.com/pydantic/genai-prices). [Pydantic Evals](https://pydantic.dev/docs/ai/evals/evals/) tests agent behavior the way pytest tests code.

- **Batteries, composably.** One primitive, the [capability](https://pydantic.dev/docs/ai/capabilities/overview/), bundles [tools](https://pydantic.dev/docs/ai/tools-toolsets/tools/), [instructions](https://pydantic.dev/docs/ai/core-concepts/agent/#instructions), [hooks](https://pydantic.dev/docs/ai/core-concepts/hooks/), and [model settings](https://pydantic.dev/docs/ai/core-concepts/agent/#model-run-settings) into reusable units. Core ships fundamentals like [MCP](https://pydantic.dev/docs/ai/capabilities/mcp/) and [web search](https://pydantic.dev/docs/ai/capabilities/web-search/), the [Harness](https://pydantic.dev/docs/ai/harness/) ships everything else, and complete agents like [Coder](https://pydantic.dev/docs/ai/harness/coder/) and [Researcher](https://pydantic.dev/docs/ai/harness/researcher/) are just capabilities composed: they come apart the way they went together. Or skip code entirely with [YAML/JSON agent specs](https://pydantic.dev/docs/ai/core-concepts/agent-spec/).

- **[Every interface](https://pydantic.dev/docs/ai/overview/interfaces/).** One agent definition runs as a [CLI](https://pydantic.dev/docs/ai/integrations/cli/), a [built-in web chat](https://pydantic.dev/docs/ai/guides/web/), or [realtime speech](https://pydantic.dev/docs/ai/realtime/overview/) (OpenAI Realtime, Gemini Live, Azure, xAI Grok Voice); [UI event streams](https://pydantic.dev/docs/ai/integrations/ui/overview/) (AG-UI, Vercel AI) connect it to your own frontend or anything else; [ACP](https://pydantic.dev/docs/ai/harness/acp/) serves it as an editor agent; and [GitHub Agentic Workflows](https://pydantic.dev/docs/ai/harness/gh-aw/) runs it headless on issues, pull requests or a schedule.

- **Durable execution.** [Durable execution](https://pydantic.dev/docs/ai/capabilities/durable_execution/overview/) on eight engines: Temporal, DBOS, Prefect, Restate, AWS Lambda, Kitaru, Airflow, and Absurd, the first five co-maintained with the vendor teams. Agents survive restarts and run for days on the engine you already operate, with [human-in-the-loop approval](https://pydantic.dev/docs/ai/tools-toolsets/deferred-tools/#human-in-the-loop-tool-approval) built in.

- **Coming from another framework?** The [comparisons](https://pydantic.dev/docs/ai/comparisons/overview/) show where Pydantic AI differs from LangChain, Google ADK, the Claude Agent SDK and seven more, and the [migration skills](https://pydantic.dev/docs/ai/comparisons/migrate-from-other-frameworks/) let your coding agent port an existing application over.


Built by the [Pydantic](https://docs.pydantic.dev/) team: [Pydantic Validation](https://pydantic.dev/docs/) is the validation layer of the OpenAI SDK, the Anthropic SDK, the Google ADK, LangChain, and most of the AI ecosystem (and the foundation FastAPI was built on). Pydantic AI brings that same feeling to agents.

## Putting it together: a bank support agent

A typed support agent showing several features working together: [dependency injection](https://pydantic.dev/docs/ai/core-concepts/dependencies/), [function tools](https://pydantic.dev/docs/ai/tools-toolsets/tools/), [structured output](https://pydantic.dev/docs/ai/core-concepts/output/), a reusable [capability](https://pydantic.dev/docs/ai/capabilities/overview/) bundling the customer context, and an [on-demand capability](https://pydantic.dev/docs/ai/capabilities/on-demand/) the model loads only when the conversation calls for it:

```
from dataclasses import dataclass

from pydantic import BaseModel, Field

from pydantic_ai import Agent, Capability, RunContext

from bank_database import DatabaseConn

@dataclass
class SupportDependencies:  # inject any client: DB pools, HTTP APIs, user info
    customer_id: int
    db: DatabaseConn

class SupportOutput(BaseModel):
    support_advice: str = Field(description='Advice returned to the customer')
    block_card: bool = Field(description="Whether to block the customer's card")
    risk: int = Field(description='Risk level of query', ge=0, le=10)

customer_context = Capability[SupportDependencies](  # a reusable unit of tools + instructions
    id='customer-context',
    description="Who the customer is and what's on their account.",
)

@customer_context.instructions
async def add_customer_name(ctx: RunContext[SupportDependencies]) -> str:
    customer_name = await ctx.deps.db.customer_name(id=ctx.deps.customer_id)
    return f"The customer's name is {customer_name!r}"

@customer_context.tool  # signature and docstring become the tool schema the LLM sees
async def customer_balance(
    ctx: RunContext[SupportDependencies], include_pending: bool
) -> float:
    """Returns the customer's current account balance."""
    return await ctx.deps.db.customer_balance(
        id=ctx.deps.customer_id,
        include_pending=include_pending,
    )

refunds = Capability[SupportDependencies](  # deferred: loads on demand, like a skill
    id='refunds',
    description='Refund eligibility and refund status.',
    defer_loading=True,
)

@refunds.tool
async def refund_status(ctx: RunContext[SupportDependencies]) -> str:
    """Look up the refund status for the customer's most recent charge."""
    return await ctx.deps.db.refund_status(id=ctx.deps.customer_id)

support_agent = Agent(
    'openai:gpt-6-sol',
    deps_type=SupportDependencies,
    output_type=SupportOutput,  # the run returns a validated SupportOutput, typed as such
    instructions=(
        'You are a support agent in our bank, give the '
        'customer support and judge the risk level of their query.'
    ),
    capabilities=[customer_context, refunds],
)

...  # in a real use case: more tools, longer instructions

async def main():
    deps = SupportDependencies(customer_id=123, db=DatabaseConn())
    result = await support_agent.run('What is my balance?', deps=deps)
    print(result.output)
    """
    support_advice='Hello John, your current account balance, including pending transactions, is $123.45.' block_card=False risk=1
    """

    result = await support_agent.run('I just lost my card!', deps=deps)
    print(result.output)
    """
    support_advice="I'm sorry to hear that, John. We are temporarily blocking your card to prevent unauthorized transactions." block_card=True risk=8
    """

    result = await support_agent.run(  # the model loads `refunds` on demand, then answers
        'Was I refunded for the duplicate charge on my last statement?', deps=deps
    )
    print(result.output)
    """
    support_advice='Good news, John: the duplicate charge on your last statement was refunded on 2026-05-01.' block_card=False risk=1
    """
```

For the annotated walkthrough and Logfire tracing, see the [same example in the docs](https://pydantic.dev/docs/ai/overview/#putting-it-together-a-bank-support-agent).

## Next Steps

- [Install Pydantic AI](https://pydantic.dev/docs/ai/overview/install/) and put your own coding agent to work: install the [Pydantic AI skill](https://pydantic.dev/docs/ai/overview/coding-agent-skills/), point it at the [examples](https://pydantic.dev/docs/ai/examples/setup/) and the [Harness index](https://pydantic.dev/docs/ai/harness/), and tell it what you'd like to build. No API key needed to start (there's a built-in [`'test'` model](https://pydantic.dev/docs/ai/guides/testing/#unit-testing-with-testmodel)), and the [Pydantic AI Gateway](https://pydantic.dev/docs/ai/overview/gateway/) is one key for every model when you're ready.
- See what your agent did: [instrument it](https://pydantic.dev/docs/ai/integrations/logfire/) with one line of setup, and every model call and tool call shows up. It's standard OpenTelemetry: [Pydantic Logfire](https://pydantic.dev/logfire?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai), which has a [free tier](https://pydantic.dev/pricing/) (no credit card; sign up with just a GitHub account), is the easiest way to look, any OTLP backend works.
- Read the [docs](https://pydantic.dev/docs/ai/core-concepts/agent/) and the [API reference](https://pydantic.dev/docs/ai/api/pydantic-ai/agent/).
- Give your agent its batteries: [Pydantic AI Harness](https://pydantic.dev/docs/ai/harness/).
- Join [Slack](https://logfire.pydantic.dev/docs/join-slack/) or file an issue on [GitHub](https://github.com/pydantic/pydantic-ai/issues).

## Part of the Pydantic Stack

Everything you need to ship production-grade AI agents:

- [Pydantic AI](https://pydantic.dev/pydantic-ai?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai): the type-safe AI SDK
- [Pydantic AI Harness](https://pydantic.dev/docs/ai/harness/): the official capability library and harness, from single capabilities to complete agents
- [Pydantic Logfire](https://pydantic.dev/logfire?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai): AI-first, full-stack observability
- [Pydantic AI Gateway](https://pydantic.dev/ai-gateway?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai): one key for every model, with cost monitoring and spending limits
- [Pydantic Evals](https://pydantic.dev/docs/ai/evals/evals/): evaluate any Python function, agents included, with [production evals on Logfire](https://pydantic.dev/logfire/evals?utm_source=github&utm_medium=readme&utm_campaign=pydantic-ai)
- [Pydantic Graph](https://pydantic.dev/docs/ai/graph/graph/): typed graph control flow
- [genai-prices](https://github.com/pydantic/genai-prices): model pricing data, kept current
- [Monty](https://github.com/pydantic/monty): a sandboxed Python interpreter for model-written code

## Project links

Data verified by PyPI on Oct 3, 2026

Data provided by the project maintainers, verified at the time the release was uploaded to PyPI.

- [Changelog](https://github.com/pydantic/pydantic-ai/releases)
- [Source](https://github.com/pydantic/pydantic-ai)

- [Documentation](https://pydantic.dev/docs/ai/)
- [Homepage](https://pydantic.dev/docs/ai/)

## Key dates

PyPI data

Data sourced directly from PyPI's database.

- **Released:** about 16 hours ago

Latest release

## Owner

PyPI data

Data sourced directly from PyPI's database.

- [Pydantic](https://pypi.org/org/pydantic/)

## 2 maintainers

PyPI data

Data sourced directly from PyPI's database.

[![Avatar for dmontagu from gravatar.com](https://pypi-camo.freetls.fastly.net/90455d378e961216f2e250c01689fdaad0d134d7/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f31366538633330396130343164653630383032363965356665613736336139313f73697a653d3335)dmontagu](https://pypi.org/user/dmontagu/) [![Avatar for samuelcolvin from gravatar.com](https://pypi-camo.freetls.fastly.net/86d89f15dca5b7a3dd27fa9d975c987b57d89b66/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f61386235373736393965653865656463383639613733356464353231633838653f73697a653d3335)samuelcolvin](https://pypi.org/user/samuelcolvin/)

## Credits

**Author:** [Douwe Maan](mailto:douwe@pydantic.dev)

## GitHub Statistics

Data verified by PyPI on Oct 3, 2026

The GitHub source repository was provided by the project maintainers and verified by PyPI at the time of upload. Stars, forks, and open issues/PRs are derived from that repository and have not been independently verified.

- [Repository](https://github.com/pydantic/pydantic-ai)
- [Stars:\\
**20388**](https://github.com/pydantic/pydantic-ai/stargazers)
- [Forks:\\
**2855**](https://github.com/pydantic/pydantic-ai/network/members)
- [Open issues:\\
**973**](https://github.com/pydantic/pydantic-ai/issues)
- [Open PRs:\\
**401**](https://github.com/pydantic/pydantic-ai/pulls)

## License expression [About license expressions](https://spdx.github.io/spdx-spec/v3.0.1/annexes/spdx-license-expressions/)

MIT


[View SPDX License List](https://spdx.org/licenses/)

## Requires

**Python** >=3.10

## Provides Extra

`ag-ui``bedrock``bedrock-mantle``cohere``dbos``duckduckgo``exa``examples``google-realtime``groq``huggingface``mcp-tasks``mistral``openai-realtime``openrouter``prefect``realtime``retries``sentence-transformers``spec``tavily``temporal``typesafe``ui``voyageai``web-fetch``xai``xai-realtime`

## Classifiers

- Development Status
  - [5 - Production/Stable](https://pypi.org/search/?c=Development+Status+%3A%3A+5+-+Production%2FStable)
- Framework
  - [Pydantic](https://pypi.org/search/?c=Framework+%3A%3A+Pydantic)
  - [Pydantic :: 2](https://pypi.org/search/?c=Framework+%3A%3A+Pydantic+%3A%3A+2)
- Intended Audience
  - [Developers](https://pypi.org/search/?c=Intended+Audience+%3A%3A+Developers)
  - [Information Technology](https://pypi.org/search/?c=Intended+Audience+%3A%3A+Information+Technology)
- Operating System
  - [OS Independent](https://pypi.org/search/?c=Operating+System+%3A%3A+OS+Independent)
- Programming Language
  - [Python](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python)
  - [Python :: 3](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3)
  - [Python :: 3 :: Only](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3+%3A%3A+Only)
  - [Python :: 3.10](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.10)
  - [Python :: 3.11](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.11)
  - [Python :: 3.12](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.12)
  - [Python :: 3.13](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.13)
  - [Python :: 3.14](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.14)
- Topic
  - [Internet](https://pypi.org/search/?c=Topic+%3A%3A+Internet)
  - [Scientific/Engineering :: Artificial Intelligence](https://pypi.org/search/?c=Topic+%3A%3A+Scientific%2FEngineering+%3A%3A+Artificial+Intelligence)
  - [Software Development :: Libraries :: Python Modules](https://pypi.org/search/?c=Topic+%3A%3A+Software+Development+%3A%3A+Libraries+%3A%3A+Python+Modules)

[Report project as malware](https://pypi.org/project/pydantic-ai/submit-malware-report/)

## Metadata

## Project links

Data verified by PyPI on Oct 3, 2026

Data provided by the project maintainers, verified at the time the release was uploaded to PyPI.

- [Changelog](https://github.com/pydantic/pydantic-ai/releases)
- [Source](https://github.com/pydantic/pydantic-ai)

- [Documentation](https://pydantic.dev/docs/ai/)
- [Homepage](https://pydantic.dev/docs/ai/)

## Key dates

PyPI data

Data sourced directly from PyPI's database.

- **Released:** about 16 hours ago

Latest release

## Owner

PyPI data

Data sourced directly from PyPI's database.

- [Pydantic](https://pypi.org/org/pydantic/)

## 2 maintainers

PyPI data

Data sourced directly from PyPI's database.

[![Avatar for dmontagu from gravatar.com](https://pypi-camo.freetls.fastly.net/90455d378e961216f2e250c01689fdaad0d134d7/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f31366538633330396130343164653630383032363965356665613736336139313f73697a653d3335)dmontagu](https://pypi.org/user/dmontagu/) [![Avatar for samuelcolvin from gravatar.com](https://pypi-camo.freetls.fastly.net/86d89f15dca5b7a3dd27fa9d975c987b57d89b66/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f61386235373736393965653865656463383639613733356464353231633838653f73697a653d3335)samuelcolvin](https://pypi.org/user/samuelcolvin/)

## Credits

**Author:** [Douwe Maan](mailto:douwe@pydantic.dev)

## GitHub Statistics

Data verified by PyPI on Oct 3, 2026

The GitHub source repository was provided by the project maintainers and verified by PyPI at the time of upload. Stars, forks, and open issues/PRs are derived from that repository and have not been independently verified.

- [Repository](https://github.com/pydantic/pydantic-ai)
- [Stars:\\
**20388**](https://github.com/pydantic/pydantic-ai/stargazers)
- [Forks:\\
**2855**](https://github.com/pydantic/pydantic-ai/network/members)
- [Open issues:\\
**973**](https://github.com/pydantic/pydantic-ai/issues)
- [Open PRs:\\
**401**](https://github.com/pydantic/pydantic-ai/pulls)

## License expression [About license expressions](https://spdx.github.io/spdx-spec/v3.0.1/annexes/spdx-license-expressions/)

MIT


[View SPDX License List](https://spdx.org/licenses/)

## Requires

**Python** >=3.10

## Provides Extra

`ag-ui``bedrock``bedrock-mantle``cohere``dbos``duckduckgo``exa``examples``google-realtime``groq``huggingface``mcp-tasks``mistral``openai-realtime``openrouter``prefect``realtime``retries``sentence-transformers``spec``tavily``temporal``typesafe``ui``voyageai``web-fetch``xai``xai-realtime`

## Classifiers

- Development Status
  - [5 - Production/Stable](https://pypi.org/search/?c=Development+Status+%3A%3A+5+-+Production%2FStable)
- Framework
  - [Pydantic](https://pypi.org/search/?c=Framework+%3A%3A+Pydantic)
  - [Pydantic :: 2](https://pypi.org/search/?c=Framework+%3A%3A+Pydantic+%3A%3A+2)
- Intended Audience
  - [Developers](https://pypi.org/search/?c=Intended+Audience+%3A%3A+Developers)
  - [Information Technology](https://pypi.org/search/?c=Intended+Audience+%3A%3A+Information+Technology)
- Operating System
  - [OS Independent](https://pypi.org/search/?c=Operating+System+%3A%3A+OS+Independent)
- Programming Language
  - [Python](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python)
  - [Python :: 3](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3)
  - [Python :: 3 :: Only](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3+%3A%3A+Only)
  - [Python :: 3.10](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.10)
  - [Python :: 3.11](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.11)
  - [Python :: 3.12](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.12)
  - [Python :: 3.13](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.13)
  - [Python :: 3.14](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.14)
- Topic
  - [Internet](https://pypi.org/search/?c=Topic+%3A%3A+Internet)
  - [Scientific/Engineering :: Artificial Intelligence](https://pypi.org/search/?c=Topic+%3A%3A+Scientific%2FEngineering+%3A%3A+Artificial+Intelligence)
  - [Software Development :: Libraries :: Python Modules](https://pypi.org/search/?c=Topic+%3A%3A+Software+Development+%3A%3A+Libraries+%3A%3A+Python+Modules)

[Report project as malware](https://pypi.org/project/pydantic-ai/submit-malware-report/)

## Release files for pydantic-ai 2.54.0

For a detailed explanation of source distributions (sdists) and built distributions (wheels), please see the [package formats documentation](https://packaging.python.org/en/latest/discussions/package-formats/#package-formats "External link").

### Source distribution (sdist)

| File | Size | Uploaded |  |
| --- | --- | --- | --- |
| [pydantic\_ai-2.54.0.tar.gz](https://files.pythonhosted.org/packages/91/ba/fe435fa9f06b5a78e72d2ba44918656e5824ccfc739700e141f3e2a386d8/pydantic_ai-2.54.0.tar.gz) | 28.0 kB | about 16 hours ago | [Details](https://pypi.org/project/pydantic-ai/#pydantic_ai-2.54.0.tar.gz) |

Source distribution for pydantic-ai 2.54.0

* * *

### Built distribution (wheel)

| File | Interpreter | ABI | Platform | [Reset](https://pypi.org/project/pydantic-ai/#files) |
| --- | --- | --- | --- | --- |
| [pydantic\_ai-2.54.0-py3-none-any.whl](https://files.pythonhosted.org/packages/5d/74/92ebc5f809e1791bc909dc04fb032a885c1e2f32ab69ce6ee9d661d68eaf/pydantic_ai-2.54.0-py3-none-any.whl)10.2 kBabout 16 hours ago | Python 3 | none | any | [Details](https://pypi.org/project/pydantic-ai/#pydantic_ai-2.54.0-py3-none-any.whl) |

Table of built distributions (wheels) for pydantic-ai 2.54.0

* * *

**Total release size:** 38.1 kB


## [Release files](https://pypi.org/project/pydantic-ai/\#files)  / pydantic\_ai-2.54.0.tar.gz

| Download URL | [pydantic\_ai-2.54.0.tar.gz](https://files.pythonhosted.org/packages/91/ba/fe435fa9f06b5a78e72d2ba44918656e5824ccfc739700e141f3e2a386d8/pydantic_ai-2.54.0.tar.gz) |
| Size | 28.0 kB |
| Tags | Source |
| SHA-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            8c3e4a08a9e5a4aa28c80ca40e064fe1115dfcc9ffdd2faa3818046ab6766467<br>` |
| BLAKE2b-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            91bafe435fa9f06b5a78e72d2ba44918656e5824ccfc739700e141f3e2a386d8<br>` |
| Upload date | about 16 hours ago |
| Uploaded using Trusted Publishing? <br>[What is trusted publishing?](https://docs.pypi.org/trusted-publishers/) | Yes |
| Uploaded via | `twine/6.1.0 CPython/3.13.13` |

### Provenance

**Provenance** describes where a file came from. On PyPI, provenance is shared via **attestations**, which provide a verifiable record of the build or publishing details. [View details, limitations and caveats.](https://docs.pypi.org/attestations/)

![](https://pypi.org/static/images/github.683a0246.svg)![](https://pypi.org/static/images/pypi-attestation-cube.1cfdb012.svg)

#### [PyPI Publish](https://docs.pypi.org/attestations/publish/v1) Attestation

PyPI verified that this artifact, at this checksum, originated from the publisher listed below.

**Signed by GitHub Actions, verified by PyPI on Oct 3, 2026.**

[Transparency log](https://search.sigstore.dev/?logIndex=3067848766 "Sigstore transparency entry")

##### Identity

Publishing platform
GitHub Actions

Publishing repository [github.com/pydantic/pydantic-ai](https://github.com/pydantic/pydantic-ai)
Publishing commit [github.com/pydantic/pydantic-ai/tree/66951321b89587235f432281eba909a30a585ffd](https://github.com/pydantic/pydantic-ai/tree/66951321b89587235f432281eba909a30a585ffd)

##### Workflow

Publishing configuration [github.com/pydantic/pydantic-ai/blob/66951321b89587235f432281eba909a30a585ffd/.github/workflows/ci.yml](https://github.com/pydantic/pydantic-ai/blob/66951321b89587235f432281eba909a30a585ffd/.github/workflows/ci.yml)
Publishing logs [github.com/pydantic/pydantic-ai/actions/runs/37092926449/attempts/1](https://github.com/pydantic/pydantic-ai/actions/runs/37092926449/attempts/1)

##### Artifact

Subject`pydantic_ai-2.54.0.tar.gz`SHA-256 checksum`
              8c3e4a08a9e5a4aa28c80ca40e064fe1115dfcc9ffdd2faa3818046ab6766467

` [Verifying attestations](https://docs.pypi.org/attestations/consuming-attestations/)

## [Release files](https://pypi.org/project/pydantic-ai/\#files)  / pydantic\_ai-2.54.0-py3-none-any.whl

| Download URL | [pydantic\_ai-2.54.0-py3-none-any.whl](https://files.pythonhosted.org/packages/5d/74/92ebc5f809e1791bc909dc04fb032a885c1e2f32ab69ce6ee9d661d68eaf/pydantic_ai-2.54.0-py3-none-any.whl) |
| Size | 10.2 kB |
| Tags | Python 3 |
| SHA-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            c69ad15501e49a8584ce24bc89c4fa7bd67e15a8294fbeb28e3d017fe6480119<br>` |
| BLAKE2b-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            5d7492ebc5f809e1791bc909dc04fb032a885c1e2f32ab69ce6ee9d661d68eaf<br>` |
| Upload date | about 16 hours ago |
| Uploaded using Trusted Publishing? <br>[What is trusted publishing?](https://docs.pypi.org/trusted-publishers/) | Yes |
| Uploaded via | `twine/6.1.0 CPython/3.13.13` |

### Provenance

**Provenance** describes where a file came from. On PyPI, provenance is shared via **attestations**, which provide a verifiable record of the build or publishing details. [View details, limitations and caveats.](https://docs.pypi.org/attestations/)

![](https://pypi.org/static/images/github.683a0246.svg)![](https://pypi.org/static/images/pypi-attestation-cube.1cfdb012.svg)

#### [PyPI Publish](https://docs.pypi.org/attestations/publish/v1) Attestation

PyPI verified that this artifact, at this checksum, originated from the publisher listed below.

**Signed by GitHub Actions, verified by PyPI on Oct 3, 2026.**

[Transparency log](https://search.sigstore.dev/?logIndex=3067850648 "Sigstore transparency entry")

##### Identity

Publishing platform
GitHub Actions

Publishing repository [github.com/pydantic/pydantic-ai](https://github.com/pydantic/pydantic-ai)
Publishing commit [github.com/pydantic/pydantic-ai/tree/66951321b89587235f432281eba909a30a585ffd](https://github.com/pydantic/pydantic-ai/tree/66951321b89587235f432281eba909a30a585ffd)

##### Workflow

Publishing configuration [github.com/pydantic/pydantic-ai/blob/66951321b89587235f432281eba909a30a585ffd/.github/workflows/ci.yml](https://github.com/pydantic/pydantic-ai/blob/66951321b89587235f432281eba909a30a585ffd/.github/workflows/ci.yml)
Publishing logs [github.com/pydantic/pydantic-ai/actions/runs/37092926449/attempts/1](https://github.com/pydantic/pydantic-ai/actions/runs/37092926449/attempts/1)

##### Artifact

Subject`pydantic_ai-2.54.0-py3-none-any.whl`SHA-256 checksum`
              c69ad15501e49a8584ce24bc89c4fa7bd67e15a8294fbeb28e3d017fe6480119

` [Verifying attestations](https://docs.pypi.org/attestations/consuming-attestations/)

## Release history[Release notifications](https://pypi.org/help/\#project-release-notifications) \|  [RSS feed](https://pypi.org/rss/project/pydantic-ai/releases.xml)

This release

![](https://pypi.org/static/images/blue-cube.572a5bfb.svg)

[2.54.0](https://pypi.org/project/pydantic-ai/2.54.0/) This release

about 16 hours ago [2 release files](https://pypi.org/project/pydantic-ai/2.54.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.53.0](https://pypi.org/project/pydantic-ai/2.53.0/)

Oct 1, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.53.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.52.0](https://pypi.org/project/pydantic-ai/2.52.0/)

Sep 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.52.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.51.0](https://pypi.org/project/pydantic-ai/2.51.0/)

Sep 25, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.51.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.50.0](https://pypi.org/project/pydantic-ai/2.50.0/)

Sep 25, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.50.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.49.0](https://pypi.org/project/pydantic-ai/2.49.0/)

Sep 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.49.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.48.0](https://pypi.org/project/pydantic-ai/2.48.0/)

Sep 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.48.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.47.0](https://pypi.org/project/pydantic-ai/2.47.0/)

Sep 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.47.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.46.0](https://pypi.org/project/pydantic-ai/2.46.0/)

Sep 19, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.46.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.45.0](https://pypi.org/project/pydantic-ai/2.45.0/)

Sep 18, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.45.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.44.0](https://pypi.org/project/pydantic-ai/2.44.0/)

Sep 17, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.44.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.43.0](https://pypi.org/project/pydantic-ai/2.43.0/)

Sep 11, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.43.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.42.0](https://pypi.org/project/pydantic-ai/2.42.0/)

Sep 8, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.42.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.41.0](https://pypi.org/project/pydantic-ai/2.41.0/)

Sep 8, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.41.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.40.0](https://pypi.org/project/pydantic-ai/2.40.0/)

Sep 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.40.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.39.0](https://pypi.org/project/pydantic-ai/2.39.0/)

Sep 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.39.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.38.0](https://pypi.org/project/pydantic-ai/2.38.0/)

Sep 3, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.38.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.37.0](https://pypi.org/project/pydantic-ai/2.37.0/)

Aug 31, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.37.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.36.0](https://pypi.org/project/pydantic-ai/2.36.0/)

Aug 28, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.36.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.35.3](https://pypi.org/project/pydantic-ai/2.35.3/)

Aug 27, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.35.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.35.1](https://pypi.org/project/pydantic-ai/2.35.1/)

Aug 27, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.35.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.35.0](https://pypi.org/project/pydantic-ai/2.35.0/)

Aug 25, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.35.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.34.0](https://pypi.org/project/pydantic-ai/2.34.0/)

Aug 24, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.34.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.33.0](https://pypi.org/project/pydantic-ai/2.33.0/)

Aug 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.33.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.32.2](https://pypi.org/project/pydantic-ai/2.32.2/)

Aug 20, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.32.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.32.1](https://pypi.org/project/pydantic-ai/2.32.1/)

Aug 19, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.32.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.32.0](https://pypi.org/project/pydantic-ai/2.32.0/)

Aug 19, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.32.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.31.1](https://pypi.org/project/pydantic-ai/2.31.1/)

Aug 17, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.31.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.31.0](https://pypi.org/project/pydantic-ai/2.31.0/)

Aug 14, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.31.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.30.0](https://pypi.org/project/pydantic-ai/2.30.0/)

Aug 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.30.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.29.0](https://pypi.org/project/pydantic-ai/2.29.0/)

Aug 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.29.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.28.0](https://pypi.org/project/pydantic-ai/2.28.0/)

Aug 11, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.28.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.27.1](https://pypi.org/project/pydantic-ai/2.27.1/)

Aug 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.27.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.27.0](https://pypi.org/project/pydantic-ai/2.27.0/)

Aug 8, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.27.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.26.0](https://pypi.org/project/pydantic-ai/2.26.0/)

Aug 6, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.26.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.25.0](https://pypi.org/project/pydantic-ai/2.25.0/)

Aug 5, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.25.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.24.0](https://pypi.org/project/pydantic-ai/2.24.0/)

Aug 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.24.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.23.0](https://pypi.org/project/pydantic-ai/2.23.0/)

Aug 3, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.23.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.22.0](https://pypi.org/project/pydantic-ai/2.22.0/)

Jul 31, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.22.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.21.0](https://pypi.org/project/pydantic-ai/2.21.0/)

Jul 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.21.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.20.0](https://pypi.org/project/pydantic-ai/2.20.0/)

Jul 28, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.20.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.19.0](https://pypi.org/project/pydantic-ai/2.19.0/)

Jul 27, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.19.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.18.0](https://pypi.org/project/pydantic-ai/2.18.0/)

Jul 24, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.18.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.17.0](https://pypi.org/project/pydantic-ai/2.17.0/)

Jul 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.17.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.16.0](https://pypi.org/project/pydantic-ai/2.16.0/)

Jul 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.16.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.15.0](https://pypi.org/project/pydantic-ai/2.15.0/)

Jul 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.15.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.14.1](https://pypi.org/project/pydantic-ai/2.14.1/)

Jul 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.14.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.14.0](https://pypi.org/project/pydantic-ai/2.14.0/)

Jul 20, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.14.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.13.0](https://pypi.org/project/pydantic-ai/2.13.0/)

Jul 17, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.13.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.12.0](https://pypi.org/project/pydantic-ai/2.12.0/)

Jul 16, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.12.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.11.0](https://pypi.org/project/pydantic-ai/2.11.0/)

Jul 15, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.11.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.10.0](https://pypi.org/project/pydantic-ai/2.10.0/)

Jul 14, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.10.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.9.1](https://pypi.org/project/pydantic-ai/2.9.1/)

Jul 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.9.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.9.0](https://pypi.org/project/pydantic-ai/2.9.0/)

Jul 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.9.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.8.0](https://pypi.org/project/pydantic-ai/2.8.0/)

Jul 9, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.8.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.7.0](https://pypi.org/project/pydantic-ai/2.7.0/)

Jul 8, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.7.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.6.0](https://pypi.org/project/pydantic-ai/2.6.0/)

Jul 7, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.6.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.5.1](https://pypi.org/project/pydantic-ai/2.5.1/)

Jul 6, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.5.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.5.0](https://pypi.org/project/pydantic-ai/2.5.0/)

Jul 3, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.5.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.4.0](https://pypi.org/project/pydantic-ai/2.4.0/)

Jul 2, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.4.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.3.0](https://pypi.org/project/pydantic-ai/2.3.0/)

Jul 1, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.3.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.2.0](https://pypi.org/project/pydantic-ai/2.2.0/)

Jun 30, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.1.0](https://pypi.org/project/pydantic-ai/2.1.0/)

Jun 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.0.0](https://pypi.org/project/pydantic-ai/2.0.0/)

Jun 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b7](https://pypi.org/project/pydantic-ai/2.0.0b7/)

Jun 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b6](https://pypi.org/project/pydantic-ai/2.0.0b6/)

Jun 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b5](https://pypi.org/project/pydantic-ai/2.0.0b5/)

Jun 2, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b4](https://pypi.org/project/pydantic-ai/2.0.0b4/)

May 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b3](https://pypi.org/project/pydantic-ai/2.0.0b3/)

May 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b2](https://pypi.org/project/pydantic-ai/2.0.0b2/)

May 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[2.0.0b1](https://pypi.org/project/pydantic-ai/2.0.0b1/)

May 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/2.0.0b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.7](https://pypi.org/project/pydantic-ai/1.107.7/)

Sep 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.6](https://pypi.org/project/pydantic-ai/1.107.6/)

Sep 17, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.5](https://pypi.org/project/pydantic-ai/1.107.5/)

Aug 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.4](https://pypi.org/project/pydantic-ai/1.107.4/)

Aug 11, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.2](https://pypi.org/project/pydantic-ai/1.107.2/)

Aug 7, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.1](https://pypi.org/project/pydantic-ai/1.107.1/)

Jul 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.107.0](https://pypi.org/project/pydantic-ai/1.107.0/)

Jun 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.107.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.106.0](https://pypi.org/project/pydantic-ai/1.106.0/)

Jun 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.106.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.105.0](https://pypi.org/project/pydantic-ai/1.105.0/)

Jun 2, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.105.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.104.0](https://pypi.org/project/pydantic-ai/1.104.0/)

May 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.104.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.103.0](https://pypi.org/project/pydantic-ai/1.103.0/)

May 26, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.103.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.102.0](https://pypi.org/project/pydantic-ai/1.102.0/)

May 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.102.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.101.0](https://pypi.org/project/pydantic-ai/1.101.0/)

May 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.101.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.100.0](https://pypi.org/project/pydantic-ai/1.100.0/)

May 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.100.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.99.0](https://pypi.org/project/pydantic-ai/1.99.0/)

May 19, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.99.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.98.0](https://pypi.org/project/pydantic-ai/1.98.0/)

May 18, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.98.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.97.0](https://pypi.org/project/pydantic-ai/1.97.0/)

May 15, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.97.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.96.1](https://pypi.org/project/pydantic-ai/1.96.1/)

May 14, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.96.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.96.0](https://pypi.org/project/pydantic-ai/1.96.0/)

May 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.96.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.95.1](https://pypi.org/project/pydantic-ai/1.95.1/)

May 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.95.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.95.0](https://pypi.org/project/pydantic-ai/1.95.0/)

May 12, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.95.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.94.0](https://pypi.org/project/pydantic-ai/1.94.0/)

May 12, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.94.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.93.0](https://pypi.org/project/pydantic-ai/1.93.0/)

May 8, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.93.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.92.0](https://pypi.org/project/pydantic-ai/1.92.0/)

May 7, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.92.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.91.0](https://pypi.org/project/pydantic-ai/1.91.0/)

May 6, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.91.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.90.0](https://pypi.org/project/pydantic-ai/1.90.0/)

May 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.90.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.89.1](https://pypi.org/project/pydantic-ai/1.89.1/)

May 1, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.89.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.89.0](https://pypi.org/project/pydantic-ai/1.89.0/)

Apr 30, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.89.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.88.0](https://pypi.org/project/pydantic-ai/1.88.0/)

Apr 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.88.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.87.0](https://pypi.org/project/pydantic-ai/1.87.0/)

Apr 24, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.87.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.86.1](https://pypi.org/project/pydantic-ai/1.86.1/)

Apr 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.86.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.86.0](https://pypi.org/project/pydantic-ai/1.86.0/)

Apr 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.86.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.85.1](https://pypi.org/project/pydantic-ai/1.85.1/)

Apr 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.85.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.85.0](https://pypi.org/project/pydantic-ai/1.85.0/)

Apr 21, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.85.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.84.1](https://pypi.org/project/pydantic-ai/1.84.1/)

Apr 17, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.84.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.84.0](https://pypi.org/project/pydantic-ai/1.84.0/)

Apr 16, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.84.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.83.0](https://pypi.org/project/pydantic-ai/1.83.0/)

Apr 15, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.83.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.82.0](https://pypi.org/project/pydantic-ai/1.82.0/)

Apr 14, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.82.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.81.0](https://pypi.org/project/pydantic-ai/1.81.0/)

Apr 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.81.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.80.0](https://pypi.org/project/pydantic-ai/1.80.0/)

Apr 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.80.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.79.0](https://pypi.org/project/pydantic-ai/1.79.0/)

Apr 9, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.79.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.78.0](https://pypi.org/project/pydantic-ai/1.78.0/)

Apr 8, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.78.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.77.0](https://pypi.org/project/pydantic-ai/1.77.0/)

Apr 2, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.77.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.76.0](https://pypi.org/project/pydantic-ai/1.76.0/)

Apr 1, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.76.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.75.0](https://pypi.org/project/pydantic-ai/1.75.0/)

Mar 31, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.75.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.74.0](https://pypi.org/project/pydantic-ai/1.74.0/)

Mar 30, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.74.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.73.0](https://pypi.org/project/pydantic-ai/1.73.0/)

Mar 26, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.73.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.72.0](https://pypi.org/project/pydantic-ai/1.72.0/)

Mar 25, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.72.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.71.0](https://pypi.org/project/pydantic-ai/1.71.0/)

Mar 24, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.71.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.70.0](https://pypi.org/project/pydantic-ai/1.70.0/)

Mar 18, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.70.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.69.0](https://pypi.org/project/pydantic-ai/1.69.0/)

Mar 16, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.69.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.68.0](https://pypi.org/project/pydantic-ai/1.68.0/)

Mar 12, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.68.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.67.0](https://pypi.org/project/pydantic-ai/1.67.0/)

Mar 6, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.67.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.66.0](https://pypi.org/project/pydantic-ai/1.66.0/)

Mar 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.66.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.65.0](https://pypi.org/project/pydantic-ai/1.65.0/)

Mar 3, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.65.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.64.0](https://pypi.org/project/pydantic-ai/1.64.0/)

Mar 2, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.64.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.63.0](https://pypi.org/project/pydantic-ai/1.63.0/)

Feb 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.63.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.62.0](https://pypi.org/project/pydantic-ai/1.62.0/)

Feb 19, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.62.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.61.0](https://pypi.org/project/pydantic-ai/1.61.0/)

Feb 17, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.61.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.60.0](https://pypi.org/project/pydantic-ai/1.60.0/)

Feb 16, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.60.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.59.0](https://pypi.org/project/pydantic-ai/1.59.0/)

Feb 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.59.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.58.0](https://pypi.org/project/pydantic-ai/1.58.0/)

Feb 10, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.58.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.57.0](https://pypi.org/project/pydantic-ai/1.57.0/)

Feb 9, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.57.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.56.0](https://pypi.org/project/pydantic-ai/1.56.0/)

Feb 5, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.56.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.55.0](https://pypi.org/project/pydantic-ai/1.55.0/)

Feb 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.55.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.54.0](https://pypi.org/project/pydantic-ai/1.54.0/)

Feb 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.54.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.53.0](https://pypi.org/project/pydantic-ai/1.53.0/)

Feb 4, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.53.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.52.0](https://pypi.org/project/pydantic-ai/1.52.0/)

Feb 2, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.52.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.51.0](https://pypi.org/project/pydantic-ai/1.51.0/)

Jan 30, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.51.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.50.0](https://pypi.org/project/pydantic-ai/1.50.0/)

Jan 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.50.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.49.0](https://pypi.org/project/pydantic-ai/1.49.0/)

Jan 29, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.49.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.48.0](https://pypi.org/project/pydantic-ai/1.48.0/)

Jan 27, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.48.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.47.0](https://pypi.org/project/pydantic-ai/1.47.0/)

Jan 23, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.47.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.46.0](https://pypi.org/project/pydantic-ai/1.46.0/)

Jan 22, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.46.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.44.0](https://pypi.org/project/pydantic-ai/1.44.0/)

Jan 16, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.44.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.43.0](https://pypi.org/project/pydantic-ai/1.43.0/)

Jan 15, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.43.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.42.0](https://pypi.org/project/pydantic-ai/1.42.0/)

Jan 13, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.42.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.41.0](https://pypi.org/project/pydantic-ai/1.41.0/)

Jan 9, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.41.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.40.0](https://pypi.org/project/pydantic-ai/1.40.0/)

Jan 6, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.40.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.39.1](https://pypi.org/project/pydantic-ai/1.39.1/)

Jan 5, 2026 [2 release files](https://pypi.org/project/pydantic-ai/1.39.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.39.0](https://pypi.org/project/pydantic-ai/1.39.0/)

Dec 23, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.39.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.38.0](https://pypi.org/project/pydantic-ai/1.38.0/)

Dec 22, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.38.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.37.0](https://pypi.org/project/pydantic-ai/1.37.0/)

Dec 19, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.37.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.36.0](https://pypi.org/project/pydantic-ai/1.36.0/)

Dec 18, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.36.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.35.0](https://pypi.org/project/pydantic-ai/1.35.0/)

Dec 17, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.35.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.34.0](https://pypi.org/project/pydantic-ai/1.34.0/)

Dec 16, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.34.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.33.0](https://pypi.org/project/pydantic-ai/1.33.0/)

Dec 15, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.33.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.32.0](https://pypi.org/project/pydantic-ai/1.32.0/)

Dec 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.32.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.31.0](https://pypi.org/project/pydantic-ai/1.31.0/)

Dec 11, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.31.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.30.1](https://pypi.org/project/pydantic-ai/1.30.1/)

Dec 11, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.30.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.30.0](https://pypi.org/project/pydantic-ai/1.30.0/)

Dec 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.30.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.29.0](https://pypi.org/project/pydantic-ai/1.29.0/)

Dec 9, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.29.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.28.0](https://pypi.org/project/pydantic-ai/1.28.0/)

Dec 8, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.28.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.27.0](https://pypi.org/project/pydantic-ai/1.27.0/)

Dec 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.27.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.26.0](https://pypi.org/project/pydantic-ai/1.26.0/)

Dec 2, 2025 [1 release file](https://pypi.org/project/pydantic-ai/1.26.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.25.1](https://pypi.org/project/pydantic-ai/1.25.1/)

Nov 28, 2025 [1 release file](https://pypi.org/project/pydantic-ai/1.25.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.25.0](https://pypi.org/project/pydantic-ai/1.25.0/)

Nov 28, 2025 [1 release file](https://pypi.org/project/pydantic-ai/1.25.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.24.0](https://pypi.org/project/pydantic-ai/1.24.0/)

Nov 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.24.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.23.0](https://pypi.org/project/pydantic-ai/1.23.0/)

Nov 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.23.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.22.0](https://pypi.org/project/pydantic-ai/1.22.0/)

Nov 21, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.22.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.21.0](https://pypi.org/project/pydantic-ai/1.21.0/)

Nov 20, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.21.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.20.0](https://pypi.org/project/pydantic-ai/1.20.0/)

Nov 18, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.20.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.19.0](https://pypi.org/project/pydantic-ai/1.19.0/)

Nov 17, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.19.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.18.0](https://pypi.org/project/pydantic-ai/1.18.0/)

Nov 14, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.18.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.17.0](https://pypi.org/project/pydantic-ai/1.17.0/)

Nov 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.17.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.16.0](https://pypi.org/project/pydantic-ai/1.16.0/)

Nov 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.16.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.15.0](https://pypi.org/project/pydantic-ai/1.15.0/)

Nov 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.15.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.14.1](https://pypi.org/project/pydantic-ai/1.14.1/)

Nov 11, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.14.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.14.0](https://pypi.org/project/pydantic-ai/1.14.0/)

Nov 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.14.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.13.0](https://pypi.org/project/pydantic-ai/1.13.0/)

Nov 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.13.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.12.0](https://pypi.org/project/pydantic-ai/1.12.0/)

Nov 6, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.12.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.11.1](https://pypi.org/project/pydantic-ai/1.11.1/)

Nov 5, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.11.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.11.0](https://pypi.org/project/pydantic-ai/1.11.0/)

Nov 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.11.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.10.0](https://pypi.org/project/pydantic-ai/1.10.0/)

Nov 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.10.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.9.1](https://pypi.org/project/pydantic-ai/1.9.1/)

Oct 30, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.9.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.9.0](https://pypi.org/project/pydantic-ai/1.9.0/)

Oct 29, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.9.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.8.0](https://pypi.org/project/pydantic-ai/1.8.0/)

Oct 29, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.8.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.7.0](https://pypi.org/project/pydantic-ai/1.7.0/)

Oct 27, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.7.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.6.0](https://pypi.org/project/pydantic-ai/1.6.0/)

Oct 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.6.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.0](https://pypi.org/project/pydantic-ai/1.5.0/)

Oct 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.5.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.4.0](https://pypi.org/project/pydantic-ai/1.4.0/)

Oct 23, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.4.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.3.0](https://pypi.org/project/pydantic-ai/1.3.0/)

Oct 22, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.3.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.2.1](https://pypi.org/project/pydantic-ai/1.2.1/)

Oct 20, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.2.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.2.0](https://pypi.org/project/pydantic-ai/1.2.0/)

Oct 20, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.0](https://pypi.org/project/pydantic-ai/1.1.0/)

Oct 15, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.18](https://pypi.org/project/pydantic-ai/1.0.18/)

Oct 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.18/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.17](https://pypi.org/project/pydantic-ai/1.0.17/)

Oct 9, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.17/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.16](https://pypi.org/project/pydantic-ai/1.0.16/)

Oct 8, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.16/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.15](https://pypi.org/project/pydantic-ai/1.0.15/)

Oct 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.15/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.14](https://pypi.org/project/pydantic-ai/1.0.14/)

Oct 2, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.14/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.13](https://pypi.org/project/pydantic-ai/1.0.13/)

Oct 1, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.13/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.12](https://pypi.org/project/pydantic-ai/1.0.12/)

Sep 30, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.12/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.11](https://pypi.org/project/pydantic-ai/1.0.11/)

Sep 29, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.10](https://pypi.org/project/pydantic-ai/1.0.10/)

Sep 19, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.9](https://pypi.org/project/pydantic-ai/1.0.9/)

Sep 18, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.8](https://pypi.org/project/pydantic-ai/1.0.8/)

Sep 16, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.7](https://pypi.org/project/pydantic-ai/1.0.7/)

Sep 15, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.6](https://pypi.org/project/pydantic-ai/1.0.6/)

Sep 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.5](https://pypi.org/project/pydantic-ai/1.0.5/)

Sep 11, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.4](https://pypi.org/project/pydantic-ai/1.0.4/)

Sep 11, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.3](https://pypi.org/project/pydantic-ai/1.0.3/)

Sep 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.2](https://pypi.org/project/pydantic-ai/1.0.2/)

Sep 8, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.1](https://pypi.org/project/pydantic-ai/1.0.1/)

Sep 5, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.0](https://pypi.org/project/pydantic-ai/1.0.0/)

Sep 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[1.0.0b1](https://pypi.org/project/pydantic-ai/1.0.0b1/)

Aug 30, 2025 [2 release files](https://pypi.org/project/pydantic-ai/1.0.0b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.8.1](https://pypi.org/project/pydantic-ai/0.8.1/)

Aug 29, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.8.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.8.0](https://pypi.org/project/pydantic-ai/0.8.0/)

Aug 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.8.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.6](https://pypi.org/project/pydantic-ai/0.7.6/)

Aug 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.5](https://pypi.org/project/pydantic-ai/0.7.5/)

Aug 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.4](https://pypi.org/project/pydantic-ai/0.7.4/)

Aug 20, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.3](https://pypi.org/project/pydantic-ai/0.7.3/)

Aug 19, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.2](https://pypi.org/project/pydantic-ai/0.7.2/)

Aug 14, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.1](https://pypi.org/project/pydantic-ai/0.7.1/)

Aug 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.7.0](https://pypi.org/project/pydantic-ai/0.7.0/)

Aug 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.7.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.6.2](https://pypi.org/project/pydantic-ai/0.6.2/)

Aug 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.6.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.6.1](https://pypi.org/project/pydantic-ai/0.6.1/)

Aug 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.6.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.6.0](https://pypi.org/project/pydantic-ai/0.6.0/)

Aug 6, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.6.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.5.1](https://pypi.org/project/pydantic-ai/0.5.1/)

Aug 6, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.5.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.5.0](https://pypi.org/project/pydantic-ai/0.5.0/)

Aug 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.5.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.11](https://pypi.org/project/pydantic-ai/0.4.11/)

Aug 1, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.10](https://pypi.org/project/pydantic-ai/0.4.10/)

Jul 30, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.9](https://pypi.org/project/pydantic-ai/0.4.9/)

Jul 28, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.8](https://pypi.org/project/pydantic-ai/0.4.8/)

Jul 28, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.7](https://pypi.org/project/pydantic-ai/0.4.7/)

Jul 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.6](https://pypi.org/project/pydantic-ai/0.4.6/)

Jul 23, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.5](https://pypi.org/project/pydantic-ai/0.4.5/)

Jul 22, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.4](https://pypi.org/project/pydantic-ai/0.4.4/)

Jul 18, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.3](https://pypi.org/project/pydantic-ai/0.4.3/)

Jul 16, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.2](https://pypi.org/project/pydantic-ai/0.4.2/)

Jul 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.1](https://pypi.org/project/pydantic-ai/0.4.1/)

Jul 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.4.0](https://pypi.org/project/pydantic-ai/0.4.0/)

Jul 8, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.4.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.7](https://pypi.org/project/pydantic-ai/0.3.7/)

Jul 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.6](https://pypi.org/project/pydantic-ai/0.3.6/)

Jul 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.5](https://pypi.org/project/pydantic-ai/0.3.5/)

Jun 30, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.4](https://pypi.org/project/pydantic-ai/0.3.4/)

Jun 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.3](https://pypi.org/project/pydantic-ai/0.3.3/)

Jun 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.2](https://pypi.org/project/pydantic-ai/0.3.2/)

Jun 21, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.1](https://pypi.org/project/pydantic-ai/0.3.1/)

Jun 18, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.3.0](https://pypi.org/project/pydantic-ai/0.3.0/)

Jun 17, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.3.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.20](https://pypi.org/project/pydantic-ai/0.2.20/)

Jun 17, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.20/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.19](https://pypi.org/project/pydantic-ai/0.2.19/)

Jun 16, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.19/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.18](https://pypi.org/project/pydantic-ai/0.2.18/)

Jun 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.18/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.17](https://pypi.org/project/pydantic-ai/0.2.17/)

Jun 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.17/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.16](https://pypi.org/project/pydantic-ai/0.2.16/)

Jun 8, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.16/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.15](https://pypi.org/project/pydantic-ai/0.2.15/)

Jun 5, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.15/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.14](https://pypi.org/project/pydantic-ai/0.2.14/)

Jun 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.14/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.13](https://pypi.org/project/pydantic-ai/0.2.13/)

Jun 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.13/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.12](https://pypi.org/project/pydantic-ai/0.2.12/)

May 29, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.12/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.11](https://pypi.org/project/pydantic-ai/0.2.11/)

May 28, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.10](https://pypi.org/project/pydantic-ai/0.2.10/)

May 27, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.9](https://pypi.org/project/pydantic-ai/0.2.9/)

May 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.8](https://pypi.org/project/pydantic-ai/0.2.8/)

May 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.7](https://pypi.org/project/pydantic-ai/0.2.7/)

May 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.6](https://pypi.org/project/pydantic-ai/0.2.6/)

May 21, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.5](https://pypi.org/project/pydantic-ai/0.2.5/)

May 20, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.4](https://pypi.org/project/pydantic-ai/0.2.4/)

May 14, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.3](https://pypi.org/project/pydantic-ai/0.2.3/)

May 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.2](https://pypi.org/project/pydantic-ai/0.2.2/)

May 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.1](https://pypi.org/project/pydantic-ai/0.2.1/)

May 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.0](https://pypi.org/project/pydantic-ai/0.2.0/)

May 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Yanked](https://pypi.org/help/#yanked "Release yanked on May 12, 2025")

[0.1.12](https://pypi.org/project/pydantic-ai/0.1.12/)

May 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.12/#files)

**Yanked reason:** Had a breaking change and we forgot to increment minor

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.11](https://pypi.org/project/pydantic-ai/0.1.11/)

May 10, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.10](https://pypi.org/project/pydantic-ai/0.1.10/)

May 6, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.9](https://pypi.org/project/pydantic-ai/0.1.9/)

May 2, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.8](https://pypi.org/project/pydantic-ai/0.1.8/)

Apr 28, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.7](https://pypi.org/project/pydantic-ai/0.1.7/)

Apr 28, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.6](https://pypi.org/project/pydantic-ai/0.1.6/)

Apr 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.5](https://pypi.org/project/pydantic-ai/0.1.5/)

Apr 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.4](https://pypi.org/project/pydantic-ai/0.1.4/)

Apr 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.3](https://pypi.org/project/pydantic-ai/0.1.3/)

Apr 18, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.2](https://pypi.org/project/pydantic-ai/0.1.2/)

Apr 17, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.1](https://pypi.org/project/pydantic-ai/0.1.1/)

Apr 16, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.0](https://pypi.org/project/pydantic-ai/0.1.0/)

Apr 15, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.55](https://pypi.org/project/pydantic-ai/0.0.55/)

Apr 9, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.55/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.54](https://pypi.org/project/pydantic-ai/0.0.54/)

Apr 9, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.54/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.53](https://pypi.org/project/pydantic-ai/0.0.53/)

Apr 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.53/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.52](https://pypi.org/project/pydantic-ai/0.0.52/)

Apr 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.52/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.51](https://pypi.org/project/pydantic-ai/0.0.51/)

Apr 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.51/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.50](https://pypi.org/project/pydantic-ai/0.0.50/)

Apr 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.50/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.49](https://pypi.org/project/pydantic-ai/0.0.49/)

Apr 1, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.49/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.48](https://pypi.org/project/pydantic-ai/0.0.48/)

Mar 31, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.48/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.47](https://pypi.org/project/pydantic-ai/0.0.47/)

Mar 31, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.47/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.46](https://pypi.org/project/pydantic-ai/0.0.46/)

Mar 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.46/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.45](https://pypi.org/project/pydantic-ai/0.0.45/)

Mar 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.45/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.44](https://pypi.org/project/pydantic-ai/0.0.44/)

Mar 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.44/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.43](https://pypi.org/project/pydantic-ai/0.0.43/)

Mar 21, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.43/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.42](https://pypi.org/project/pydantic-ai/0.0.42/)

Mar 19, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.42/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.41](https://pypi.org/project/pydantic-ai/0.0.41/)

Mar 17, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.41/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.40](https://pypi.org/project/pydantic-ai/0.0.40/)

Mar 15, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.40/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.39](https://pypi.org/project/pydantic-ai/0.0.39/)

Mar 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.39/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.38](https://pypi.org/project/pydantic-ai/0.0.38/)

Mar 13, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.38/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.37](https://pypi.org/project/pydantic-ai/0.0.37/)

Mar 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.37/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.36](https://pypi.org/project/pydantic-ai/0.0.36/)

Mar 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.36/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.35](https://pypi.org/project/pydantic-ai/0.0.35/)

Mar 5, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.35/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.34](https://pypi.org/project/pydantic-ai/0.0.34/)

Mar 5, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.34/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.33](https://pypi.org/project/pydantic-ai/0.0.33/)

Mar 5, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.33/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.32](https://pypi.org/project/pydantic-ai/0.0.32/)

Mar 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.32/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.31](https://pypi.org/project/pydantic-ai/0.0.31/)

Mar 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.31/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.30](https://pypi.org/project/pydantic-ai/0.0.30/)

Feb 28, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.30/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.29](https://pypi.org/project/pydantic-ai/0.0.29/)

Feb 27, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.29/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.28](https://pypi.org/project/pydantic-ai/0.0.28/)

Feb 27, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.28/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.27](https://pypi.org/project/pydantic-ai/0.0.27/)

Feb 26, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.27/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.26](https://pypi.org/project/pydantic-ai/0.0.26/)

Feb 25, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.26/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.25](https://pypi.org/project/pydantic-ai/0.0.25/)

Feb 24, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.25/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.24](https://pypi.org/project/pydantic-ai/0.0.24/)

Feb 12, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.24/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.23](https://pypi.org/project/pydantic-ai/0.0.23/)

Feb 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.23/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.22](https://pypi.org/project/pydantic-ai/0.0.22/)

Feb 4, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.22/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.21](https://pypi.org/project/pydantic-ai/0.0.21/)

Jan 30, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.21/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.20](https://pypi.org/project/pydantic-ai/0.0.20/)

Jan 23, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.20/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.19](https://pypi.org/project/pydantic-ai/0.0.19/)

Jan 15, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.19/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.18](https://pypi.org/project/pydantic-ai/0.0.18/)

Jan 7, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.18/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.17](https://pypi.org/project/pydantic-ai/0.0.17/)

Jan 3, 2025 [2 release files](https://pypi.org/project/pydantic-ai/0.0.17/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.16](https://pypi.org/project/pydantic-ai/0.0.16/)

Dec 30, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.16/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.15](https://pypi.org/project/pydantic-ai/0.0.15/)

Dec 23, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.15/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.14](https://pypi.org/project/pydantic-ai/0.0.14/)

Dec 19, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.14/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.13](https://pypi.org/project/pydantic-ai/0.0.13/)

Dec 16, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.13/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.12](https://pypi.org/project/pydantic-ai/0.0.12/)

Dec 8, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.12/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.11](https://pypi.org/project/pydantic-ai/0.0.11/)

Dec 6, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.10](https://pypi.org/project/pydantic-ai/0.0.10/)

Dec 6, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.9](https://pypi.org/project/pydantic-ai/0.0.9/)

Dec 4, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.8](https://pypi.org/project/pydantic-ai/0.0.8/)

Dec 2, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.7](https://pypi.org/project/pydantic-ai/0.0.7/)

Nov 29, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.6](https://pypi.org/project/pydantic-ai/0.0.6/)

Nov 25, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[0.0.6a4](https://pypi.org/project/pydantic-ai/0.0.6a4/)

Nov 25, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.6a4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[0.0.6a3](https://pypi.org/project/pydantic-ai/0.0.6a3/)

Nov 25, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.6a3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[0.0.6a2](https://pypi.org/project/pydantic-ai/0.0.6a2/)

Nov 25, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.6a2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[0.0.6a1](https://pypi.org/project/pydantic-ai/0.0.6a1/)

Nov 25, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.6a1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.5](https://pypi.org/project/pydantic-ai/0.0.5/)

Nov 20, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.4](https://pypi.org/project/pydantic-ai/0.0.4/)

Nov 19, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.3](https://pypi.org/project/pydantic-ai/0.0.3/)

Nov 18, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.2](https://pypi.org/project/pydantic-ai/0.0.2/)

Oct 30, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.1](https://pypi.org/project/pydantic-ai/0.0.1/)

Oct 29, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.0](https://pypi.org/project/pydantic-ai/0.0.0/)

May 19, 2024 [2 release files](https://pypi.org/project/pydantic-ai/0.0.0/#files)

[![](https://pypi-camo.freetls.fastly.net/0e16ff2846ab7bc04f1e52d760b072c987232f52/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f416e7468726f7069635f6c6f676f5f2d5f536c6174652e706e67)Anthropic, PBCVisionary sponsor](https://www.anthropic.com/) [![](https://pypi-camo.freetls.fastly.net/2056e7cc45e271b6b509980e9ff24b8b6346f2f4/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f626c6f6f6d626572672e706e67)BloombergVisionary sponsor](https://www.techatbloomberg.com/) [![](https://pypi-camo.freetls.fastly.net/7e24ecafc35532bbd56c7c91521ea6701110c742/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f6872742e706e67)Hudson River TradingVisionary sponsor](https://www.hudsonrivertrading.com/careers/) [![](https://pypi-camo.freetls.fastly.net/6f7cbf25b7d9ee146661528e012e8fa51d6f3337/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f4d6574615f6c6f636b75705f706f7369746976655f7072696d6172795f5247425f636f70795f68546b493532472e706e67)MetaVisionary sponsor](https://about.facebook.com/meta/) [![](https://pypi-camo.freetls.fastly.net/22baa32a7b36b109ce052634015d878f5d029280/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f6e76696469612e706e67)NVIDIAVisionary sponsor](https://developer.nvidia.com/) [![](https://pypi-camo.freetls.fastly.net/34ebcaca9a4316e862f2f7641b12534f0cb81bf1/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f6d6963726f736f66742e706e67)MicrosoftSustainability sponsor](https://aka.ms/python) [![](https://pypi-camo.freetls.fastly.net/237c8773674b9f8beff9f894a07424e3b579cd6a/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f6465706f742d636f6c6f722d6c6f676f2d35567a75416e7a6b2e706e67)DepotContinuous Integration](https://depot.dev/) [![](https://pypi-camo.freetls.fastly.net/f0e9bd2edb2aa1c533d61b0d4fda0ee761bef88a/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f6177732d636f6c6f722d6c6f676f2d416c6f43525230612e706e67)AWSCloud computing and Security Sponsor](https://aws.amazon.com/) [![](https://pypi-camo.freetls.fastly.net/530379bec76c3440bd94a24092f49e27323ad0d7/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f64617461646f672d636f6c6f722d6c6f676f2d71616563774a67722e706e67)DatadogMonitoring](https://www.datadoghq.com/) [![](https://pypi-camo.freetls.fastly.net/9706778018adad6f5bf682f55d7bbc226abe551c/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f666173746c792d636f6c6f722d6c6f676f2d766c6d424c33654c2e706e67)FastlyCDN](https://www.fastly.com/) [![](https://pypi-camo.freetls.fastly.net/522342e78db3080c18697369dde99a0ed7925e86/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f676f6f676c652d636f6c6f722d6c6f676f2d32755437496c54702e706e67)GoogleDownload Analytics](https://careers.google.com/) [![](https://pypi-camo.freetls.fastly.net/f2a422796f8e4d51d60d7030b7973aa1651bd096/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f73656e7472792d636f6c6f722d6c6f676f2d346e306a654878502e706e67)SentryError logging](https://sentry.io/for/python/?utm_source=pypi&utm_medium=paid-community&utm_campaign=python-na-evergreen&utm_content=static-ad-pypi-sponsor-learnmore) [![](https://pypi-camo.freetls.fastly.net/b0ba0741ac65afcb01ebb4bbf0634c54b8a15827/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f737461747573706167652d636f6c6f722d6c6f676f2d423232436b746e6b2e706e67)StatusPageStatus page](https://statuspage.io/)

- "PyPI", "Python Package Index", and the blocks logos are registered [trademarks](https://pypi.org/trademarks/) of the [Python Software Foundation](https://www.python.org/psf-landing).
- © 2026 [Python Software Foundation](https://www.python.org/psf-landing/ "External link")
- [Site map](https://pypi.org/sitemap/)
- Deployed from [`8f38ce5`](https://github.com/pypi/warehouse/commit/8f38ce5c45aef4f0370509d6651551073a2a82fa "External link")
