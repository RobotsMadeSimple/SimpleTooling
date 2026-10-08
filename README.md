# SimpleTooling

End-of-arm tooling for the [RobotsMadeSimple](https://github.com/RobotsMadeSimple) robot ecosystem.

Each top-level directory is a self-contained **tool**: a gripper, effector or other attachment that mounts on
the robot's end of arm (ASTRO's J4). A tool holds its print files (and, where relevant, docs and a BOM) so it
can be built on its own.

## Tools

| Tool | Description |
|------|-------------|
| [`ServoGripper`](ServoGripper) | Rack-and-pinion parallel gripper driven by a NEMA 17 stepper and GT2 pulley. |

## Repository layout

```
<ToolName>/
  README.md           # parts list, hardware, mounting options
  Print Files/        # STL / CAD files to print or machine
  CAD/                # assembled STEP file (optional)
```

## Git LFS

3D geometry (`.stl`, `.step`/`.stp`, `.3mf`, `.f3d`/`.f3z`, `.obj`) is stored in **[Git LFS](https://git-lfs.com/)**.
Install it once before cloning so you get the real files instead of pointer stubs:

```bash
git lfs install
git clone https://github.com/RobotsMadeSimple/SimpleTooling.git
```

If you cloned before installing LFS, run `git lfs pull` to fetch the binaries.

## Print-file releases

Every tool's print files are published as a downloadable ZIP under
[Releases](https://github.com/RobotsMadeSimple/SimpleTooling/releases), so you can grab a tool's files without
cloning the repo or installing LFS.

Packaging is automated: on every push to `main`, a GitHub Action detects which tool directories changed and
rebuilds **only those** releases. Each tool has one rolling release tagged with the tool name (e.g.
`ServoGripper`), whose ZIP assets are overwritten with the latest files: `<Tool>-print-files.zip` (the `Print Files/` folder) and,
when the tool has an assembled STEP in `CAD/`, `<Tool>-step-files.zip`. Each zip has a `VERSION.txt` naming the
commit it was built from.

## Adding a tool

1. Create a new top-level directory named after the tool.
2. Put its print files under `<ToolName>/Print Files/`.
3. Open a PR; when it merges to `main`, the Action creates/updates the tool's release automatically.
