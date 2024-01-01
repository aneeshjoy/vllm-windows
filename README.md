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


6. Check throughput ( I am running on a RTX 3090 )

http://127.0.0.1:8000/metrics

```
# HELP exceptions_total_counter Total number of requested which generated an exception
# TYPE exceptions_total_counter counter
# HELP requests_total_counter Total number of requests received
# TYPE requests_total_counter counter
requests_total_counter{method="POST",path="/v1/completions"} 24
# HELP responses_total_counter Total number of responses sent
# TYPE responses_total_counter counter
responses_total_counter{method="POST",path="/v1/completions"} 24
# HELP status_codes_counter Total number of response status codes
# TYPE status_codes_counter counter
status_codes_counter{method="POST",path="/v1/completions",status_code="200"} 24
# HELP vllm:avg_generation_throughput_toks_per_s Average generation throughput in tokens/s.
# TYPE vllm:avg_generation_throughput_toks_per_s gauge
vllm:avg_generation_throughput_toks_per_s{model_name="/models/mistral-7b"} 842.7750196184555
# HELP vllm:avg_prompt_throughput_toks_per_s Average prefill throughput in tokens/s.
# TYPE vllm:avg_prompt_throughput_toks_per_s gauge
vllm:avg_prompt_throughput_toks_per_s{model_name="/models/mistral-7b"} 1211.5997677115236
# HELP vllm:cpu_cache_usage_perc CPU KV-cache usage. 1 means 100 percent usage.
# TYPE vllm:cpu_cache_usage_perc gauge
vllm:cpu_cache_usage_perc{model_name="/models/mistral-7b"} 0.0
# HELP vllm:gpu_cache_usage_perc GPU KV-cache usage. 1 means 100 percent usage.
# TYPE vllm:gpu_cache_usage_perc gauge
vllm:gpu_cache_usage_perc{model_name="/models/mistral-7b"} 0.38849487785658
# HELP vllm:num_requests_running Number of requests that is currently running for inference.
```
