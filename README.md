# World Water Reserve — Reddit Content Bot

An n8n automation workflow that publishes educational content about water quality,
home filtration, well water treatment, and environmental water issues to relevant
Reddit communities.

## What It Does

1. **Reads an RSS feed** from [worldwaterreserve.com](https://worldwaterreserve.com),
   a site I publish covering water quality, filtration, and conservation topics
2. **Extracts one specific angle** from each new article using the Claude AI API —
   not a summary, but a focused insight or practical finding worth discussing
3. **Generates a standalone Reddit text post** on that angle, written to provide
   full value to the reader without requiring them to click any link
4. **Routes the post** to the most topically relevant subreddit from a fixed list,
   matched by WordPress article category (e.g. well water articles → r/wellwater,
   environmental news → r/climate)
5. **Submits the post** via the Reddit OAuth2 API using a single registered account
6. **Logs the post** to a deduplication sheet to prevent re-posting the same article
   to the same subreddit

## Posting Behavior

- Maximum **1 post per day** globally across all subreddits
- Maximum **1–3 posts per week** per individual subreddit, depending on community size
- Posts are **text-only** — no image or link posts
- The article URL is included at the end of the post body as an optional reference,
  not as the primary content
- Each post ends with a genuine discussion question inviting community engagement

## What It Does NOT Do

- Does not scrape or read Reddit content
- Does not vote on posts or comments
- Does not comment at scale or reply to users automatically
- Does not access private messages or user data
- Does not use Reddit data to train AI models
- Does not sell, share, or commercialize any data
- Does not run on multiple accounts

## Subreddits

Posts are routed to one of the following communities based on article topic.
Each subreddit has a weekly posting cap enforced by the workflow.

| Subreddit | Cap/Week | Topic Category |
|---|---|---|
| r/homeimprovement | 2 | Water Filtration, Water Management |
| r/DIY | 2 | Water Filtration, Water Management |
| r/climate | 3 | News, Water Crisis |
| r/collapse | 2 | News |
| r/homesteading | 1 | Rainwater Harvesting, Well Water, Permaculture, Self Sufficiency |
| r/Permaculture | 1 | Rainwater Harvesting, Permaculture, Aquaponics |
| r/Plumbing | 1 | Water Filtration |
| r/wellwater | 1 | Well Water Treatment |
| r/homestead | 1 | Well Water, Permaculture |
| r/preppers | 1 | News |
| r/prepping | 1 | News, Self Sufficiency |
| r/survivalism | 1 | Self Sufficiency, Well Water |
| r/bugout | 1 | Self Sufficiency |
| r/Bushcraft | 1 | Self Sufficiency, Well Water |
| r/WaterFilters | 1 | Water Filtration |
| r/OffTheGrid | 1 | Rainwater Harvesting, Well Water, Self Sufficiency |
| r/OffGridCabins | 1 | Rainwater Harvesting, Self Sufficiency |
| r/OffGridLiving | 1 | Rainwater Harvesting, Self Sufficiency |
| r/OffGrid | 1 | Self Sufficiency |
| r/SelfSufficiency | 1 | Self Sufficiency |
| r/ClimateActionPlan | 1 | Community Resilience, News |
| r/ZeroWaste | 1 | Community Resilience |
| r/simpleliving | 1 | Community Resilience |
| r/OrganicGardening | 1 | Permaculture, Rainwater Harvesting |
| r/RenewableEnergy | 1 | Self Sufficiency |
| r/water | 1 | Water Management, News |
| r/aquaponics | 1 | Aquaponics |
| r/Irrigation | 1 | Water Management, Permaculture |

## Tech Stack

- **[n8n](https://n8n.io)** — self-hosted workflow automation (workflow definition in this repo)
- **Claude API (Anthropic)** — angle extraction and post generation
- **WordPress REST API** — article source
- **Google Sheets** — deduplication and posting log
- **Reddit OAuth2 API** — post submission

## File in This Repo

`WWR — Reddit Article Publisher.json` — the complete n8n workflow definition,
including all node configurations, routing logic, weekly cap enforcement,
deduplication checks, and the AI prompt used to generate posts.
