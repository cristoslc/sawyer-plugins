# Handoff: this fork owns the OpenRouter Inference fix

**Status as of 2026-09-27.** This file exists so a second thread working the
same bug stops duplicating it.

## Who owns it

Thread `@thread:thr_3t5v2zcp87` owns this work. If you are reading this from
another thread, stop here and coordinate there instead of starting a third
copy.

## Where the fix lives

| | |
|---|---|
| Working copy | `/Users/cristos/Documents/code/sawyer-plugins` (fork of `SawyerHood/sawyer-plugins`) |
| Branch | `fix/openrouter-inference-ai-service-api-0.5` |
| Pushed to | `cristoslc/sawyer-plugins`, same branch name |
| Commit | `0224cd6` `fix(openrouter-inference): port to the 0.5.x AI-service API` |
| Upstream issue | https://github.com/SawyerHood/sawyer-plugins/issues/9 |
| Installed as | `openrouter-inference@0.3.0`, from this path |

## Superseded copy

A parallel thread produced a second port with the same diagnosis, at
`/Users/cristos/code/bb-plugin-openrouter-inference-fork` (version 0.2.1, no git
repo, 27 tests). It is **not** installed. bb reports the 0.3.0 from this repo.
The directory is left on disk for reference; do not reinstall from it.

Differences worth knowing if you read both:

- This fork keeps git history, so the change is reviewable and pushable.
- This fork's tests drive the real registration path through
  `createFakePluginHost`, so `complete`, `transcribe`, `status`, the `status`
  RPC, and `useFor` are all exercised. The other copy's tests cover the HTTP
  helpers and the request builders only.
- The other copy reports 27 tests, this one 35.

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
