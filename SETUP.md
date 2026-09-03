# Setup

The workshop runs on JupyterHub at <https://notebooks.vezilka.ai/>. The
packages that every day uses are already installed there. The later days need a
few more, which you install yourself, and the environment check below tells you
when and how.

## Choosing A Flavour

The Hub offers two flavours of server. They provide the same base packages and
the same three cores and twelve gigabytes of memory, and they differ in whether
PyTorch and a GPU are present.

| Flavour | Provides | Use it for |
| --- | --- | --- |
| CPU | The SciPy stack, meaning numpy, pandas, scikit-learn, matplotlib, seaborn, and statsmodels. | Days 1, 2, 5, and 6. |
| GPU | The same, plus PyTorch built for CUDA 12.8, on one MIG slice of ten gigabytes. | Days 3 and 4. |

Switching flavour means stopping your server from the Hub control panel and
starting the other one. Your home directory comes with you, so nothing you have
written or installed is lost in the move.

## Getting The Materials

One link gives you everything. Opening it copies the repository into your home
directory on the Hub and opens it in JupyterLab.

```
https://notebooks.vezilka.ai/hub/user-redirect/git-pull?repo=https://github.com/peshevskidimitar/MLTP2026&branch=main&urlpath=lab/tree/MLTP2026
```

Open the same link again at the start of every session. It brings down whatever
has been added since, so one bookmark carries you through the whole workshop.

Each day is published before the session that uses it, so a day you cannot see
yet has not been released rather than gone missing. The same is true of the
solution to a laboratory exercise, which appears after the session that sets
it.

## What Happens To Your Work

The link is safe to open as often as you like. When it brings down new
material it keeps everything you have written. Where you and the material have
both changed the same thing, your version wins, and you are never asked to
resolve a conflict.

That rule has one consequence worth knowing. If a correction is published for a
task you have already worked in, the correction does not reach you, and nothing
tells you that it did not. When the assistant announces a fix during a session,
rename your copy of the notebook and then open the link again. The original
file comes back corrected and your renamed copy keeps your answers.

## The Environment Check

Open `environment_setup.ipynb` and run every cell. It reports which flavour you
are on, installs the packages every day uses, lists what each later day still
needs, and confirms that the data for each released day is where the notebooks
expect it.

Read the summary at the bottom. For anything that is missing it prints the
exact command to run, so there is nothing to work out from this document.

## Packages You Install Yourself

Days 3 to 6 each use packages beyond the base ones, listed in a requirements
file of their own under `setup/`. Day 5 needs a key as well as packages, and
the section after this one says where to put it. Two rules govern installing
them, and the environment check follows both in the commands it prints.

Install into your home directory with `--user`, because a plain install goes
into the server's container and disappears the next time the server restarts.

Install with `setup/requirements.txt` as a constraints file. Anything in your
home directory takes precedence over the image, so a package that quietly
brought a different numpy or pandas with it would override the image
everywhere, including on days that worked yesterday. Passing the base pins as
constraints makes pip refuse such an install rather than perform it silently.

Never install PyTorch yourself. The GPU flavour provides a build compiled
against CUDA, and a copy in your home directory would be loaded instead of it,
on both flavours, with the GPU going unused and nothing saying so. If PyTorch
is missing, you are on the CPU flavour and the answer is to switch.

## The Key For Day 5

Day 5 is the only day that talks to a language model, and a language model
needs a credential. Yours is issued to you personally before that session, and
it is not in this repository and must never be put there.

The endpoint is not OpenAI. It is the faculty's own service, at
<https://vllm.finki.ukim.mk/v1>, and it serves open-weight models. It speaks
the same protocol OpenAI does, which is why the notebooks reach it with the
`openai` client, and why nothing on Day 5 costs money per question.

### Where To Put It

Both of Day 5's notebooks look in two places, in this order, and neither one is
inside your copy of the repository.

1. The environment variable `OPENAI_API_KEY`.
2. The file `~/.mltp2026-key`, holding the key and nothing else.

The file is the one to use on the Hub, because it survives a kernel restart and
a server restart and you only write it once. Open a terminal from the
JupyterLab launcher and run this, with your own key in place of the example:

```bash
printf '%s' 'sk-your-own-key-here' > ~/.mltp2026-key
chmod 600 ~/.mltp2026-key
```

`~` is your home directory and the repository sits inside it, so the key is
beside your copy of the material rather than in it. That is the point. A key
written into a notebook cell travels with that notebook, and a key committed
once is public forever.

If neither place has a key, the first cell of each notebook stops with one
sentence telling you so rather than failing somewhere further down.

### What The Endpoint Will And Will Not Do

Each key allows two requests at a time. Nothing in Day 5 sends more than one at
once, so you will not meet that limit working normally, and you may meet it if
you leave the walkthrough running and start the laboratory exercise beside it.
The notebooks retry rather than fail when it happens, waiting a little longer
each time, so the symptom is slowness rather than an error.

The day names one model and two fallbacks, and the first cell reports which one
answered. A model name on this endpoint is an alias, and an alias can stop
pointing at anything without warning, which is why there are fallbacks and why
the notebooks print the name and the time of the run.

## Working Outside JupyterHub

Working on your own machine is not required, but it is supported. The notebooks
do not depend on the Hub and read their data through paths relative to
themselves, so a local copy behaves the same way.

```bash
git clone https://github.com/peshevskidimitar/MLTP2026.git
cd MLTP2026
python3.13 -m venv .venv
source .venv/bin/activate
pip install -r setup/requirements.txt -r setup/requirements-local.txt
jupyter lab
```

`setup/requirements-local.txt` holds JupyterLab itself, which the Hub supplies
and which must never be installed on the Hub. Installing a different JupyterLab
underneath a running server breaks that server together with the Git and
nbgitpuller extensions it depends on.

## The Python Version

Use Python 3.13. It is what the Hub runs and what the materials are verified
against, and matching it keeps the numbers you produce identical to the ones on
screen. Another version is not forbidden, but any difference in output it
causes is yours to explain.

## Versions

`setup/requirements.txt` pins exact versions, and they are the versions both
flavours of the image provide. Pinning keeps the numbers you produce identical
to the numbers the assistant demonstrates, which matters when an exercise asks
you to compare one against the other. If the environment check reports a
version that differs from a pin, raise it before the first session rather than
after.

Day 5 is the exception, and it is worth knowing before that session rather than
during it. Its answers come from a language model on a service outside this
repository, so no pin here governs them. The database figures it is scored
against do not move, and the sentences the model writes around them may. Both
of its notebooks print the model that answered and the time they ran, which is
what tells a stale output from a wrong one.
