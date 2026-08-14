# TODO

- [ ] Daily-channel contradiction (SERVER.md, HYBRID.md, API.md — GitHub + Gitea
  daily workflows, 2 sites per file): `daily.yml` publishes a rolling release with
  `tag_name: daily`, but the updater's `matches_branch` classifies daily builds by
  `r.tag_name.len() == 14 && !r.tag_name.contains('.')` (timestamp tags) and
  detects new versions via `r.tag_name != current_version`. A rolling `daily` tag
  is never classified as daily and can never signal a new version. Decide one
  design and apply to both repos in parity: (a) tag daily releases with the
  `YYYYMMDDHHMMSS` timestamp and prune older daily releases by pattern, or
  (b) keep the rolling tag and have the updater compare the release's
  `version.txt` asset (or release name) against the embedded build version.
