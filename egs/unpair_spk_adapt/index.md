# Demo of speech sample

- Semi-supervised speaker adaptation for end-to-end speech synthesis with pretrained models
- Katsuki Inoue, Sunao Hara, Masanobu Abe, Tomoki Hayashi, Ryuichi Yamamoto, Shinji Watanabe

## Abstract 

Recently, end-to-end text-to-speech (TTS) models have achieved a remarkable performance, however, requiring a large amount of paired text and speech data for training.
On the other hand, we can easily collect unpaired dozen minutes of speech recordings for a target speaker without corresponding text data.
To make use of such accessible data, the proposed method leverages the recent great success of state-of-the-art end-to-end automatic speech recognition (ASR) systems and obtains corresponding transcriptions from pretrained ASR models.
Although these models could only provide text output instead of intermediate linguistic features like phonemes, end-to-end TTS can be well trained with such raw text data directly.
Thus, **the proposed method can greatly simplify a speaker adaptation pipeline by consistently employing end-to-end ASR/TTS ecosystems.**
The experimental results show that our proposed method achieved comparable performance to a paired data adaptation method in terms of subjective speaker similarity and objective cepstral distance measures.

## Model

All TTS models have Transformer [1] architecture.

- PT : the pretrained model
- **PROPOSED : the adapted model based on fine-tuning with unpaired speech data**
- AD-FT-P : the adapted model based on fine-tuning with paired data (speech, texts)
- AD-FT-p : the adapted model based on fine-tuning with half size of paired data (speech, texts)
- AD-EM : the adapted model based on feature embedding (x-vector)

## Sample

DMOS results of speaker similarity  
<img src="img/DMOS_spk_similar.png" width="320px"> 

### FemaleA  

| Model | Speech |  
| --- | --- |  
| Target speaker (ground-truth) | <audio src="wav/ground-truth/237_134500_000036_000000.wav" controls></audio> |  
| PT | <audio src="wav/pretrained/237_134500_000036_000000.wav" controls></audio> |  
| PROPOSED | <audio src="wav/adapt-ft-unpair/237_134500_000036_000000.wav" controls></audio> |  
| AD-FT-P | <audio src="wav/adapt-ft-pair/237_134500_000036_000000.wav" controls></audio> |  
| AD-FT-p | <audio src="wav/adapt-ft-pair-half/237_134500_000036_000000.wav" controls></audio> |  
| AD-EM | <audio src="wav/adapt-ft-em/237_134500_000036_000000.wav" controls></audio> |  
