# TripoSF-devcontainer

This repository offers a simple way to run TripoSF in a Docker environment.

## Requirements
* Docker ([rootless](https://docs.docker.com/engine/security/rootless) is even better)
* [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
* VSCode with the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension installed

## Usage
1. Pull TripoSF submodule:
```bash
git submodule update --init --recursive
```
2. In the `.devcontainer/devcontainer.json` file, update the mounts configuration with your models data root:
```json
"mounts": [
  "source=${localEnv:HOME}/Path/To/My/Models/TripoSF/vae,target=/home/vscode/TripoSF/ckpts,type=bind,readonly"
]
```
3. Navigate to TripoSF and run the demo generation:
```bash
cd TripoSF && python inference.py --mesh-path "assets/examples/jacket.obj" --output-dir "outputs/" --config "configs/TripoSFVAE_1024.yaml"
```

## Building and running the image manually
```bash
docker build . -t triposf-devcontainer -f .devcontainer/Dockerfile
docker run -it --name triposf --gpus all --mount type=bind,src=.,dst=/home/vscode --mount type=bind,src=$HOME/Path/To/My/Models/TripoSF/vae,dst=/home/vscode/TripoSF/ckpts,ro triposf-devcontainer
cd /home/vscode/TripoSF && python inference.py --mesh-path "assets/examples/jacket.obj" --output-dir "outputs/" --config "configs/TripoSFVAE_1024.yaml"
```
