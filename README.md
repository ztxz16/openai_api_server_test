## OpenAI API Server 性能测试程序

该测试是VLLM中的测试程序(https://github.com/vllm-project/vllm/blob/main/benchmarks/benchmark_serving.py)

## 测试流程

### 0. 下载测试数据集
可以从这里下载： https://hf-mirror.com/datasets/learnanything/sharegpt_v3_unfiltered_cleaned_split/tree/main

### 1. 打开一个VLLM Openai API Server

``` bash
python3 -m vllm.entrypoints.openai.api_server --gpu-memory-utilization 0.9 --disable-log-requests --host 127.0.0.1 --port 8000 --trust-remo
te-code --model /root/github/Qwen2-7B-Instruct/
# --model 指定的是模型存放在的目录，这里使用的Qwen2-7B-Instruct模型
```

### 2. 开始测试

``` bash
python benchmark_serving.py --dataset ./ShareGPT_V3_unfiltered_cleaned_split.json --base-url http://localhost:8000 --model /root/github/Qwen2-7B-Instruct --num-prompts=100
# 这里--model 指定的路径需要和server一致
```
