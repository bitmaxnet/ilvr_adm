# ILVR + ADM

This is the implementation of [ILVR: Conditioning Method for Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2108.02938) (ICCV 2021 Oral).

This repository is heavily based on [improved diffusion](https://github.com/openai/improved-diffusion) and [guided diffusion](https://github.com/openai/guided-diffusion).

# Download pre-trained models
Create a folder `models/` and download model checkpoints into it.
Here are the unconditional models trained on FFHQ and AFHQ-dog:

 * 256x256 FFHQ: [ffhq_10m.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/64x64_classifier.pt)
 * 256x256 AFHQ-dog: [afhq_dog_4m.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/64x64_diffusion.pt)

These models have seen 10M and 4M images respectively.
You may also try with models from [guided diffusion](https://github.com/openai/guided-diffusion).


# ILVR Sampling

Use the `ilvr_sample.py` script.
Here, we provide flags for sampling from above models.
Feel free to change --down_N and --range_t to adapt downsampling factor and conditioning range from our paper.

Refer to [improved diffusion](https://github.com/openai/improved-diffusion) for --timestep_respacing flag.

```
python scripts/ilvr_sample.py  --attention_resolutions 16 --class_cond False --diffusion_steps 1000 --dropout 0.0 --image_size 256 --learn_sigma True --noise_schedule linear --num_channels 128 --num_head_channels 64 --num_res_blocks 1 --resblock_updown True --use_fp16 False --use_scale_shift_norm True --timestep_respacing 100 --model_path models/ffhq_10m.pt --base_samples ref_imgs/face --down_N 32 --range_t 0 --save_dir output
```


# Results

These are samples generated with N=8 and 16:

![a](gif/full_face8_small.gif)
![b](gif/full_face16_small.gif)

These are cat-to-dog samples generated with N=32:

![c](gif/full_cat2dog_small.gif)


