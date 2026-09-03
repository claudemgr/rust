# TODO

- [ ] HYBRID.md (and go/HYBRID.md): resolve the `:z` SELinux volume-label
  contradiction in the compose examples — one section says bind mounts
  must carry `:z`, another omits it; direction is undecidable without a
  user decision on whether SELinux-labeled hosts are the assumed target
- [ ] Template-engine inconsistency across the rust family: API.md uses
  Tera syntax (`{% if x %}`, `and`) while SERVER.md and HYBRID.md use
  Askama (`&&`); pick one engine for the whole family and convert the
  odd files out
