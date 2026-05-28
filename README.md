# OpsDirector EDA test rulebooks

Test rulebooks for end-to-end verification of OpsDirector's Ansible Event-Driven
Ansible (EDA) integration against Ansible Automation Platform (AAP).

## Rulebooks

### `rulebooks/opsd-eda-smoke.yml`

Minimal "log everything" rulebook. Use this with an AAP Event Stream attached
to its `ansible.eda.generic` source. Every event POSTed to the attached stream
is matched and printed to the activation's stdout via the `debug` action.

## How to use in AAP

1. **Project** — create an AAP project pointing at this git repo.
2. **Event Stream** — create an HMAC event stream and save the secret.
3. **Rulebook Activation** — create an activation that:
   - uses this project,
   - selects `rulebooks/opsd-eda-smoke.yml`,
   - attaches the event stream from step 2 and maps it to the
     `ansible.eda.generic` source listed in the rulebook.
4. Smoke-test by POSTing a signed payload to the event stream URL; verify the
   `debug` line appears in the activation logs.
