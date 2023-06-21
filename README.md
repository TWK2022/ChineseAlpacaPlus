## 快速在Linux上部署大型中文对话模型(chatGPT)
>基于Chinese-Alpaca-Plus官方项目改编：https://github.com/ymcui/Chinese-LLaMA-Alpaca  
>有Chinese-Alpaca-Plus-7B(14G)和Chinese-Alpaca-Plus-13B(27G)  
>支持CPU和GPU运行，GPU占用：Chinese-Alpaca-Plus-7B(14500M)、Chinese-Alpaca-Plus-13B(26500M)  
### Chinese-Alpaca-Plus介绍
>有对话交互能力的大型语言模型  
>2022年facebook发布LLaMA模型，此后中文团队训练出中文模型补丁  
>中文模型只是部分权重，原LLaMA-7B模型(13G)、Chinese-LLaMA-Plus-7B补丁(790M)、Chinese-Alpaca-Plus-7B补丁(1.1G)要合并后才可使用  
>中文模型只是部分权重，原LLaMA-13B模型(38G)、Chinese-LLaMA-Plus-13B补丁(1G)、Chinese-Alpaca-Plus-13B补丁(1.3G)要合并后才可使用  
### 项目介绍
>本项目记录了在Linux上部署Chinese-Alpaca-Plus-7B和Chinese-Alpaca-Plus-13B模型的流程  
>如果直接下载合并好的chinese_alpaca_plus_7b_hf模型(推荐)，可直接使用模型，详见(*，直接下载chinese_alpaca_plus_7b_hf或chinese_alpaca_plus_13b_hf)  
### 1.环境：linux
>torch==1.12.0：https://pytorch.org/get-started/previous-versions/  
>```
>pip install transformers sentencepiece -i https://pypi.doubanio.com/simple
>pip install git+https://github.com/huggingface/peft
>```
### 2.下载llama_7b_hf(13G)或llama_13b_hf(38G)
>llama_7b_hf(13G)地址：https://huggingface.co/decapoda-research/llama-7b-hf  
>llama_13b_hf(G)地址：https://huggingface.co/decapoda-research/llama-13b-hf  
>```
>sudo apt-get install git-lfs：安装git-lfs
>git lfs install：启用lfs。不使用lfs无法下载大文件
>git clone https://huggingface.co/decapoda-research/llama-7b-hf：下载模型llama_7b_hf
>git clone https://huggingface.co/decapoda-research/llama-13b-hf：下载模型llama_13b_hf
>```
### 3.下载chinese_llama_plus_lora_7b(790M)或chinese_llama_plus_lora_13b(1G)
>chinese_llama_plus_lora_7b：  
>百度网盘：https://pan.baidu.com/s/1zvyX9FN-WSRDdrtMARxxfw?pwd=2gtr  
>google网盘(外网)：https://drive.google.com/uc?id=1N97m3rBj-rp-J1X8rgRfluyomEscfAq0&export=download  
>  
>chinese_llama_plus_lora_13b：  
>百度网盘：https://pan.baidu.com/s/1VGpNlrLx5zHuNzLOcTG-xw?pwd=8cvd  
>google网盘(外网)：https://drive.google.com/uc?id=1q0L5Me_1j_9iiRRNfuEFUt3SOjQo3-g3&export=download  
### 4.下载chinese_alpaca_plus_lora_7b(1.1G)或chinese_alpaca_plus_lora_13b(1.3G)
>chinese_alpaca_plus_lora_7b：  
>百度网盘：https://pan.baidu.com/s/12tjjxmDWwLBM8Tj_7FAjHg?login_type=qzone&pwd=32hc&_at_=1683274834793  
>google网盘(外网)：https://drive.google.com/uc?id=1EDcTmq6tDmRxqarpapdyDGBE9opY0zrB&export=download  
>  
>chinese_alpaca_plus_lora_13b：  
>百度网盘：https://pan.baidu.com/s/1Mew4EjBlejWBBB6_WW6vig?pwd=mf5w  
>google网盘(外网)：https://drive.google.com/uc?id=1CcLJvY7XsFAOjfSIqCpDI7jf3EEPDcEF&export=download  
### 5.merge_model.py
>合并llama_7b_hf、chinese_llama_plus_lora_7b、chinese_alpaca_plus_lora_7b为chinese_alpaca_plus_7b_hf  
>合并llama_13b_hf、chinese_llama_plus_lora_13b、chinese_alpaca_plus_lora_13b为chinese_alpaca_plus_13b_hf  
>```
>python merge_model.py --base_model /TRAINING_CACHE/llama_7b_hf --lora_model /TRAINING_CACHE/chinese_llama_plus_lora_7b,/TRAINING_CACHE/chinese_alpaca_plus_lora_7b --output_type huggingface --output_dir /TRAINING_CACHE/chinese_alpaca_plus_7b_hf
>python merge_model.py --base_model /TRAINING_CACHE/llama_13b_hf --lora_model /TRAINING_CACHE/chinese_llama_plus_lora_13b,/TRAINING_CACHE/chinese_alpaca_plus_lora_13b --output_type huggingface --output_dir /TRAINING_CACHE/chinese_alpaca_plus_13b_hf
>--offload_dir cache：如果内存不够可使用缓存，命令中加上缓存路径
>```
### *.直接下载chinese_alpaca_plus_7b_hf(14G)或chinese_alpaca_plus_13b_hf(27G)
>使用huggingface上别人合并好上传的chinese_alpaca_plus_7b/13b_hf模型，若不能使用，可以找找其他的或手动合并  
>chinese_alpaca_plus_7b地址：https://huggingface.co/shibing624/chinese-alpaca-plus-7b  
>chinese_alpaca_plus_13b地址：https://huggingface.co/shibing624/chinese-alpaca-plus-13b-hf  
>```
>sudo apt-get install git-lfs：安装git-lfs
>git lfs install：启用lfs，不使用lfs无法下载大文件
>git clone https://huggingface.co/shibing624/chinese-alpaca-plus-7b：下载模型chinese_alpaca_plus_7b_hf
>git clone https://huggingface.co/shibing624/chinese-alpaca-plus-13b：下载模型chinese_alpaca_plus_13b_hf
>```
### 6.inference_hf.py
>启动模型  
>交互式：  
>```
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_7b_hf --with_prompt --interactive
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_13b_hf --with_prompt --interactive
>```
>读取文本式：  
>```
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_7b_hf --with_prompt --data_file data.txt
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_13b_hf --with_prompt --data_file data.txt
>--data_file：待预测数据，按行读取
>```
### 更多模型和功能
>请参考原项目：https://github.com/ymcui/Chinese-LLaMA-Alpaca  
### 其他
>github链接：https://github.com/TWK2022/ChineseAlpacaPlus  
>学习笔记：https://github.com/TWK2022/notebook  
>邮箱：1024565378@qq.com  