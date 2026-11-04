# ResearchSkills

ResearchSkills is the research pack of
[Grove](https://github.com/Linkuistics/grove). It ships Grove's research
session kinds as agent skills. Grove's core supplies the spine that each kind
loads.

## Kinds

| Kind | Skill | Purpose |
| --- | --- | --- |
| `research-a` | `grove-research-a` | One half of a citation-disciplined survey of literature and prior art |
| `research-b` | `grove-research-b` | The other half of the survey pair, with the same brief |
| `combine-research` | `grove-combine-research` | Unites the two surveys and flags each disagreement |

The `research-family` skill holds the procedure that `research-a` and
`research-b` share. It is not a kind. Each half loads it after Grove's `grove`
skill.

## Layout

The source directory is `plugins/research`. It is the Claude Code plugin root
and the Ravel source directory. Its only root is `skills`, which holds the
three kind skills and the family skill. The repository root holds the files
that the pack does not deliver: this README, the licence and the Taskfile.

Grove's external pack contract, `docs/specs/external-pack-contract.md` in the
Grove repository, states the layout, the references between skills and the
conformance rules.

## Install

Each route also needs Grove's core, which supplies the `grove` skill.

### Ravel

Add this record to the `skills.sources` list of the Ravel settings, beside the
record of Grove's core. Replace `<checkout>` with the absolute path of a
checkout of this repository:

```json
{ "id": "research", "type": "local", "path": "<checkout>/plugins/research", "roots": ["skills"] }
```

Ravel reads the checkout as a local directory. It does not fetch or update the
checkout. A tool outside Ravel holds the checkout at a published commit.

### Claude Code plugin

Install the plugin from Grove's marketplace:

```text
/plugin marketplace add Linkuistics/grove
/plugin install research@linkuistics
```

The manifest declares the dependency `grove`, so the installation also adds
Grove's core. The skills then have the namespace `research:`, for example
`research:grove-research-a`.

### Manual installation

Grove's manual installer links the skills of a pack:

```sh
<grove checkout>/plugins/install.sh --pack <research checkout>/plugins/research
```

Grove's marketplace entry and the installer's `--pack` option arrive with the
Grove release that removes the research kinds from core. Until that release,
Grove ships its own copies of these kinds.

## Checks

Run every check of the pack:

```sh
task check
```

The checks use Grove's conformance runner from a plain Git checkout of Grove,
under `.cache/grove/`. The `Taskfile.yml` variable `GROVE_COMMIT` names that
Grove commit. The variable `GROVE_REPOSITORY` names the public Grove
repository.

- `task check:conformance` checks the pack alone, then the aggregate of
  Grove's core and this pack.
- `task check:plugin` checks the Claude Code plugin with
  `claude plugin validate`. It skips when Claude Code is not installed.

## Provenance

The skills come from Grove commit `6eb881035a8eea1f4bb91ca1394dcbe7ddf1ec2e`,
at these paths:

- `plugins/grove/skills/grove-research-a/`
- `plugins/grove/skills/grove-research-b/`
- `plugins/grove/skills/grove-combine-research/`
- `plugins/grove/skills/grove/references/research.md`, which is now
  `plugins/research/skills/research-family/SKILL.md`

Grove keeps the full history of these files. This repository imports none of
it. The move changed the opening paragraph of each kind skill and added the
frontmatter of the family skill. It changed no other text.

## Licence

ResearchSkills uses the Apache License 2.0, as Grove does. The `LICENSE` file
holds the full text.
