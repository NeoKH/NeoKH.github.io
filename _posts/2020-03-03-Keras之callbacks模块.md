---
title: Keras之callbacks
tags:
  - Keras
---

今天在看PIE的训练代码，发现里面用到了三个`callbacks`函数：

```py
from keras.callbacks import EarlyStopping
from keras.callbacks import ModelCheckpoint
from keras.callbacks import ReduceLROnPlateau
```

于是记录一下自己找到的资料。

## callbacks是什么？

> A callback is a set of functions to be applied at **given stages of the  training procedure**（在特定的训练阶段）. You can use callbacks to **get a view on internal  states**(查看内部状态) and **statistics of the model**(统计模型) during training. You can **pass a list  of callbacks to the `.fit()` method** (你可以向`.fit函数`传递一个`回调函数列表`给`callbacks参数`) of the `Sequential` or `Model` classes. The relevant methods of the callbacks will then be called at each stage of the training. 



## ModelCheckpoint

```py
keras.callbacks.callbacks.ModelCheckpoint(
	filepath, 
	monitor='val_loss', 
	verbose=0, 
	save_best_only=False, 
	save_weights_only=False, 
	mode='auto', 
	period=1
)
```

- 功能：Save the model after every epoch.

- 参数：
  - filepath：字符串，保存模型的路径。`filepath` 可以包括命名格式选项，可以由 `epoch` 的值和 `logs` 的键（由 `on_epoch_end` 参数传递）来填充。例如：如果 `filepath` 是 `weights.{epoch:02d}-{val_loss:.2f}.hdf5`， 那么模型被保存的的文件名就会有训练轮数和验证损失。
  - monitor：被监测的数据。
  - verbose：详细信息模式，0 或者 1 。
  - save_best_only：如果 `save_best_only=True`， 被监测数据的最佳模型就不会被覆盖。
  - save_weights_only：如果为真，那么只有模型的权重会被保存 (`model.save_weights(filepath)`)； 否则，整个模型会被保存 (`model.save(filepath)`)。
  - mode： {auto, min, max} 的其中之一。 如果 `save_best_only=True`，那么是否覆盖保存文件的决定就取决于被监测数据的最大或者最小值。 对于 `val_acc`，模式就会是 `max`，而对于 `val_loss`，模式就需要是 `min`，等等。 在 `auto` 模式中，方向会自动从被监测的数据的名字中判断出来。
  - period：每个检查点之间的间隔（训练轮数）。

## EarlyStopping

```py
keras.callbacks.EarlyStopping(
	monitor='val_loss', 
	min_delta=0, 
	patience=0, 
	verbose=0, 
	mode='auto', 
	baseline=None, 
	restore_best_weights=False
)
```

- 功能：当被监测的数据不再增加，则停止训练。

- 参数：
  - **monitor**：被监测的数据。
  - **min_delta**：被监测数据被认为发生变化的最小增量，小于 min_delta 的绝对变化会被认为没有变化。
  - **patience**：一个整数，表示`epoch`数目。如果被检测数据在连续`patience`个`epoch`中都认为没有变化，则停止训练。需要注意的是，被检测数据可能不是每个epoch产生一次，即`model.fit`函数的参数`validation_freq`大于1时。
  - **verbose**：详细信息模式。
  - **mode**： 取值{auto, min, max} 其中之一。 在 `min` 模式中， 当被监测的数据停止下降，训练就会停止；在 `max` 模式中，当被监测的数据停止上升，训练就会停止；在 `auto` 模式中，方向会自动从被监测的数据的名字中判断出来。
  - **baseline**：被监控数据的基准值。如果模型没有比基准线显示出改进，那么训练将会停止。
  - **restore_best_weights**：是否从被监测数据的最佳值的时期恢复模型权重。 如果为 False，则使用在训练的最后一步获得的模型权重。

## ReduceLROnPlateau(自动降低学习率)

```py
keras.callbacks.ReduceLROnPlateau(
    monitor='val_loss', 
    factor=0.1, 
    patience=10, 
    verbose=0, 
    mode='auto', 
    min_delta=0.0001, 
    cooldown=0, 
    min_lr=0
)
```

- 功能：当标准评估停止提升时，降低学习速率。（因为一旦学习停滞不前，模型通常会受益于将学习率降低2-10倍。所以，该函数将检测数据，如果数据在`patience`个`epoch`里没有变化，则学习率降低）

- 参数：
  - monitor：被监测的数据。
  - factor：新的学习率 = 学习率 * factor
  - patience：一个整数，表示`epoch`数目。如果被检测数据在连续`patience`个`epoch`中都认为没有变化，则降低学习率。
  - verbose：整数。0: quiet, 1: update messages.
  - mode：{auto, min, max} 其中之一。如果是 `min` 模式，学习速率会被降低如果被监测的数据已经停止下降； 在 `max` 模式，学习塑料会被降低如果被监测的数据已经停止上升； 在 `auto` 模式，方向会被从被监测的数据中自动推断出来。
  - min_delta：小于该值的变化被认为没有变化。
  - cooldown：减少lr后恢复正常操作前等待的`epoch`数。
  - min_lr：学习率的下边界。

## TensorBoard

```py
keras.callbacks.TensorBoard(
	log_dir='./logs', 
	histogram_freq=0, 
	batch_size=32, 
	write_graph=True, 
	write_grads=False, 
	write_images=False, 
	embeddings_freq=0, 
	embeddings_layer_names=None, 
	embeddings_metadata=None, 
	embeddings_data=None, 
	update_freq='epoch'
)
```

