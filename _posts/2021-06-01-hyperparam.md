---
layout: post
title: Hyperparameter Tuning in Tensorflow With Hparams Dashboard
date: 2021-06-01 21:01:00
description:
tags: code
categories: tech
---

The term `hyperparameter` is widely used when building machine learning models. The hyperparameters are those parameters on which other parameters, such as model weights and bias, depend. Examples of hyperparameters are learning rate, optimizer, number of hidden layers, number of neurons in each hidden layer, etc. Therefore, it is crucial to find the optimal set of hyperparameters for your problem, which often occurs through an experimentation process known as `Hyperparameter Tuning.`

Tensorboard provides several tools through the Hparams dashboard to help seek the best hyperparameters through experimentation. You can follow up on the tutorial [here](https://www.tensorflow.org/tensorboard/hyperparameter_tuning_with_hparams).

## Contents

- [Contents](#contents)
- [The usual way](#the-usual-way)
- [Refactoring - without using nested loops](#refactoring---without-using-nested-loops)
- [If you are not a fan of tensorboard](#if-you-are-not-a-fan-of-tensorboard)
- [References](#references)

## The usual way

You may have to write multiple for loops to go through each hyperparameter, which you may want to avoid.

```python
HP_NUM_UNITS = hp.HParam('num_units', hp.Discrete([16, 32]))
HP_DROPOUT = hp.HParam('dropout', hp.RealInterval(0.1, 0.2))
HP_OPTIMIZER = hp.HParam('optimizer', hp.Discrete(['adam', 'sgd']))
METRIC_ACCURACY = 'loss'

...

for num_units in HP_NUM_UNITS.domain.values:
  for dropout_rate in (HP_DROPOUT.domain.min_value, HP_DROPOUT.domain.max_value):
    for optimizer in HP_OPTIMIZER.domain.values:
      hparams = {
          HP_NUM_UNITS: num_units,
          HP_DROPOUT: dropout_rate,
          HP_OPTIMIZER: optimizer,
      }
      print({h.name: hparams[h] for h in hparams})
      # run model with hparams
      session_num += 1
```

---

## Refactoring - without using nested loops

A way to refactor the above code could be using the product() function from the itertools module. This function finds the cartesian product of multiple sets i.e returns each possible combination of set elements.

```python
from itertools import product
param_values = [HP_NUM_UNITS.domain.values, [d for d in (HP_DROPOUT.domain.min_value, HP_DROPOUT.domain.max_value)],
                HP_OPTIMIZER.domain.values]
print(param_values)
>>> [[16, 32], [0.1, 0.2], ['adam', 'sgd']]
list(product(*param_values))
>>> [(16, 0.1, 'adam'),
(16, 0.1, 'sgd'),
(16, 0.2, 'adam'),
(16, 0.2, 'sgd'),
(32, 0.1, 'adam'),
(32, 0.1, 'sgd'),
(32, 0.2, 'adam'),
(32, 0.2, 'sgd')]
```

A single for loop can then be used to iterate over all combinations of hyperparameters.

```python
for num_units, dropout_rate, optimizer in list(product(*param_values)):
	hparams = {
	        HP_NUM_UNITS: num_units,
	        HP_DROPOUT: dropout_rate,
	        HP_OPTIMIZER: optimizer,
	    }
	run_name = "run-%d" % session_num
	print({h.name: hparams[h] for h in hparams})
	# run model with hparams
	session_num += 1
```

---

## If you are not a fan of tensorboard

We'll save all the data ourselves, so we can analyze it outside TensorBoard. We can utilize the panda's data frame to keep all crucial parameters. It is recommended to use classes and objects for implementing the models. Here's an example:

```python
def model(self, ...):
    ...

    results = OrderedDict()
    results["run"] = self.run_count
    results["epoch"] = self.epoch_count
    results['loss'] = loss
    results["accuracy"] = accuracy
    results['epoch duration'] = epoch_duration
    results['batch size'] = run_duration
    for k,v in self.run_params._asdict().items(): results[k] = v
    self.run_data.append(results)

    df = pd.DataFrame.from_dict(self.run_data, orient='columns')

    ...
```

| run | epoch | loss  | accuracy | epoch duration | batch size |
| --- | ----- | ----- | -------- | -------------- | ---------- |
| 1   | 1     | 0.994 | 0.621    | 20.2           | 1024       |
| 1   | 2     | 0.546 | 0.814    | 19.3           | 1024       |
| 1   | 3     | 0.434 | 0.825    | 20.5           | 1024       |

---

## References

[Deep Lizard - Hyperparameter Tuning and Experimenting - Training Deep Neural Networks](https://deeplizard.com/learn/video/ycxulUVoNbk)

[Deep Lizard - CNN Training Loop Refactoring - Simultaneous Hyperparameter Testing](https://deeplizard.com/learn/video/ozpv_peZ894)
