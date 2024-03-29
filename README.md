# ARDN: Attention Re-distribution Network for Visual Question Answering


### Training

**Train model on VQA-v2/GQA with default hyperparameters:**

```bash
 python run.py --RUN='train' --MODEL='mcan_small' --DATASET='vqa'
```
and the training log will be seved to:

```
results/log/log_run_<VERSION>.txt
```
Args:
- `--MODEL={'mcan_small', 'trar'}` to choose the base model for training.
- `--DATASET={'vqa', 'gqa'}` to choose the task for training.
- `--GPU=str`, e.g. `--GPU='2'` to train model on specific GPU device.
- `--SPLIT={'train', 'train+val', train+val+vg'}`, which combines different training datasets. When the task is `vqa`, our experiment sets `'train+val+vg'`; When the task is `gqa`, our experimental setting is `'train+val'`.
- `--MAX_EPOCH=int` to set the total training epoch number. VQA task, default is 13 epochs; The default GQA task is 11 epochs.




**Resume Training**

Resume training from specific saved model weights
```bash
python run.py --RUN='train' --DATASET='vqa' --MODEL='mcan_small' --RESUME=True --CKPT_V=str --CKPT_E=int
```
- `--CKPT_V=str`: the specific checkpoint version.
- `--CKPT_E=int`: the resumed epoch number.

**Multi-GPU Training and Gradient Accumulation**
1. Multi-GPU Training:
Add `--GPU='0, 1, 2, 3...'` after the training scripts.
```bash
python3 run.py --RUN='train' --DATASET='vqa' --MODEL='mcan_small' --GPU='0,1,2,3'
```
The batch size on each GPU will be divided into `BATCH_SIZE/GPUs` automatically.
**Online Testing**
All the evaluations on the `test` dataset of the VQA-v2 benchmark can be achieved as follows:

```bash
python run.py --RUN='test' --MODEL='lsat' --DATASET='{vqa}' --CKPT_V=str --CKPT_E=int
```

Result file are saved at:

`results/result_test/result_run_<CKPT_V>_<CKPT_E>.json`

You can upload the obtained result json file to [Eval AI](https://evalai.cloudcv.org/web/challenges) to evaluate the scores.



## Acknowledgements
- [openvqa](https://github.com/MILVLG/openvqa)
- [grid-feats-vqa](https://github.com/facebookresearch/grid-feats-vqa)
- [TRAR](https://github.com/rentainhe/TRAR-VQA)

