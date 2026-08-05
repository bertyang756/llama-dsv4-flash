# DeepSeek v4 Flash experimental support for 170HX

This is a fork of a fork of llama.cpp that implements DSv4 support, to load DeepSeek v4 Flash GGUF that uses 2bit quantization of routed experts, to fit in combined RAM+VRAM <100GB, and **runs on 170HX with 610.43.03 driver and CUDA 13.3**.

Based on https://github.com/antirez/llama.cpp-deepseek-v4-flash, and models from https://huggingface.co/antirez/deepseek-v4-gguf

I meet a few bugs from directly using antirez's codes, so I created this fork and fixed them with help of DeepSeek v4 Pro.

I have only tested Qwen3.5-9B-Q4_K_M.gguf and DeepSeek-V4-Flash-IQ2XXS-w2Q2K-AProjQ8-SExpQ8-OutQ8-chat-v2-imatrix-0731.gguf under ubuntu 26 using CUDA13.3. 
 - The Qwen 9B model would fully load into VRAM, and output speed starts about 98tokens/s.
 - DeepSeek-V4-Flash loaded with --n-cpu-moe 12 --flash-attn on, would take around 62GB VRAM + 24GB RAM, some of MoE computation would be moved to CPU, and output speed starts about 10.5tokens/s. (Ryzen 7700 CPU + 24GB DDR5 5600*2) (For a quick comparison, 3090 24G VRAM + 245K + 48GB DDR5 6800*2 with --n-cpu-moe 38 would also output ~10tokens/s)
