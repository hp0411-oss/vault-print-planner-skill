# VAULT Print Planner Skill

English | [简体中文](README.zh-CN.md)

A local bilingual planner and Codex skill for USSA VAULT modular drawers and storage boxes. Configure complete builds or accessories, inspect simplified 3D assemblies and actual STL parts, save and restore print tasks, track completed sets, and export Bambu Studio 3MF projects.

Download **vault-print-planner-skill.zip** from this repository and extract it first. Paths below refer to the extracted folder.

## Chinese / English switch

Use the language selector at the top right of the planner. Your current configuration and accessory quantities carry over, and the browser remembers your language. Both versions share the same saved tasks and print records. User-entered names, notes, original filenames, and images from the original manuals retain their original language. Save progress-record edits before switching languages.

## Run the standalone planner

Requires Python 3.11+, initialized Bambu Studio profiles, and your own legally obtained VAULT model archive and manuals. Model files are not included. See the model and manual policy below.

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python skills/vault-print-planner/scripts/launch.py --archive '/path/to/VAULT' --port 8766
```

Open http://127.0.0.1:8766/planner.html in Chrome or another browser. On Windows, use `.venv\Scripts\python.exe`. The automatic Open in Bambu Studio action currently supports macOS only; open exported 3MF files manually on other systems. Keep the local server running. Do not expose this unauthenticated service to the public internet.

## Model purchase, local deployment, and manuals

**This tool does not include or distribute VAULT model files. Each user must purchase the models from the designer or an authorized seller and comply with the model license.** Download and extract your purchased archive on your own computer, then pass that local folder to `--archive`. This tool and its AGPL license do not grant rights to the VAULT models.

Keep model files and anything containing their geometry local: STL/STEP/3MF files, converted meshes, print projects, and model archives must not be uploaded to this repository or included in release packages. The local planner reads your archive to preview parts and prepare print projects; it does not require uploading the models to GitHub.

Manuals may be used as reference material for selection, printing, and assembly. Read the user’s local manuals when needed. A manual may also be included as a reference resource when its redistribution is permitted by the rights holder; permission to use a local manual is not automatically permission to republish it. No third-party manuals are bundled in the current package.

## Install the skill

Copy `skills/vault-print-planner` into `~/.codex/skills/` (or your `$CODEX_HOME/skills/` folder). Start a new session and invoke `$vault-print-planner`.

Example: “Use $vault-print-planner to configure an M5 drawer build, add two replacement baseplates, and check clearance from the front purge line.”

## Printing scope

The planner targets the P1S, 0.4 / 0.6 mm nozzles, and PLA / PETG. Exporting or opening a project does not start printing. A 3MF export still needs slicer inspection: verify the actual printer, nozzle, filament, plate, AMS mapping, start G-code, brim, and supports.

The packaged planner includes conservative front and edge clearances. Larger parts may require manual layout or separate plates; never scale assembly parts to fit. Old exported projects do not automatically receive updated clearances. Simplified previews do not validate dimensions, assembly tolerances, motion, load capacity, or stability.

## Development

Chinese frontend sources are `planner.html`, `planner-preview.js`, and `planner-overview.js` under `skills/vault-print-planner/assets/app/`. Edit `tools/translations.tsv` and run `python3 tools/build_languages.py` to regenerate English assets and the response translation dictionary. System messages are translated; user-authored text and model paths are preserved. The original upstream configurator is separate from the bilingual planner.

## Credits and license

Based on a downloaded version of [marcelfarres/vault-configurator](https://github.com/marcelfarres/vault-configurator), under [GNU AGPL v3](LICENSE). Additions include the bilingual planner, accessory-only mode, task deletion and recovery, completion records, assembly previews, skill instructions, and conservative P1S clearances. This package does not retain upstream Git history or claim a verified upstream commit.

Three.js retains its bundled license. VAULT models, manuals, and brands belong to USSA Design and are not licensed by this repository. This is not an official USSA Design or Bambu Lab product. Designer print statistics are excluded; the slicer is authoritative for weight and time.

Models, generated files, caches, personal paths, and print records remain local and are excluded by `.gitignore`.
