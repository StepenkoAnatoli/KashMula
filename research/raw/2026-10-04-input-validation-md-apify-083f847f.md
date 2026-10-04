---
url: https://docs.apify.com/sdk/python/docs/guides/input-validation.md
retrieved: 2026-10-04
command: firecrawl scrape https://docs.apify.com/sdk/python/docs/guides/input-validation.md --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
---
# Input validation with Pydantic

Copy for LLM

In this guide, you'll learn how to validate your Apify Actor's input with [Pydantic](https://docs.pydantic.dev/), so that your code works with a typed, guaranteed-valid object instead of a raw dictionary.

## Introduction[](#introduction)

An Actor reads its input with [`Actor.get_input`](https://docs.apify.com/sdk/python/reference/class/Actor.md#get_input), which returns the input record as a plain `dict`. Working with that dictionary directly is fragile:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBhcGlmeSBpbXBvcnQgQWN0b3JcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgRW50ZXIgdGhlIGNvbnRleHQgb2YgdGhlIEFjdG9yLlxcbiAgICBhc3luYyB3aXRoIEFjdG9yOlxcbiAgICAgICAgIyBSZWFkIHRoZSBpbnB1dCBhbmQgcmVhY2ggaW50byB0aGUgcmF3IGRpY3QuXFxuICAgICAgICBhY3Rvcl9pbnB1dCA9IGF3YWl0IEFjdG9yLmdldF9pbnB1dCgpIG9yIHt9XFxuICAgICAgICBzZWFyY2hfdGVybXMgPSBhY3Rvcl9pbnB1dC5nZXQoJ3NlYXJjaFRlcm1zJywgW10pXFxuICAgICAgICBtYXhfcmVzdWx0cyA9IGFjdG9yX2lucHV0LmdldCgnbWF4UmVzdWx0cycsIDEwKVxcblxcbiAgICAgICAgQWN0b3IubG9nLmluZm8oJ3NlYXJjaF90ZXJtcz0lcywgbWF4X3Jlc3VsdHM9JXMnLCBzZWFyY2hfdGVybXMsIG1heF9yZXN1bHRzKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.GqKCwyxP7eQ0-yOIMw_heXwvresBy0m6w0Wa5bPD4wA\&asrc=run_on_apify)

```
import asyncio



from apify import Actor





async def main() -> None:

    # Enter the context of the Actor.

    async with Actor:

        # Read the input and reach into the raw dict.

        actor_input = await Actor.get_input() or {}

        search_terms = actor_input.get('searchTerms', [])

        max_results = actor_input.get('maxResults', 10)



        Actor.log.info('search_terms=%s, max_results=%s', search_terms, max_results)





if __name__ == '__main__':

    asyncio.run(main())
```

* There are no type guarantees. `max_results` can arrive as the string `"10"` or `None` and you won't know until something breaks.
* There's no validation. Nothing stops `max_results` from being `0` or `-5`, or `search_terms` from being empty.
* A typo in a key, like `maxResult` instead of `maxResults`, silently falls back to the default instead of failing.
* Defaults are scattered across the codebase, and your editor can't autocomplete the fields or catch mistakes.

[Pydantic](https://docs.pydantic.dev/) solves all of these problems. You declare the shape of your input once as a model, and Pydantic parses the raw dictionary into a typed object, applies defaults, enforces constraints, and produces clear error messages when the input doesn't match.

To use Pydantic, install it into your Actor's environment:

```
pip install pydantic
```

## Example Actor[](#example-actor)

The following Actor declares its input as a Pydantic `BaseModel`, validates the raw input against it, and then works with a fully typed object. On invalid input it fails fast with a readable error. On valid input it logs the normalized values and stores them as the Actor's output.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSB0eXBpbmcgaW1wb3J0IExpdGVyYWxcXG5cXG5mcm9tIHB5ZGFudGljIGltcG9ydCBCYXNlTW9kZWwsIENvbmZpZ0RpY3QsIEZpZWxkLCBWYWxpZGF0aW9uRXJyb3IsIGZpZWxkX3ZhbGlkYXRvclxcbmZyb20gcHlkYW50aWMuYWxpYXNfZ2VuZXJhdG9ycyBpbXBvcnQgdG9fY2FtZWxcXG5cXG5mcm9tIGFwaWZ5IGltcG9ydCBBY3RvclxcblxcblxcbmNsYXNzIEFjdG9ySW5wdXQoQmFzZU1vZGVsKTpcXG4gICAgXFxcIlxcXCJcXFwiVHlwZWQgYW5kIHZhbGlkYXRlZCByZXByZXNlbnRhdGlvbiBvZiB0aGUgQWN0b3IgaW5wdXQuXFxcIlxcXCJcXFwiXFxuXFxuICAgICMgRGVyaXZlIGVhY2ggZmllbGQncyBjYW1lbENhc2UgYWxpYXMgKHNlYXJjaFRlcm1zLCBtYXhSZXN1bHRzLCAuLi4pIGF1dG9tYXRpY2FsbHk7XFxuICAgICMgYWNjZXB0IGJvdGggc3BlbGxpbmdzIGFuZCBpZ25vcmUgZXh0cmFzLlxcbiAgICBtb2RlbF9jb25maWcgPSBDb25maWdEaWN0KFxcbiAgICAgICAgcG9wdWxhdGVfYnlfbmFtZT1UcnVlLCBleHRyYT0naWdub3JlJywgYWxpYXNfZ2VuZXJhdG9yPXRvX2NhbWVsXFxuICAgIClcXG5cXG4gICAgIyBSZXF1aXJlZDogbm9uLWVtcHR5IGxpc3Qgb2Ygc2VhcmNoIHRlcm1zIChub3JtYWxpemVkIGJlbG93KS5cXG4gICAgc2VhcmNoX3Rlcm1zOiBsaXN0W3N0cl0gPSBGaWVsZChtaW5fbGVuZ3RoPTEpXFxuXFxuICAgICMgT3B0aW9uYWw6IDEtMTAwLCBkZWZhdWx0cyB0byAxMC5cXG4gICAgbWF4X3Jlc3VsdHM6IGludCA9IEZpZWxkKGRlZmF1bHQ9MTAsIGdlPTEsIGxlPTEwMClcXG5cXG4gICAgIyBPcHRpb25hbDogcmVzdHJpY3RlZCB0byBhIGZpeGVkIHNldCBvZiBjaG9pY2VzLlxcbiAgICBvdXRwdXRfZm9ybWF0OiBMaXRlcmFsWydqc29uJywgJ2NzdiddID0gRmllbGQoZGVmYXVsdD0nanNvbicpXFxuXFxuICAgIEBmaWVsZF92YWxpZGF0b3IoJ3NlYXJjaF90ZXJtcycpXFxuICAgIEBjbGFzc21ldGhvZFxcbiAgICBkZWYgX25vcm1hbGl6ZV90ZXJtcyhjbHMsIHZhbHVlOiBsaXN0W3N0cl0pIC0-IGxpc3Rbc3RyXTpcXG4gICAgICAgICMgVHJpbSB3aGl0ZXNwYWNlIGFuZCBkcm9wIGVtcHR5IHRlcm1zLlxcbiAgICAgICAgY2xlYW5lZCA9IFt0ZXJtLnN0cmlwKCkgZm9yIHRlcm0gaW4gdmFsdWUgaWYgdGVybS5zdHJpcCgpXVxcbiAgICAgICAgaWYgbm90IGNsZWFuZWQ6XFxuICAgICAgICAgICAgcmFpc2UgVmFsdWVFcnJvcignc2VhcmNoVGVybXMgbXVzdCBjb250YWluIGF0IGxlYXN0IG9uZSBub24tZW1wdHkgdGVybScpXFxuICAgICAgICByZXR1cm4gY2xlYW5lZFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgYXN5bmMgd2l0aCBBY3RvcjpcXG4gICAgICAgICMgUmVhZCB0aGUgcmF3IGlucHV0IChhIHBsYWluIGRpY3QsIG5vdCB5ZXQgdmFsaWRhdGVkKS5cXG4gICAgICAgIHJhd19pbnB1dCA9IGF3YWl0IEFjdG9yLmdldF9pbnB1dCgpIG9yIHt9XFxuXFxuICAgICAgICAjIFZhbGlkYXRlIHRoZSByYXcgaW5wdXQgYWdhaW5zdCB0aGUgbW9kZWwuXFxuICAgICAgICB0cnk6XFxuICAgICAgICAgICAgYWN0b3JfaW5wdXQgPSBBY3RvcklucHV0Lm1vZGVsX3ZhbGlkYXRlKHJhd19pbnB1dClcXG4gICAgICAgIGV4Y2VwdCBWYWxpZGF0aW9uRXJyb3IgYXMgZXhjOlxcbiAgICAgICAgICAgICMgTG9nIGEgcGVyLWZpZWxkIHN1bW1hcnkgYW5kIGZhaWwgdGhlIHJ1biBjbGVhbmx5LCB3aXRob3V0IGEgcmF3IHRyYWNlYmFjay5cXG4gICAgICAgICAgICBBY3Rvci5sb2cuZXJyb3IoJ1RoZSBBY3RvciBpbnB1dCBpcyBpbnZhbGlkOlxcXFxuJXMnLCBleGMpXFxuICAgICAgICAgICAgYXdhaXQgQWN0b3IuZmFpbChzdGF0dXNfbWVzc2FnZT0nVGhlIEFjdG9yIGlucHV0IGlzIGludmFsaWQuJylcXG4gICAgICAgICAgICByZXR1cm5cXG5cXG4gICAgICAgICMgV29yayB3aXRoIHR5cGVkIGF0dHJpYnV0ZXMgZnJvbSBoZXJlIG9uLlxcbiAgICAgICAgQWN0b3IubG9nLmluZm8oJ0lucHV0IHBhc3NlZCB2YWxpZGF0aW9uOiAlcycsIGFjdG9yX2lucHV0Lm1vZGVsX2R1bXAoKSlcXG5cXG4gICAgICAgIG1heF9yZXN1bHRzID0gYWN0b3JfaW5wdXQubWF4X3Jlc3VsdHNcXG4gICAgICAgIGZvciB0ZXJtIGluIGFjdG9yX2lucHV0LnNlYXJjaF90ZXJtczpcXG4gICAgICAgICAgICBBY3Rvci5sb2cuaW5mbygnUHJvY2Vzc2luZyAlciAobWF4ICVkIHJlc3VsdHMpJywgdGVybSwgbWF4X3Jlc3VsdHMpXFxuXFxuICAgICAgICAjIFN0b3JlIHRoZSBub3JtYWxpemVkIGlucHV0IGFzIG91dHB1dC5cXG4gICAgICAgIGF3YWl0IEFjdG9yLnNldF92YWx1ZSgnT1VUUFVUJywgYWN0b3JfaW5wdXQubW9kZWxfZHVtcCgpKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.vCEbp-0yQPp-92urioTWcQOnEyoCyJRFwUklPK5uTYY\&asrc=run_on_apify)

```
import asyncio

from typing import Literal



from pydantic import BaseModel, ConfigDict, Field, ValidationError, field_validator

from pydantic.alias_generators import to_camel



from apify import Actor





class ActorInput(BaseModel):

    """Typed and validated representation of the Actor input."""



    # Derive each field's camelCase alias (searchTerms, maxResults, ...) automatically;

    # accept both spellings and ignore extras.

    model_config = ConfigDict(

        populate_by_name=True, extra='ignore', alias_generator=to_camel

    )



    # Required: non-empty list of search terms (normalized below).

    search_terms: list[str] = Field(min_length=1)



    # Optional: 1-100, defaults to 10.

    max_results: int = Field(default=10, ge=1, le=100)



    # Optional: restricted to a fixed set of choices.

    output_format: Literal['json', 'csv'] = Field(default='json')



    @field_validator('search_terms')

    @classmethod

    def _normalize_terms(cls, value: list[str]) -> list[str]:

        # Trim whitespace and drop empty terms.

        cleaned = [term.strip() for term in value if term.strip()]

        if not cleaned:

            raise ValueError('searchTerms must contain at least one non-empty term')

        return cleaned





async def main() -> None:

    async with Actor:

        # Read the raw input (a plain dict, not yet validated).

        raw_input = await Actor.get_input() or {}



        # Validate the raw input against the model.

        try:

            actor_input = ActorInput.model_validate(raw_input)

        except ValidationError as exc:

            # Log a per-field summary and fail the run cleanly, without a raw traceback.

            Actor.log.error('The Actor input is invalid:\n%s', exc)

            await Actor.fail(status_message='The Actor input is invalid.')

            return



        # Work with typed attributes from here on.

        Actor.log.info('Input passed validation: %s', actor_input.model_dump())



        max_results = actor_input.max_results

        for term in actor_input.search_terms:

            Actor.log.info('Processing %r (max %d results)', term, max_results)



        # Store the normalized input as output.

        await Actor.set_value('OUTPUT', actor_input.model_dump())





if __name__ == '__main__':

    asyncio.run(main())
```

### About the model[](#about-the-model)

* Apify input fields conventionally use camel case (`maxResults`), while Python attributes use snake case (`max_results`). Since every field follows that convention, `alias_generator=to_camel` derives the camel case alias for the whole model at once, instead of spelling out `Field(alias=...)` on each field. `populate_by_name=True` lets the model accept either spelling, which is handy in tests.
* A field without a default (`search_terms`) is required. A field with a default (`max_results`) is optional. There's a single, obvious place where every default lives.
* `ge=1, le=100` enforces a numeric range, `min_length=1` rejects an empty list, and `Literal['json', 'csv']` restricts a field to a fixed set of choices, mirroring an `enum` in the input schema.
* The `field_validator` normalizes the search terms (trimming whitespace, dropping empties) and rejects input that has nothing left. The rest of your code never has to repeat those checks.
* `extra='ignore'` means adding a new field to your input schema won't break an older Actor build that doesn't know about it yet. Use `extra='forbid'` instead if you prefer to reject anything unexpected.

### About the validation[](#about-the-validation)

* `model_validate` parses the raw dictionary into a typed `ActorInput` instance. It fills in defaults and guarantees every field is valid, or raises a `ValidationError` that describes every problem at once.

* Catching that error, logging a readable summary, and failing the run with [`Actor.fail`](https://docs.apify.com/sdk/python/reference/class/Actor.md#fail) marks the run as `FAILED` with a clear status message. It fails fast right at the start with a readable explanation, instead of crashing with a raw traceback deeper in the run.

* The error messages refer to the fields by their input-schema aliases. For invalid input like `{"searchTerms": [], "maxResults": 999, "outputFormat": "xml"}`, the log shows exactly what's wrong:

  ```
  The Actor input is invalid:

  3 validation errors for ActorInput

  searchTerms

    List should have at least 1 item after validation, not 0 ...

  maxResults

    Input should be less than or equal to 100 ...

  outputFormat

    Input should be 'json' or 'csv' ...
  ```

Once validation passes, the rest of `main` works with `actor_input.search_terms`, `actor_input.max_results`, and `actor_input.output_format`, all correctly typed, with editor autocompletion and static type checking.

## Relationship to the input schema[](#relationship-to-the-input-schema)

Pydantic validation complements the Actor's [input schema](https://docs.apify.com/platform/actors/development/input-schema) (`.actor/input_schema.json`). It doesn't replace it. The two serve different layers:

* The input schema drives the [Apify Console](https://console.apify.com/) form, documents the fields for your users, and lets the platform validate input before the run even starts. Keep declaring your fields there.
* The Pydantic model validates the input again inside your Python code, where it gives you a typed object, IDE support, and richer rules (normalization, cross-field checks, custom formats) that the input schema can't express. It's also your safety net for runs started programmatically by [another Actor](https://docs.apify.com/sdk/python/docs/concepts/interacting-with-other-actors.md) or executed [locally](https://docs.apify.com/cli/docs/reference#apify-run), and for keeping the two definitions honest with each other.

Keep the model's aliases in sync with the field keys in `input_schema.json`, and the two definitions describe the same input from both sides.

## Useful validation features[](#useful-validation-features)

Pydantic offers extra features for validating Actor input. For the full set of types, constraints, and validators, see the [Pydantic documentation](https://docs.pydantic.dev/latest/concepts/models/).

### Format-validated types[](#format-validated-types)

For common string formats, for example `HttpUrl` for URLs or `EmailStr` for e-mail addresses, use format-validated types:

```
from pydantic import BaseModel, EmailStr, HttpUrl





class ActorInput(BaseModel):

    target_url: HttpUrl

    # `EmailStr` needs the `pydantic[email]` extra installed.

    contact_email: EmailStr
```

### Cross-field validation[](#cross-field-validation)

When one field's validity depends on another, use `model_validator`:

```
from typing import Self



from pydantic import BaseModel, model_validator





class ActorInput(BaseModel):

    min_price: int = 0

    max_price: int = 100



    @model_validator(mode='after')

    def _check_range(self) -> Self:

        if self.min_price > self.max_price:

            raise ValueError('min_price must not exceed max_price')

        return self
```

### Secret input fields[](#secret-input-fields)

The platform decrypts [secret input fields](https://docs.apify.com/platform/actors/development/secret-input) for you before [`Actor.get_input`](https://docs.apify.com/sdk/python/reference/class/Actor.md#get_input) returns, so you receive plaintext. To keep them from leaking into logs or `model_dump()` output, wrap such fields in Pydantic's `SecretStr` and read the plaintext with `get_secret_value()` when you actually need it:

```
from pydantic import BaseModel, SecretStr





class ActorInput(BaseModel):

    # Masked in logs and `model_dump()`; read the plaintext with `get_secret_value()`.

    api_token: SecretStr





actor_input = ActorInput.model_validate({'api_token': 'my-secret-token'})

token = actor_input.api_token.get_secret_value()
```

## Conclusion[](#conclusion)

In this guide, you learned how to validate Actor input with Pydantic: declaring the input as a model with aliases, defaults, and constraints, parsing the raw input with `model_validate`, failing fast with a readable error when the input is invalid, and working with a typed object for the rest of the run. To get started with your own Actors, see the [Actor templates](https://apify.com/templates/categories/python). If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/apify-sdk-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy validating!

## Additional resources[](#additional-resources)

* [Pydantic: Official documentation](https://docs.pydantic.dev/)
* [Pydantic: Models](https://docs.pydantic.dev/latest/concepts/models/)
* [Pydantic: Validators](https://docs.pydantic.dev/latest/concepts/validators/)
* [Apify: Actor input](https://docs.apify.com/platform/actors/running/input)
* [Apify: Input schema specification](https://docs.apify.com/platform/actors/development/input-schema)

