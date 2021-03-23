## Instructions

* install requirements (requires `master` branch of `transformers)

  `pip install wandb datasets==1.4.1 torchaudio librosa jiwer`
  `pip install git+https://github.com/huggingface/transformers`
  `pip install --upgrade torch==1.8.0+cu111 torchvision==0.9.0+cu111 torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html`

  Note: use your torch install instructions (without it I was getting some cudnn issues). Also it's always good to use a virtual env (I like pipenv).

* define your sweep configuration file (see `sweep.yaml`)

* update `train.py` if you want

* create a sweep -> this will return a sweep id

  `wandb sweep sweep.yaml`

* launch an agent against the sweep (see the return from previous command)

  `wandb agent my_sweep_yd`

  Note: you can launch as many agents as your machine handles, and use other machines. Just don't recreate another sweep and use the same sweep id.

## TODO

* apply [this trick](https://huggingface.slack.com/archives/C01QZ90Q83Z/p1616343320403900) to avoid reprocessing data but with torchaudio
* find a better way than early stopping callback to stop training if loss is NaN:
  * build a custom callback?
  * raise an exception within the logging callback -> should be easy but hacky (no problem with that!)
* upload tokenizer and preprocessor files ("extra" folder) as W&B artifacts at the end of training (currently only best model files are uploaded)
* show how to use sweeps in a notebook (it uses slightly more resources which was creating issues on my local machine and pushed me towards the "script" route)