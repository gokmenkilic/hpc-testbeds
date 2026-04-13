---
name: "COSMA V100"
status: in-service
category: testbed
focus: discipline
focus-detail: "Prototyping and testing"
grouping: "COSMA"
funders:
- STFC
- DiRAC
- ExCALIBUR
partitions:
- nodes: 1
  accelerator: "NVIDIA V100 32GB"
  accelerator-count: 6
  manufacturer: "NVIDIA"
  scheduler: "Direct SSH"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 823
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
reference: https://cosma.readthedocs.io/en/latest/gpu.html
---

## COSMA V100

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The V100 node is a GPU testbed within COSMA, with 6x NVIDIA V100s.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| gn001 | 768GB | 2x Intel Xeon Gold 5218 | Direct SSH |

### Documentation

- <https://cosma.readthedocs.io/en/latest/gpu.html>
- <https://www.nvidia.com/en-gb/data-center/v100/>

### Gaining access

Access requires a COSMA account, obtained via the [DiRAC SAFE portal](https://safe.epcc.ed.ac.uk/dirac/).

1. Create a SAFE account with an institutional email.
2. Upload an SSH public key on SAFE. If you do not have one, generate with `ssh-keygen -t ed25519`.
2. Request a login account. This requires selecting a project, either:
- Project `do016` for NVIDIA GPU testbed access.
- A DiRAC project code for a given allocation (provided by a supervisor).
3. **Wait** for the account to be approved by the project manager. Keep an eye on your email!
4. Connect to COSMA via SSH: `ssh username@login8.cosma.dur.ac.uk` (Note: On first login you will be asked to change the password provided in your email)

Visit <https://cosma.readthedocs.io/en/latest/account.html> for more details.
Contact cosma-support@durham.ac.uk for any questions.

### Usage

Connect directly via SSH from a login node:
```bash
ssh gn001
nvidia-smi
./gpu_program_to_run
```

To use a single GPU, set `CUDA_VISIBLE_DEVICES`:
```bash
CUDA_VISIBLE_DEVICES=0 ./gpu_program_to_run
```

### Restrictions

- Nodes are non-exclusive by default (shared with other users). Use `--exclusive` if you require the entire node
- V100 (sm_70) requires older CUDA: `module load nvhpc/24.5`
