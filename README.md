# DLhw4

**files**

* data filter:https://github.com/qli74/ParlAI/blob/master/parlai/tasks/opensubtitles/build_2018.py
* P(S|T):https://github.com/qli74/ParlAI/blob/master/parlai/agents/transformer/generator_inv.py
* MMI:https://github.com/qli74/ParlAI/blob/master/parlai/agents/transformer/generatorMMI.py
* Mturk:https://github.com/qli74/ParlAI/tree/master/parlai/mturk/tasks/model_evaluator

**Clone the repo**
```
git clone https://github.com/qli74/ParlAI
cd ParlAI
python setup.py develop install
```

**Train the model**
 * ttim: training time, set to 100 for quick test
```
python -m parlai.scripts.train_model -t opensubtitles -mf tmp/transMMI_open -m transformer/generatorMMI -bs 4 --inference beam --beam-size 20 -lr 0.01 --variant xlm --dropout 0.3 -stim 10 -ttim 100
python -m parlai.scripts.train_model -t opensubtitles -mf tmp/transMMI_inv -m transformer/generator_inv -bs 4 --inference beam --beam-size 20 -lr 0.01 --variant xlm --dropout 0.3 -stim 10 -ttim 100
python -m parlai.scripts.train_model --init-model tmp/transMMI_open -t dailydialog -mf tmp/transMMI -m transformer/generatorMMI -bs 10 --inference beam --beam-size 20 -stim 10 -ttim 100 --variant xlm --dropout 0.3
```
**Mturk Evaluation**
```
python parlai/mturk/tasks/model_evaluator/run.py
```
Workers can score this model on Amazon Mturk. It looks like:

<img src="https://github.com/qli74/DLhw4/blob/master/im1.png" width="800" >

## Issues and future works
* All responses are the same and are not meaningful. The training parameters need be optimized. Pretrained model can be used to improve the results.

