# 快速在服务器上部署大型语言对话模型(类似GPT)
>基于Chinese-Alpaca-Plus-7B官方项目改编:https://github.com/ymcui/Chinese-LLaMA-Alpaca  
>官方项目中除了Chinese-Alpaca-Plus-7B外还有多种型号  
>需要手动下载官方原LLaMA、Chinese-LLaMA-Plus-7B、Chinese-Alpaca-Plus-7B(共约28G)  
>如在CPU上运行要有32GB内存；如在GPU上运行要有20GB内存  
## Chinese-Alpaca-Plus-7B介绍
>类似GPT一样有对话交互能力的大型语言模型  
>中文团队根据2023年facebook发布的LLaMA-7B模型用中文数据集训练的中文模型补丁  
>只是部分权重，要与原LLaMA-7B模型、合并后才可使用  
### 项目介绍
>本项目将建立图片特征数据库，然后用文本描述(75字以内，长的会被截断)去搜索符合描述的图片  