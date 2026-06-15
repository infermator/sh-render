# sh-render

Free-tier render runner. Public repo *only* so that GitHub-hosted Actions
minutes are unlimited (the 2,000 min/mo cap applies to private repos only).

**No application code lives here.** Each workflow clones the private generator
repo at runtime using the `GH_PAT` secret and runs the generator from
`generator/`. The Remotion templates and scripts stay private.

### Why this is safe to be public
- Triggers are `schedule` + `workflow_dispatch` only (not fork-triggerable;
  dispatch needs write access). Strangers can't run jobs or touch the queue.
- Fork PRs get no secrets, so the tokens here can't leak.

### Required secrets
| Secret | What it is |
| --- | --- |
| `GH_PAT` | fine-grained PAT, Contents:read on the private generator repo |
| `BUFFER_PUSH_SECRET` | enqueue bearer token |
| `BLOB_READ_WRITE_TOKEN` | Vercel Blob upload |

### Workflows
- `daily-blog-videos.yml` — 04:30 UTC, ramped blog→video generation
- `daily-blog-photos.yml` — 05:00 UTC, 3-headline photo slideshow
