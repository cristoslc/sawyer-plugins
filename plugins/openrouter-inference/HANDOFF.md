# Handoff: thread thr_82yrjuu389 owns this fix

**Status as of 2026-09-27.** This file points the work at the thread that owns
it, so nobody starts a third copy of the same port.

## Who owns it

`@thread:thr_82yrjuu389` ("Fix the OpenRouter inference marketplace") owns this
work. Its working directory is the same as this file's directory.

The port in this directory was produced first by `@thread:thr_3t5v2zcp87`, which
has handed it over. Treat that thread's commit as the starting point, not as a
competing branch. Read the handoff note, then continue here.

## Where the fix lives

| | |
|---|---|
| Working copy | `/Users/cristos/Documents/code/sawyer-plugins` (fork of `SawyerHood/sawyer-plugins`) |
| Branch | `fix/openrouter-inference-ai-service-api-0.5` |
| Pushed to | `cristoslc/sawyer-plugins`, same branch name |
| Port commit | `0224cd6` `fix(openrouter-inference): port to the 0.5.x AI-service API` |
| Upstream issue | https://github.com/SawyerHood/sawyer-plugins/issues/9 |
| Installed as | `openrouter-inference@0.3.0`, from this path |

## Superseded copy

The owning thread also produced a port at
`/Users/cristos/code/bb-plugin-openrouter-inference-fork` (version 0.2.1, no git
repo, 27 tests). It is **not** installed. bb reports the 0.3.0 from this repo.
The directory stays on disk for reference; do not reinstall from it.

Differences worth knowing:

- This fork has git history, so the change is reviewable and pushable.
- This fork's tests drive the real registration path through
  `createFakePluginHost`, so `complete`, `transcribe`, `status`, the `status`
  RPC, and `useFor` are all exercised. The 0.2.1 copy's tests cover the HTTP
  helpers and request builders only.
- 35 tests here, 27 there.

## Verified state

```
$ bb plugin list
openrouter-inference@0.3.0  running
  source: path:/Users/cristos/Documents/code/sawyer-plugins/plugins/openrouter-inference

$ bb settings ai-services show
Services:
  codex                            [thread-title, commit-message, voice]  Automatic #1  ready
  openrouter-inference  (API key)  [thread-title, commit-message, voice]  not ready: Add an OpenRouter API key…
```

`not ready` is the plugin's own `status()` function being honest about a missing
key. It is not an error state.

## What is left

1. Set an API key. Use the settings UI, not `bb plugin config … set`, so the
   key does not land in a transcript.
2. Review commit `0224cd6` before any pull request goes upstream.
3. Open the PR only after that review. PR #8 was opened and closed once already
   on a misread instruction; do not repeat that.
