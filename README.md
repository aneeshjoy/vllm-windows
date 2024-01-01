# Welcome to vLLM Windows Home!
This repository contains a Docker Compose setup for running vLLM on Windows. With this setup, you can easily run and experiment with vLLM on Windows Home.

Enjoy the state-of-the art LLM serving throughput on your Windows Home PC with efficient paged attention, continuous batching and fast inferencing, Plus Qualitzation.

![vllm-windows-home](https://github.com/aneeshjoy/vllm-windows/assets/5285961/5b9caae0-1cfd-4fb4-b86f-a8330e8428f0)

Once the following is setup, you can start vLLM on the click of a button on Docker Desktop or configure to start at windows startup.

## Getting Started
### Prerequisites
Docker Desktop: 
Install Docker Desktop from <https://www.docker.com/products/docker-desktop>

Note: Windows Home uses WSL as backend engine.

### Steps
1. Clone the Repository
```bash
git clone https://github.com/aneeshjoy/vllm-windows.git
cd vllm-windows
```

2. Update Hugging Face Token
Open `docker-compose.yml` and replace `<hugging_face_token>` with your own Hugging Face token. The format should be like this:

```yaml
  environment:
    - HUGGING_FACE_HUB_TOKEN=<hugging_face_token>
```

3. Copy Model Weights
Download or copy the desired LLM model weights into the `models` directory within the cloned repository and update the model name.
```yaml
  command: --model /models/mistral-7b
```
4. Simply execute the following command at the root level of the project:

```bash
docker-compose up
```
5. Test by accessing the /models endpoints

http://127.0.0.1:8000/v1/models

