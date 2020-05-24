# MXNet extension for OpenML python

MXNet extension for [openml-python API](https://github.com/openml/openml-python).

#### Installation Instructions:

`pip install openml-keras`

PyPi link https://pypi.org/project/openml-mxnet/

#### Usage
Import openML libraries
```python
import openml
import openml_mxnet
```
Create a MXNet model
```python
model = mxnet.gluon.nn.HybridSequential()
with model.name_scope():
    model.add(mxnet.gluon.nn.BatchNorm())
    model.add(mxnet.gluon.nn.Dense(units=1024, activation="relu"))
    model.add(mxnet.gluon.nn.Dropout(rate=0.4))
    model.add(mxnet.gluon.nn.Dense(units=2))
model.hybridize()
```
Download the task from openML and run the model on task.
```python
task = openml.tasks.get_task(3573)
run = openml.runs.run_model_on_task(model, task, avoid_duplicate_runs=False)
run.publish()
print('URL for run: %s/run/%d' % (openml.config.server, run.run_id))
```
