---
tags:
    - software
    - ai
---

AI coding agents such as Claude Code, Codex CLI and Gemini CLI aren't
installed on FarmShare, and there are no modules for them. You can install
them yourself in your home directory, the same way you'd install other
software without administrator rights.

## Install an Agent

Use the install instructions from the tool's own documentation, and choose the
option for installing as a regular user on Linux. Most agents offer either a
standalone installer or a package from npm.

Installers that put files in your home directory, such as under `~/.local`,
work without administrator rights. Instructions that start with `sudo` won't
work on FarmShare. If a tool needs Node.js, check whether it's installed as a
module:

```bash
module spider nodejs
```

For general advice on installing software without administrator rights, see
[Install Software Yourself](install-yourself.md).

## Things to Know

We don't block the Anthropic, OpenAI or other AI service APIs on FarmShare, so
agents that connect to them can run here. That isn't a promise that a
particular tool will work, and we can't support the tools themselves. You need
your own account or API key with the service, and you're responsible for its
costs.

Agents, their caches and the files they create are stored in your home
directory and count toward your {{ facts.home_quota }} home quota. Some keep
large logs or caches, so check them with `du` if your home directory fills up.
See [Check and Free Up Space](../use/free-up-space.md).

You can run an agent on a login node for editing and small tasks. If it runs
heavy work, such as training a model or a long test suite, run that work on a
compute node in an [interactive session](../use/interactive-sessions.md) or a
[batch job](../use/batch-jobs.md).

An agent sends your code and files to an outside service. FarmShare isn't
approved for high-risk data, and you shouldn't send data to an AI service
unless Stanford's rules for that data allow it. See
[Policies](../reference/policies.md).

## If Something Goes Wrong

If an agent can't connect, or hangs the next time you start it, save the full
error output. Check the tool's own documentation and issue tracker first. If it
looks like a FarmShare problem, such as a network connection that fails only
on FarmShare, [ask us](../fix/get-help.md) and include the error.
