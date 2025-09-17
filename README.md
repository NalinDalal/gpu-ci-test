# Ephemeral GPU Runner (PoC)

This is a proof-of-concept repo to explore **ephemeral self-hosted GitHub Actions runners** for GPU testing.

## Goal

- Show that a self-hosted runner can:
  1. Register with GitHub Actions.
  2. Run a workflow job (mocked GPU test).
  3. Deregister/exit (ephemeral behavior).

Even though this MacBook Air M1 has an integrated GPU (not NVIDIA), the infra setup is the same — the "GPU test" is mocked for now.  
Later, someone with a proper GPU machine (CUDA, WebGPU, etc.) can replace the mock command with real tests.

## Current Workflow

- `.github/workflows/gpu-test.yml` runs a job on a self-hosted runner.
- The "GPU test" step just prints a fake `nvidia-smi` output.

```yaml
name: GPU Test
on: [push]

jobs:
  gpu-check:
    runs-on: self-hosted
    steps:
      - name: Simulate GPU availability
        run: echo "Simulating GPU check... GPU available ✅"
```

## Next Steps

- Run a self-hosted runner locally (MacBook).
- Push to this repo → workflow should run on the local runner.
- Later: containerize it for ephemeral lifecycle.

---

### Step 2. Create Workflow

Add file `.github/workflows/gpu-test.yml` with this content:

```yaml
name: GPU Test
on: [push]

jobs:
  gpu-check:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v4
      - name: Simulate GPU availability
        run: echo "Simulating GPU check... GPU available ✅"
```
