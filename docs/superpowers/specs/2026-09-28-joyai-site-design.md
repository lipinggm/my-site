# joyai personal site — design

Date: 2026-09-28
Status: approved in brainstorming, pending spec review

## Intent

- Personal-first site for Joy G. (AI learner), showcasing one work.
- Goal: visitors learn who Joy is, what Joy is working on, and can make contact.
- Content updates are occasional page edits. No blog or content system now.
- Public on Cloudflare at `joyai.pages.dev`. Custom domain deferred.

## Decisions

| Topic | Decision | Reason |
|---|---|---|
| Stack | Single static `index.html`, no build tool | Only one page; nothing to build |
| Hosting | Cloudflare Pages, Git integration (option 1) | Push-to-deploy, previews, rollback, zero config files |
| Repo | `github.com/lipinggm/my-site`, public | Work card links to source |
| Project name | `joyai` (fallback `joy-ai` if suffixed) | Pages names are lowercase-only |
| Publish dir | `public/` | Keeps `docs/` and future repo files off the web |
| Contact email | `lipinggm1@gmail.com` | Dedicated public address |

## Page changes

1. New section between "learning" and "contact", reusing `.section-title`, `.cards`, `.card`:

   | Key | zh | en |
   |---|---|---|
   | `work` | 我的作品 | My Work |
   | `work1Title` | 这个网站 | This Website |
   | `work1Text` | 用 Claude Code 从零搭建的双语个人站，托管在 Cloudflare Pages，推送即上线。 | A bilingual personal site built from scratch with Claude Code, hosted on Cloudflare Pages and deployed on every push. |
   | `work1Live` | 在线访问 ↗ | Live ↗ |
   | `work1Source` | 源码 ↗ | Source ↗ |

   - Live link: the URL Cloudflare actually assigns (filled after step 2 below).
   - Source link: `https://github.com/lipinggm/my-site`.
   - One new style rule, `.card-links`. No JS logic changes.
2. Contact GitHub link: `https://github.com/` → `https://github.com/lipinggm`.
3. Remove the LinkedIn item.

Out of scope: screenshots, tech badges, work detail pages, analytics, `_headers`/`_redirects`, custom domain.

## Cloudflare Pages settings

| Setting | Value |
|---|---|
| Project name | `joyai` |
| Production branch | `main` |
| Framework preset | None |
| Build command | (empty) |
| Build output directory | `public` |

GitHub App access: only `lipinggm/my-site`.

## Execution order

| # | Owner | Action | Done when |
|---|---|---|---|
| 1 | Claude | `git mv index.html public/index.html`, commit, push | Root holds only `public/` and `docs/` |
| 2 | Joy | Create Pages project in dashboard with settings above | First deploy succeeds; actual URL reported |
| 3 | Claude | Apply page changes, commit, push | Second deploy succeeds |
| 4 | Claude | Run acceptance checks | All pass |

## Acceptance

- `https://joyai.pages.dev/` returns 200 and matches `public/index.html`.
- `https://joyai.pages.dev/docs/` returns 404.
- Source, GitHub, and email links point to the values above.
- The page contains no `example.com`, `linkedin`, or `href="#"`.
