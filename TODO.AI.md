# TODO

- [ ] HYBRID.md has an odd line-start fence count (1741 at commit `a83a01e022c9`, unchanged by the vanity-spec edit) while go/HYBRID.md is even (1744). Raw parity is an unreliable check here — fenced ```markdown examples embed literal fences/headings — so audit whether a genuinely unclosed fence exists or the count is a false positive from embedded examples, and fix only if real.
