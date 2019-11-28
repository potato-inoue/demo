# Demo of speech sample

- End-to-End音声認識を用いたEnd-to-End音声合成の性能評価
- 井上 勝喜, 原 直, 阿部 匡伸, 渡部 晋治

<!-- ## Abstract  -->

## モデル

### End-to-End TTS (speaker-dependent model)

- Dataset: The LJ speech dataset [1]
- Language: English
- Total sentence: 13100 文
- Total duration: 約24 時間
- Trainin data： 12100 文
- Validation data: 500 文
- Test data: 500 文

| モデル | 概要 |  
| --- | --- |  
| Tacotron2.v2 | Tacotron2 (RNN) [2]，Forward attention, transition agent [3] |  
| Tacotron2.v3 | Tacotron2 (RNN)，Location attention [4], Guided attention loss [5] |  
| Transformer.v1 | Transformer (self-attention) [6]，Guided attention loss |  
| FastSpeech.v2 | FastSpeech (self-attention) [7]，教師モデル：Trasformer.v1 |  

### End-to-End ASR (speaker-independent model)

- Dataset: Librispeech [8]
- Language: English
- Total duration: 約980 時間
- Trainin data： 約960 時間 (train_clean_100, train_clean_360, train_other_500)
- Validation data: 約10 時間 (dev_clean, dev_other)
- Test data: 約10 時間 (test_clean, test_other)

| モデル | 概要 |  
| --- | --- |  
| Transformer | Word error rate (WER), test_clean:2.6, test_other:5.7 |  

## 客観評価結果

## End-to-End音声認識に基づく単語誤り率

| Method | Waveform synthesis | S [\%] | D [\%] | I [\%] | CER [\%] |  
| --- | --- | --- | --- | --- | --- |  
| Ground truth |  | 0.3 | 0.7 | 0.3 | 1.3 |  
| Tacotron2.v2 | Griffin-Lim algorithm | 0.4 | 0.9 | 0.7 | 2.0 |  
| Tacotron2.v3 | Griffin-Lim algorithm | 0.5 | 0.9 | 0.4 | 1.8 |  
| Transformer.v1 | Griffin-Lim algorithm | 0.6 | 1.5 | 0.5 | 2.7 |  
| FastSpeech.v2 | Griffin-Lim algorithm | 0.4 | 0.9 | 0.3 | 1.6 |  
| Tacotron2.v2 | WaveNet vocoder | 0.4 | 1.0 | 3.6 | 5.0 |  
| Tacotron2.v3 | WaveNet vocoder | 0.5 | 1.2 | 0.3 | 2.1 |  
| Transformer.v1 | WaveNet vocoder | 0.6 | 1.7 | 0.5 | 2.8 |  
| FastSpeech.v2 | WaveNet vocoder | 0.4 | 1.1 | 0.4 | 1.8 |  

## サンプル

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0063.wav" controls></audio> |  
| Tacotron2.v2 | Griffin-Lim algorithm | <audio src="wav/taco2.v2.GL/LJ050-0063.wav" controls></audio> |  
| Tacotron2.v2 | WaveNet vocoder | <audio src="wav/taco2.v2.WNVmol/LJ050-0063_gen.wav" controls></audio> |  
| Tacotron2.v3 | Griffin-Lim algorithm | <audio src="wav/taco2.v3.GL/LJ050-0063.wav" controls></audio> |  
| Tacotron2.v3 | WaveNet vocoder | <audio src="wav/taco2.v3.WNVmol/LJ050-0063_gen.wav" controls></audio> |  

    Ground truth
    id: (lj050_0063)
    Scores: (#C #S #D #I) 95 0 3 0
    REF:  A N D w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    HYP:  * * * w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    Eval: D D D                                                                                                                                                                                               

    Tacotron2.v2 with Griffin-Lim algorithm
    id: (lj050_0063)
    Scores: (#C #S #D #I) 98 0 0 96
    REF:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * d * * * * * * d * * * * 
    HYP:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n D T O T H E D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O T H E D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O d E I T Y T O d E I T Y 
    Eval:                                                                                                                                                                                                 I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I   I I I I I I   I I I I 
      
    Tacotron2.v2 with WaveNet vocoder
    id: (lj050_0063)
    Scores: (#C #S #D #I) 98 0 0 721
    REF:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
    HYP:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n D T O T H E D E I T Y T O D E I T Y T O D E I T Y T O T H E D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T 
    Eval:                                                                                                                                                                                                 I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I 

    Tacotron2.v3 with Griffin-Lim algorithm
    id: (lj050_0063)
    Scores: (#C #S #D #I) 98 0 0 0
    REF:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    HYP:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    Eval:                                                                                                                                                                                                     
      
    Tacotron2.v3 with WaveNet vocoder
    id: (lj050_0063)
    Scores: (#C #S #D #I) 95 0 3 0
    REF:  A N D w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    HYP:  * * * w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    Eval: D D D                                                                                                                                                                                               


## 参考文献

- [1] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, Ł. Kaiser, and I. Polosukhin, “Attention is allyou need,”  in Advances in neural information processing sys-tems, 2017, pp. 5998–6008.
- [2] D. Snyder, D. Garcia-Romero, G. Sell, D. Povey, and S. Khu-danpur, “X-vectors: Robust DNN embeddings for speaker recognition,” in Proc. of ICASSP, 2018, pp. 5329–5333.
