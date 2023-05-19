#### 使用半精度加载模型

model = LlamaForCausalLM.from_pretrained(model_path, device_map="auto", torch_dtype=torch.half)
