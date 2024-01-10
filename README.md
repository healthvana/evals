# Healthvana OpenAI Evals

This is our fork of OpenAI's [Evals](https://github.com/healthvana/evals). See that repo their complete README.

We use Evals to test our AI Navigator. Creating high quality evals is one of the most impactful things you can do. Without evals, it can be very difficult and time intensive to understand how different model versions might effect your use case. 

## Setup

To run evals, you will need to set up and specify your [OpenAI API key](https://platform.openai.com/account/api-keys). You can request a key in #company-access-requests. 
After you obtain an API key, specify it using the [`OPENAI_API_KEY` environment variable](https://platform.openai.com/docs/quickstart/step-2-setup-your-api-key). Please be aware of the [costs](https://openai.com/pricing) associated with using the API when running evals.

**Minimum Required Version: Python 3.9**

### Downloading evals

The Evals registry is stored using [Git-LFS](https://git-lfs.com/). Once you have downloaded and installed LFS, you can fetch the evals (from within your local copy of this evals repo) with:
```sh
cd evals
git lfs fetch --all
git lfs pull
```

This will populate all the pointer files under `evals/registry/data`.

### Making evals

If you are going to be creating evals, we suggest cloning this repo directly from GitHub and installing the requirements using the following command:

```sh
pip install -e .
```

Using `-e`, changes you make to your eval will be reflected immediately without having to reinstall.

Optionally, you can install the formatters for pre-committing with:

```sh
pip install -e .[formatters]
```

Then run `pre-commit install` to install pre-commit into your git hooks. pre-commit will now run on every commit.

If you want to manually run all pre-commit hooks on a repository, run `pre-commit run --all-files`. To run individual hooks use `pre-commit run <hook_id>`.

## Terminology
- **Eval**: This is the type of test you are running. In the prep example, we use the "Includes" eval to test that certain words appear in the AI response. In evals/elsuite there are lots of different types of tests (evals), many beyond the scope of our AI navigator. We can also write our own Evals if there are types of tests we desire that don't exist here (eg: Excludes)
- **Completion Function**: What tool are we testing? In our case, we'll be testing against OpenAI's gpt-4 to replicate what's happening on h. The nuts and bolts of this live in evals/openai.py

## How to run locally
- After cloning the repo, run `oaieval gpt-4 test-includes-prep`. 
  - oaieval: See evals/cli/oaieval.py. This is the handy CLI for running evals within this repo.
  - gpt-4: This is our completion function.
  - test-includes-prep: This test name is defined in evals/registry/evals/test-basic.yaml

## Writing evals

- For a HV example: see evals/elsuite/test/prep.py.
- Walking through the process for building an eval: [build-eval.md](docs/build-eval.md)
- Exploring an example of implementing custom eval logic: [custom-eval.md](docs/custom-eval.md).

## Troubleshooting

When I run an eval, it sometimes hangs at the very end (after the final report). What's going on?

- This is a known issue, but you should be able to interrupt it safely and the eval should finish immediately after.