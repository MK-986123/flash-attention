# GitHub Workflows for Flash Attention

This directory contains GitHub Actions workflows for building and testing Flash Attention.

## Available Workflows

### Build PyTorch 2.9.0 + CUDA 13.0 wheel (`build-pytorch29-cu130.yml`)

This workflow builds Flash Attention wheels specifically for PyTorch 2.9.0 development builds with CUDA 13.0 support.

#### How to run this workflow

1. **Via GitHub Web Interface:**
   - Go to the [Actions tab](../../actions) in the GitHub repository
   - Select "Build PyTorch 2.9.0 + CUDA 13.0 wheel" from the workflow list
   - Click "Run workflow" button
   - Fill in the parameters (or use defaults):
     - **runs-on**: Runner type (default: `ubuntu-22.04`)
     - **python-version**: Python version (default: `3.12`)
     - **cuda-version**: CUDA version (default: `13.0.0`)
     - **torch-version**: PyTorch version (default: `2.9.0.dev`)
     - **cxx11_abi**: C++11 ABI flag (default: `1`)
     - **upload-to-release**: Whether to upload to a release (default: `false`)
     - **release-version**: Release version if uploading (optional)
   - Click "Run workflow"

2. **Via GitHub CLI:**
   ```bash
   gh workflow run "Build PyTorch 2.9.0 + CUDA 13.0 wheel" \
     --field runs-on=ubuntu-22.04 \
     --field python-version=3.12 \
     --field cuda-version=13.0.0 \
     --field torch-version=2.9.0.dev \
     --field cxx11_abi=1
   ```

3. **Via REST API:**
   ```bash
   curl -X POST \
     -H "Accept: application/vnd.github.v3+json" \
     -H "Authorization: token YOUR_TOKEN" \
     https://api.github.com/repos/MK-986123/flash-attention/actions/workflows/build-pytorch29-cu130.yml/dispatches \
     -d '{
       "ref": "main",
       "inputs": {
         "runs-on": "ubuntu-22.04",
         "python-version": "3.12",
         "cuda-version": "13.0.0",
         "torch-version": "2.9.0.dev",
         "cxx11_abi": "1"
       }
     }'
   ```

#### What this workflow does

- Sets up a Linux environment with the specified Python version
- Installs CUDA 13.0 toolkit
- Installs PyTorch 2.9.0 development build
- Builds Flash Attention wheel with the specified configuration
- Optionally uploads the built wheel to a GitHub release

#### Requirements

- GitHub repository with Actions enabled
- Appropriate permissions to run workflows
- For release uploads: valid release tag

## Other Workflows

- **`build.yml`**: Generic wheel building workflow with customizable parameters
- **`publish.yml`**: Automated wheel building and publishing on release tags
- **`main.yml`**: Main CI workflow for Windows builds
- **`_build.yml`**: Reusable workflow template for building wheels
- **`pytorch2.9.0+cu130-linux-py312.yaml`**: Specialized template for PyTorch 2.9.0 builds

## Troubleshooting

If you encounter issues running the workflow:

1. Check that you have the necessary permissions to run workflows in the repository
2. Verify that the branch you're running from has the workflow file
3. Check the Actions tab for detailed error logs
4. Ensure all required inputs are provided with valid values

For build-specific issues, check the build logs in the workflow run details.