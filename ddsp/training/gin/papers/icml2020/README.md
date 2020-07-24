# Self-supervised Pitch Detection by Inverse Audio Synthesis
_ICML SAS Workshop 2020, ([paper](https://openreview.net/forum?id=RlVTYWhsky7))_

Gin configs for reproducing the results of the paper.

## Generate synthetic dataset

After pip installing ddsp, create a synthetic dataset for the transcribing autoencoder using the installed script:
```bash
ddsp_generate_synthetic_dataset \
--output_tfrecord_path=/tmp/synthetic_data.tfrecord \
--gin_file=papers/icml2020/generate_synthetic_dataset.gin \
--num_shards=1000 \
--num_examples=10000000 \
--alsologtostderr
```



## Pretrain transcribing autoencoder

### Train
Point the dataset file_pattern to the synthetic dataset created above.

```bash
ddsp_run \
--mode=train \
--save_dir=/tmp/$USER-tae-pretrain-0 \
--gin_file=papers/icml2020/pretrain_model.gin \
--gin_file=papers/icml2020/pretrain_dataset.gin \
--gin_param="SyntheticNotes.file_pattern='/tmp/synthetic_dataset.tfrecord*'"
--gin_param="batch_size=16" \
--alsologtostderr
```




