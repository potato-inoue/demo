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
| Tacotron2.v3 | Tacotron2 (RNN)，Location sensitive attention [4], Guided attention loss [5] |  
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

| Method | Waveform synthesis | S [%] | D [%] | I [%] | CER [%] |  
| --- | --- | --- | --- | --- | --- |  
| Ground truth |  | 0.3 | 0.7 | 0.3 | 1.3 |  
| Tacotron2.v2 | Griffin-Lim algorithm | **0.4** | **0.9** | 0.7 | 2.0 |  
| Tacotron2.v3 | Griffin-Lim algorithm | 0.5 | **0.9** | 0.4 | 1.8 |  
| Transformer.v1 | Griffin-Lim algorithm | 0.6 | 1.5 | 0.5 | 2.7 |  
| FastSpeech.v2 | Griffin-Lim algorithm | **0.4** | **0.9** | **0.3** | **1.6** |  
| Tacotron2.v2 | WaveNet vocoder | **0.4** | **1.0** | 3.6 | 5.0 |  
| Tacotron2.v3 | WaveNet vocoder | 0.5 | 1.2 | **0.3** | 2.1 |  
| Transformer.v1 | WaveNet vocoder | 0.6 | 1.7 | 0.5 | 2.8 |  
| FastSpeech.v2 | WaveNet vocoder | **0.4** | 1.1 | 0.4 | **1.8** |  

## 単語の繰り返しのサンプル1 (Griffin-Lim)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0063.wav" controls></audio> |  
| Tacotron2.v2 | Griffin-Lim algorithm | <audio src="wav/taco2.v2.GL/LJ050-0063.wav" controls></audio> |  
| Tacotron2.v3 | Griffin-Lim algorithm | <audio src="wav/taco2.v3.GL/LJ050-0063.wav" controls></audio> |  

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
      
    Tacotron2.v3 with Griffin-Lim algorithm
    id: (lj050_0063)
    Scores: (#C #S #D #I) 98 0 0 0
    REF:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    HYP:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    Eval:                                                                                                                                                                                                     

## 単語の繰り返しのサンプル1 (WaveNet)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0063.wav" controls></audio> |  
| Tacotron2.v2 | WaveNet vocoder | <audio src="wav/taco2.v2.WNVmol/LJ050-0063_gen.wav" controls></audio> |  
| Tacotron2.v3 | WaveNet vocoder | <audio src="wav/taco2.v3.WNVmol/LJ050-0063_gen.wav" controls></audio> |  

    Ground truth
    id: (lj050_0063)
    Scores: (#C #S #D #I) 95 0 3 0
    REF:  A N D w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    HYP:  * * * w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    Eval: D D D                                                                                                                                                                                               
      
    Tacotron2.v2 with WaveNet vocoder
    id: (lj050_0063)
    Scores: (#C #S #D #I) 98 0 0 721
    REF:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
    HYP:  a n d w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n D T O T H E D E I T Y T O D E I T Y T O D E I T Y T O T H E D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T O D E I T Y T 
    Eval:                                                                                                                                                                                                 I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I I 
      
    Tacotron2.v3 with WaveNet vocoder
    id: (lj050_0063)
    Scores: (#C #S #D #I) 95 0 3 0
    REF:  A N D w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    HYP:  * * * w h o h a v e b e e n i n v o l v e d i n b o m b i n g o r b o m b m a k i n g o r w h o s e p a s t c o n d u c t i n d i c a t e s t e n d e n c i e s t o w a r d v i o l e n c e a n d d 
    Eval: D D D                                                                                                                                                                                               

## 単語の繰り返しのサンプル2 (Griffin-Lim)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0132.wav" controls></audio> |  
| Transformer.v1 | Griffin-Lim algorithm | <audio src="wav/transformer.v1.GL/LJ050-0132.wav" controls></audio> |  
| Tacotron2.v2 | Griffin-Lim algorithm | <audio src="wav/taco2.v2.GL/LJ050-0132.wav" controls></audio> |  

    Ground truth
    id: (lj050_0132)
    Scores: (#C #S #D #I) 116 0 0 0
    REF:  t h e c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l i a i s o n a r r a n g e m e n t s 
    HYP:  t h e c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l i a i s o n a r r a n g e m e n t s 
    Eval:                                                                                                                                                                                                                                         
      
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0132)
    Scores: (#C #S #D #I) 108 3 5 11
    REF:  T H E c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e * * n * * * * * * * * * a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t S l I a I s O n a r r a n g e m e n t S 
    HYP:  * * * c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e N A n D P R O P O S E D a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t A l Y a * s A n a r r a n g e m e n t * 
    Eval: D D D                                                                                                         I I   I I I I I I I I I                                                                                 S   S   D   S                         D 
      
    Tacotron2.v2 with Griffin-Lim algorithm
    id: (lj050_0132)
    Scores: (#C #S #D #I) 116 0 0 0
    REF:  t h e c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l i a i s o n a r r a n g e m e n t s 
    HYP:  t h e c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l i a i s o n a r r a n g e m e n t s 
    Eval:                                                                                                                                                                                                                                         

## 単語の繰り返しのサンプル2 (WaveNet)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0132.wav" controls></audio> |  
| Transformer.v1 | WaveNet vocoder | <audio src="wav/transformer.v1.WNVmol/LJ050-0132.wav" controls></audio> |  
| Tacotron2.v2 | WaveNet vocoder | <audio src="wav/taco2.v2.WNVmol/LJ050-0132.wav" controls></audio> |  

    Ground truth
    id: (lj050_0132)
    Scores: (#C #S #D #I) 116 0 0 0
    REF:  t h e c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l i a i s o n a r r a n g e m e n t s 
    HYP:  t h e c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l i a i s o n a r r a n g e m e n t s 
    Eval:                                                                                                                                                                                                                                         
      
    Transformer.v1 with WaveNet vocoder
    id: (lj050_0132)
    Scores: (#C #S #D #I) 108 3 5 11
    REF:  T H E c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e * * n * * * * * * * * * a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t S l I a I s O n a r r a n g e m e n t S 
    HYP:  * * * c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e N A n D P R O P O S E D a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t A l Y a * s A n a r r a n g e m e n t * 
    Eval: D D D                                                                                                         I I   I I I I I I I I I                                                                                 S   S   D   S                         D 
      
    Tacotron2.v2 with WaveNet vocoder
    id: (lj050_0132)
    Scores: (#C #S #D #I) 111 2 3 1
    REF:  T H E c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l I a I s o * n a r r a n g e m e n t s 
    HYP:  * * * c o m m i s s i o n n o t e s w i t h a p p r o v a l s e v e r a l r e c e n t m e a s u r e s t a k e n a n d p r o p o s e d b y t h e s e c r e t s e r v i c e t o i m p r o v e i t s l E a ' s o W n a r r a n g e m e n t s 
    Eval: D D D                                                                                                                                                                                               S   S     I                           

## 単語の未発話のサンプル1 (Griffin-Lim)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0176.wav" controls></audio> |  
| Transformer.v1 | Griffin-Lim algorithm | <audio src="wav/transformer.v1.GL/LJ050-0176.wav" controls></audio> |  
| Tacotron2.v2 | Griffin-Lim algorithm | <audio src="wav/taco2.v2.GL/LJ050-0176.wav" controls></audio> |  

    Ground truth
    id: (lj050_0176)
    Scores: (#C #S #D #I) 122 0 0 0
    REF:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    HYP:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    Eval:                                                                                                                                                                                                                                                     
      
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0176)
    Scores: (#C #S #D #I) 100 0 22 0
    REF:  t o e s t a b l i s h l i a i s o n w i t h l o c a L I N T E L l I G E N C E G A T H E R I N G a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t E e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    HYP:  t o e s t a b l i s h l i a i s o n w i t h l o c a * * * * * * l * * * * * * * * * * * * * * * a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t * e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    Eval:                                                     D D D D D D   D D D D D D D D D D D D D D D                                                                     D                                                                               
    　　
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0176)
    Scores: (#C #S #D #I) 122 0 0 0
    REF:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    HYP:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    Eval:                                                                                                                                                                                                                                                     

## 単語の未発話のサンプル1 (WaveNet)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0176.wav" controls></audio> |  
| Transformer.v1 | WaveNet vocoder | <audio src="wav/transformer.v1.WNVmol/LJ050-0176.wav" controls></audio> |  
| Tacotron2.v2 | WaveNet vocoder | <audio src="wav/taco2.v2.WNVmol/LJ050-0176.wav" controls></audio> |  

    Ground truth
    id: (lj050_0176)
    Scores: (#C #S #D #I) 122 0 0 0
    REF:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    HYP:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    Eval:                                                                                                                                                                                                                                                     
      
    Transformer.v1 with WaveNet vocoder
    id: (lj050_0176)
    Scores: (#C #S #D #I) 100 0 22 0
    REF:  t o e s t a b l i s h l i a i s o n w i t h l o c a L I N T E L l I G E N C E G A T H E R I N G a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t E e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    HYP:  t o e s t a b l i s h l i a i s o n w i t h l o c a * * * * * * l * * * * * * * * * * * * * * * a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t * e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    Eval:                                                     D D D D D D   D D D D D D D D D D D D D D D                                                                     D                                                                               
    　　
    Tacotron2.v2 with WaveNet vocoder
    id: (lj050_0176)
    Scores: (#C #S #D #I) 122 0 0 0
    REF:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    HYP:  t o e s t a b l i s h l i a i s o n w i t h l o c a l i n t e l l i g e n c e g a t h e r i n g a g e n c i e s a n d t o p r o v i d e f o r t h e i m m e d i a t e e v a l u a t i o n o f i n f o r m a t i o n r e c e i v e d f r o m t h e m 
    Eval:                                                                                                                                                                                                                                                     

## 単語の未発話のサンプル2 (Griffin-Lim)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0267.wav" controls></audio> |  
| Transformer.v1 | Griffin-Lim algorithm | <audio src="wav/transformer.v1.GL/LJ050-0267.wav" controls></audio> |  
| Tacotron2.v2 | Griffin-Lim algorithm | <audio src="wav/taco2.v2.GL/LJ050-0267.wav" controls></audio> |  

    Ground truth
    id: (lj050_0267)
    Scores: (#C #S #D #I) 124 1 0 0
    REF:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f h o r n I g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    HYP:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f h o r n A g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    Eval:                                                                         S                                                                                                                                                                                 
      
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0267)
    Scores: (#C #S #D #I) 110 4 11 8
    REF:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l * * * * d * * * F H o R n i * g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t F O R s C I E N C E A N D t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    HYP:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l D A N D d O N A L D o W n i N g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t * * ' s * * * * * * * * * t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    Eval:                                                             I I I I   I I I S S   S     I                                                               D D S   D D D D D D D D D                                                                                         
      
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0267)
    Scores: (#C #S #D #I) 124 0 1 0
    REF:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f H o r n i g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    HYP:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f * o r n i g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    Eval:                                                                 D                                                                                                                                                                                         

## 単語の未発話のサンプル2 (WaveNet)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0267.wav" controls></audio> |  
| Transformer.v1 | WaveNet vocoder | <audio src="wav/transformer.v1.WNVmol/LJ050-0267.wav" controls></audio> |  
| Tacotron2.v2 | WaveNet vocoder | <audio src="wav/taco2.v2.WNVmol/LJ050-0267.wav" controls></audio> |  

    Ground truth
    id: (lj050_0267)
    Scores: (#C #S #D #I) 124 1 0 0
    REF:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f h o r n I g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    HYP:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f h o r n A g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    Eval:                                                                         S                                                                                                                                                                                 
      
    Transformer.v1 with WaveNet vocoder
    id: (lj050_0267)
    Scores: (#C #S #D #I) 109 3 13 8
    REF:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l * * * * d * * * F H o R n i * g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t F O R S C I E N C E A N D t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    HYP:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l D A N D d O N A L D o W n i N g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t * * * * * * * * * * * * * t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    Eval:                                                             I I I I   I I I S S   S     I                                                               D D D D D D D D D D D D D                                                                                         
      
    Tacotron2.v2 with WaveNet vocoder
    id: (lj050_0267)
    Scores: (#C #S #D #I) 124 0 1 0
    REF:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f H o r n i g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    HYP:  b e t w e e n s e c r e t a r y d i l l o n a n d d o n a l d f * o r n i g s p e c i a l a s s i s t a n t t o t h e p r e s i d e n t f o r s c i e n c e a n d t e c h n o l o g y i s a u s e f u l e f f o r t i n t h e r i g h t d i r e c t i o n 
    Eval:                                                                 D                                                                                                                                                                                         

## 単語の未発話のサンプル2 (Griffin-Lim)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0272.wav" controls></audio> |  
| Transformer.v1 | Griffin-Lim algorithm | <audio src="wav/transformer.v1.GL/LJ050-0272.wav" controls></audio> |  
| Tacotron2.v2 | Griffin-Lim algorithm | <audio src="wav/taco2.v2.GL/LJ050-0272.wav" controls></audio> |  

    Ground truth
    id: (lj050_0272)
    Scores: (#C #S #D #I) 92 0 0 0
    REF:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    HYP:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    Eval:                                                                                                                                                                                         
      
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0272)
    Scores: (#C #S #D #I) 86 0 6 0
    REF:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r E S O D E e P s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    HYP:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r * * * * * e * s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    Eval:                                                                                                       D D D D D   D                                                                     
      
    Transformer.v1 with Griffin-Lim algorithm
    id: (lj050_0272)
    Scores: (#C #S #D #I) 92 0 0 0
    REF:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    HYP:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    Eval:                                                                                                                                                                                         

## 単語の未発話のサンプル3 (WaveNet)

| Model | Waveform synthesis | Speech |  
| --- | --- | --- |  
| Ground truth |  | <audio src="wav/ground-truth/LJ050-0272.wav" controls></audio> |  
| Transformer.v1 | WaveNet vocoder | <audio src="wav/transformer.v1.WNVmol/LJ050-0272.wav" controls></audio> |  
| Tacotron2.v2 | WaveNet vocoder | <audio src="wav/taco2.v2.WNVmol/LJ050-0272.wav" controls></audio> |  

    Ground truth
    id: (lj050_0272)
    Scores: (#C #S #D #I) 92 0 0 0
    REF:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    HYP:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    Eval:                                                                                                                                                                                         
      
    Transformer.v1 with WaveNet vocoder
    id: (lj050_0272)
    Scores: (#C #S #D #I) 86 0 6 0
    REF:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r E S O D E e P s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    HYP:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r * * * * * e * s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    Eval:                                                                                                       D D D D D   D                                                                     
      
        Tacotron2.v2 with WaveNet vocoder
    id: (lj050_0272)
    Scores: (#C #S #D #I) 92 0 0 0
    REF:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    HYP:  a n d t h e t r a d i t i o n s o f t h e o f f i c e i n a d e m o c r a c y s u c h a s o u r s a r e s o d e e p s e a t e d a s t o p r e c l u d e a b s o l u t e s e c u r i t y 
    Eval:                                                                                                                                                                                         


## 参考文献

- [1] K. Ito, “The LJ speech dataset,” https://keithito.com/LJ-Speech-Dataset/, 2017.
- [2] J. Shen, R. Pang, R. J. Weiss, M. Schuster, N. Jaitly, Z. Yang, Z. Chen, Y. Zhang, Y. Wang, R. Skerrv-Ryan, et al., “Natural TTS synthesis by conditioning WaveNet on Mel spectrogram predictions,” in Proc. of ICASSP, 2018, pp. 4779–4783.
- [3] J.-X. Zhang, Z.-H. Ling, and L.-R. Dai, “Forward attention in sequence-to-sequence acoustic modeling for speech synthesis,” in ICASSP, 2018, pp. 4789–4793.
- [4] J. K. Chorowski, D. Bahdanau, D. Serdyuk, et al., “Attention-based models for speech recognition,” in NIPS, 2015, pp. 577–585.
- [5] H. Tachibana, K. Uenoyama, and S. Aihara, “Efficiently trainable text-to-speech system based on deep convolutional networks with guided attention,” in ICASSP, 2018, pp. 4784–4788.
- [6] N. Li, S. Liu, Y. Liu, S. Zhao, M. Liu, and M. Zhou, “Close to human quality TTS with Transformer,” arXiv preprint arXiv:1809.08895, 2018.
- [7] Y. Ren, Y. Ruan, X. Tan, T. Qin, S. Zhao, Z. Zhao, and T. Liu, “FastSpeech: fast, robust and controllable text to speech,” arXiv preprint arXiv:1905.09263, 2019.
- [8] V. Panayotov, G. Chen, D. Povey, and S. Khudanpur, “Librispeech: an ASR corpus based on public domain audio books,” in Proc. of ICASSP, 2015, pp. 5206–5210.