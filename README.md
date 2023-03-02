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

