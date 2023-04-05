# Eng-Chi-Project

This documents a few of my attempts to train a translator from English to Chinese using 10,000 paired sentences obtained from https://corpus.eduhk.hk/paraconc/, and architectures based on keras code examples. In short, I tried a few different methods involving an LSTM, which I was not able to train to a meaningful level. Eventually, I switched to a transformer-architecture, which I was able to train on my personal machine to the point that it could approximately translate very basic sentences.

-------------------------

# The data

The data was downloaded from https://corpus.eduhk.hk/paraconc/ in a .xls file with entries consisting of lines of the form "<tr><td>Alice in Wonderland / 愛麗絲夢遊仙境</td><td>In another moment down went Alice after it, never once considering how in the world she was to get out again.</td><td>不一會兒﹐愛麗絲也跟著鑽了進去﹐根本沒想過以後怎樣出來。</td></tr>".

-------------------------

# Earlier attempts

Before trying a transformer architecture, I tried training an LSTM. However, my machine could not handle training a large enough fraction of the data set for enough epochs, and the results were very poor. The output of the models I trained on LSTMs did not depend on the input I gave them, e.g. for any input the output was the string of characters “我们不是我的，我们不是我们的一个人,” which is basically nonsense.

To try to lighten the training load, I tried replacing the embedding layer with a pre-trained word embedding, but this still did not help very much. However, it did allow me to practice cleaning raw text so that it tokenizes properly.

-------------------------

# The transformer model

Finally, I tried adapting the model from https://github.com/keras-team/keras-io/blob/master/examples/nlp/neural_machine_translation_with_transformer.py. With this it was possible to train for 50 epochs on the full 10,000 paired sentences in ~4 hours. Unfortunately, the model still ended up over training, bu it was possible to see that the model learned many features of the language, e.g. producing the following translations:

"where is it?" -> "— — 現 在 哪 兒 ？" lit. "--where now?"

"who is he?" -> "他 是 誰" lit. "who is he?"

"where are you?" -> "你 去 什 麼 地 方 了 ？" lit. "which place did you go?"

"sit down" -> "坐 下 吧" lit. "sit down"

Unfortunately for even slightly more complicated sentences it produced many strange results, such as the following more nonsensical "translations":

"we went for a walk" -> "我 們 走 進 去 和 她 去 。"

"is that a dog?" -> "狗 做 完 全 大 海 豚 了 ？"

-------------------------

# Future directions

There are several natural things one could do to improve the model performance. The metrics show that on a test set accuracy and loss start to stagnate pretty quickly, which indicate overtraining. This is to be expected, since the training set is quite small. To build a functional translator would require much more data. Besides finding a larger data set, one strategy to explore would be implementing callbacks that modify the learning rate over time. 
