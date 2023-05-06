# 快速在服务器上部署大型语言对话模型(类似GPT)
>基于Chinese-Alpaca-Plus-7B官方项目改编：https://github.com/ymcui/Chinese-LLaMA-Alpaca  
>官方项目中除了Chinese-Alpaca-Plus-7B外还有多种型号  
>需要手动下载官方llama_7b_hf(13G)、chinese_llama_plus_lora_7b(790M)、chinese_alpaca_plus_lora_7b(1.1G)(共约15G)  
>合成后的模型chinese_alpaca_plus_7b_hf(13G)，建议预留30G存储空间  
>如在CPU上运行要有32GB内存；如在GPU上运行要有20GB内存  
## Chinese-Alpaca-Plus-7B介绍
>类似GPT一样有对话交互能力的大型语言模型  
>2022年facebook发布LLaMA-7B模型，此后中文团队训练出中文模型补丁  
>中文模型只是部分权重，原LLaMA-7B模型、Chinese-LLaMA-Plus-7B补丁、Chinese-Alpaca-Plus-7B补丁要合并后才可使用  
### 项目介绍
>本项目记录了在服务器上部署Chinese-Alpaca-Plus-7B模型的流程  
### 1，环境:linux
>torch==1.12.0：https://pytorch.org/get-started/previous-versions/  
>```
>pip install transformers sentencepiece -i https://pypi.doubanio.com/simple  
>pip install git+https://github.com/huggingface/peft  
>```
### 2，llama_to_hf.py
>将llama_7b模型转为HuggingFace格式(推荐直接下载已经转好的llama_7b_hf模型，详见*，llama_to_hf.py)  
>下载facebook官方llama_7b模型，包含tokenizer.model、tokenizer_checklist.chk、consolidated.*.pth、params.json  
>将tokenizer.model放到input_dir中，其余文件放入input_dir/model_size中，转换后保存在output_dir  
>```
>python llama_to_hf.py  --input_dir /TRAINING_CACHE/llama --model_size 7b --output_dir /TRAINING_CACHE/llama_7b_hf  
>```
### *，llama_to_hf.py
>huggingface地址：https://huggingface.co/decapoda-research/llama-7b-hf/tree/main  
>```
>sudo apt-get install git-lfs：安装git lfs  
>git lfs install：启用lfs。不使用lfs无法下载大文件  
>git clone https://huggingface.co/decapoda-research/llama-7b-hf：克隆项目  
>```
### 3，下载chinese_llama_plus_lora_7b
>百度网盘：https://pan.baidu.com/s/1zvyX9FN-WSRDdrtMARxxfw?pwd=2gtr  
>google网盘(外网)：https://drive.google.com/uc?id=1N97m3rBj-rp-J1X8rgRfluyomEscfAq0&export=download  
### 4，下载chinese_alpaca_plus_lora_7b
>百度网盘：https://pan.baidu.com/s/12tjjxmDWwLBM8Tj_7FAjHg?login_type=qzone&pwd=32hc&_at_=1683274834793  
>google网盘(外网)：https://drive.google.com/uc?id=1EDcTmq6tDmRxqarpapdyDGBE9opY0zrB&export=download  
### 5，merge_model.py
>合并llama_7b_hf、chinese_llama_plus_lora_7b、chinese_alpaca_plus_lora_7b  
>```
>python merge_model.py --base_model /TRAINING_CACHE/llama_7b_hf --lora_model /TRAINING_CACHE/chinese_llama_plus_lora_7b,/TRAINING_CACHE/chinese_alpaca_plus_lora_7b --output_type huggingface --output_dir /TRAINING_CACHE/chinese_alpaca_plus_7b_hf  
>```
>如果内存不够可使用缓存，命令中加上缓存路径```--offload_dir cache```  
### 6，inference_hf.py
>启动模型  
>```
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_7b_hf --with_prompt --interactive  
>```
### 其他
>github链接：https://github.com/TWK2022/ChineseAlpacaPlus7b  
>学习笔记：https://github.com/TWK2022/notebook  
>邮箱：1024565378@qq.com  