
[//]: # (# 语音深度伪造检测研究进展 Research progress on audio deepfake detection)
[//]: # (***)

>This repository contains a list of audio deepfake resources. We also have a survey report on Audio Deepfake Detection (ADD). We include sections on ADD Datasets, Audio Preprocessing, Feature Extraction and Network Training to introduce beginners to carefully selected material to learn the ADD domain. We will endeavour to maintain this repository on an ongoing basis for a fixed period.

# Table of contents
- [Audio Large Model](#SpeechLargeModel)
- [Datasets](#Datasets)
- [Audio Preprocessing](#audiopreprocessing)
  - [Commonly Used Noise Datasets](#noise1)
  - [Audio Enhancement Methods](#ae)
- [Feature Extraction](#featureextraction)
  - [Handcrafted Feature-based Forgery Detection](#hf1)
  - [Hybrid Feature-based Forgery Detection](#hf2)
  - [End-to-End Forgery Detection](#ete)
  - [Feature-level Fusion Forgery Detection](#ff)
- [Network Training](#nt)
  - [Multi-task Learning-based Forgery Detection](#ml)
- [Reference](#Reference)
- [Statement](#Statement)
- [Contact](#Contact)

# <span id="SpeechLargeModel">Audio Large Model</span>
|  Model 	 |   Publisher  | Years| Achievable Tasks    |
|:----:|:-------------:|:--------------:|:--------------------|
| AudioLM  <br>  [Paper](https://arxiv.org/pdf/2209.03143) [Website](https://google-research.github.io/seanet/audiolm/examples/) [Code](https://github.com/lucidrains/audiolm-pytorch) |  Google | 2022.09 |1. AudioLM maps the input audio to a sequence of discrete tokens and casts audio generation as a language modeling task in this representation space. <br> 2. Speech continuation, Acoustic generation, Unconditional generation, Generation without semantic tokens, and Piano continuation. |
| VALL-E  <br>  [Paper](https://arxiv.org/abs/2301.02111) [Website](https://www.microsoft.com/en-us/research/project/vall-e-x/)	 |   Microsoft | 2023.01|1. Simply record a 3-second registration of an unseen speaker to create a high-quality personalised speech.  <br> 2. VALL-E X: Cross-lingual speech synthesis. |
|   USM  <br>  [Website](https://sites.research.google/usm/)  |     Google  | 2023.03| 1. ASR beyond 100 languages.<br> 2. Downstream ASR tasks. <br> 3. Automated Speech Translation (AST).    |
|  SpeechGPT <br>  [Website](https://github.com/0nutation/SpeechGPT) 	   | Fudan University |2023.05| 1. Perceive and generate multi-modal contents. <br> 2. Spoken dialogue LLM with strong human instruction.     |
|  Pengi <br>  [Paper](https://arxiv.org/pdf/2305.11834.pdf) [Website](https://github.com/microsoft/Pengi)  | Microsoft |2023.05| 1. an Audio Language Model that leverages Transfer Learning by framing all audio tasks as text-generation tasks. <br> 2. The unified architecture of Pengi enables open-ended tasks and close-ended tasks without any additional fine-tuning or task-specific extensions.     |
|  VoiceBox   <br>  [Website](https://voicebox.metademolab.com/)  | Meta  | 2023.06| 1. Synthesize speech across six languages.<br> 2. Remove transient noise.<br> 3. Edit content.<br> 4. Transfer audio style within and across languages.<br>5. Generate diverse speech samples. 	 |
|  AudioPaLM <br>  [Paper](https://arxiv.org/pdf/2306.12925) [Website](https://google-research.github.io/seanet/audiopalm/examples)	    | Google | 2023.06|1. Speech-to-speech translation. <br> 2. Automatic Speech Recognition (ASR).  |

# <span id="Datasets">Datasets</span>
|  Attack Types  | Years| Dataset   |  Number of Audio  <br>（Subdataset：Real/Fake） 	  |    Language   |
|:-----------:|:------------:|:------------:|:-------------:|:------------:|
|   TTS | 2021 | WaveFake    <br>  [Paper](https://arxiv.org/abs/2111.02813) [Dataset](https://zenodo.org/record/5642694)  	 |       16283/117985  |  English, Japanese   |
| TTS 	 |   2021 | HAD 	    <br>   [Paper](https://arxiv.org/abs/2104.03617)          |                         53612/107224 	                          |         Chinese 	         |
|   TTS  |   2022 |      ADD 2022 	<br>   [Paper](https://arxiv.org/pdf/2202.08433v2.pdf) 	      |   LF: 5619/46067  <br>PF: 5319/46419  <br>FG-D: 5319/46206 	    |         Chinese 	         |
|   TTS 	 |  2022 |       CMFD   <br>    [Paper](https://ieeexplore.ieee.org/document/9921343) 	    [Dataset](https://github.com/WuQinfang/CMFD)                                                                 |           Chinese: 1800/1000 <br>English: 1800/1000 	           |    English, Chinese 	     |
|      TTS 	      |   2022 |     In-the-Wild  <br>   [Paper](https://arxiv.org/abs/2203.16263) 	  [Dataset](https://deepfake-demo.aisec.fraunhofer.de/in_the_wild)         |                          19963/11816 	                          |         English 	         |
|      TTS 	      |   2022 |                   FAD      <br>         [Paper](https://arxiv.org/abs/2207.12308#:~:text=FAD%20dataset%20can%20be%20used%20not%20only%20for,remain%20challenging.%20The%20FAD%20dataset%20is%20publicly%20available.) 	 [Dataset](https://zenodo.org/record/6635521#.Ysjq4nZBw2x)        |                         115800/115800 	                         |         Chinese 	         |
|    Replay 	     |  2017 |                    ASVspoof 2017 <br>        [Paper](https://www.asvspoof.org/asvspoof2017overview_cameraReady.pdf) 	     [Dataset](https://datashare.ed.ac.uk/handle/10283/3055) 	              |                          3565/14465 	                           |         English 	         |
|    Replay    |    2019 |   ReMASC  <br>   	  [Paper](https://arxiv.org/abs/1904.03365) 	[Dataset](https://github.com/YuanGongND/ReMASC)           |                          9240/45472 	                           | English, Chinese, Hindi 	 |
|    TTS和VC 	     |    2015 |                         AVspoof  <br> 	                             [Paper](https://ieeexplore.ieee.org/document/7358783) 	    [Dataset](https://zenodo.org/record/4081040)                                                                |             LA: 15504/120480  <br>PA: 15504/14465 	             |         English 	         |
|    TTS和VC 	     |      2015 |                     ASVspoof 2015  <br>            [Paper](https://datashare.ed.ac.uk/bitstream/handle/10283/853/ASVspoof2015_evaluation_plan.pdf?sequence=2&isAllowed=y) 	[Dataset](http://dx.doi.org/10.7488/ds/298) 	                                       |                         16651/246500 	                          |         English 	         |
|    TTS和VC 	     |  2021 |                         FMFCC-A   <br>     [Paper](https://arxiv.org/abs/2110.09441#:~:text=The%20FMFCC-A%20dataset%20is%20by%20far%20the%20largest,10%2C000%20genuine%20Mandarin%20utterances%20collected%20from%2058%20speakers.) 	[Dataset](https://github.com/Amforever/FMFCC-A) 	 |                          10000/40000 	                          |         Chinese 	         |
|    TTS和VC 	     |      2022 |                SceneFake  <br>   [Paper](https://arxiv.org/abs/2211.06073) 	[Dataset](https://zenodo.org/record/7663324#.Y_XKMuPYuUk)                                                                           |                          19838/64642 	                          |         English 	         |
|    TTS和VC   |   2022 |                                             EmoFake    <br>           [Paper](http://arxiv.org/abs/2211.05363) 	                                                                          |                          35000/53200 	                          |    English, Chinese 	     |
|    TTS和VC 	     |    2023 |                  PartialSpoof <br>     [Paper](https://arxiv.org/abs/2104.02518)	 [Dataset](https://zenodo.org/record/4817532#.YLd8Yi2l1hF)                                                                        |                         12483/108978 	                          |         English 	         |
|    TTS和VC 	     |     2023 |                                             ADD 2023  <br>      [Paper](https://arxiv.org/abs/2305.13774)	                                                                          | FG-D: 172819/113042  <br>RL: 55468/65449  <br>AR: 14907/95383 	 |         Chinese 	         |
|    TTS和VC 	     |      2023 |                    DECRO  <br>  	   [Paper](https://dl.acm.org/doi/10.1145/3543507.3583222) 	  [Dataset](https://github.com/petrichorwq/DECRO-dataset)                                                                  |         Chinese: 21218/41880 <br>English: 12484/42799 	         |    English, Chinese 	     |
| TTS、VC和Replay 	 |   2019 |                    ASVspoof 2019 <br>    [Paper](https://arxiv.org/abs/1904.05441)	  [Dataset](https://datashare.ed.ac.uk/handle/10283/3336) 	                                                                          |            LA: 12483/108978  <br>PA: 28890/189540 	             |         English 	         |
| TTS、VC和Replay 	 |  2021 |                      ASVspoof 2021  <br>   [Paper](https://arxiv.org/abs/2109.00535) 	     [Dataset](https://www.asvspoof.org/index2021.html)                                                                    | LA: 18452/163114  <br>PA: 126630/816480  <br>PF: 14869/519059 	 |         English 	         |


# <span id="audiopreprocessing">Audio Preprocessing</span>

## <span id="noise1">Commonly Used Noise Datasets</span>
|                                       Dataset 	                                        |                                                                                                                                     Description 	                                                                                                                                     |
|:--------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                   MUSAN <br>  [Dataset](https://www.openslr.org/17/)                   |       A corpus of music, speech and noise                      |
|                      RIR <br>  [Dataset](https://www.openslr.org/28/)                       |   A database of simulated and real room impulse responses, isotropic and point-source noises. The audio files in this data are all in 16k sampling rate and 16-bit precision.  |
|           NOIZEUS <br> [Dataset](https://ecs.utdallas.edu/loizou/speech/noizeus/)           |       Contains 30 IEEE sentences (generated by three male and three female speakers) corrupted by eight different real-world noises at different SNRs. Noises include suburban train noise, murmur, car, exhibition hall, restaurant, street, airport and train station noise.        |
|               NoiseX-92  <br> [Dataset](http://spib.linse.ufsc.br/noise.html)               |                             All noises are obtained with a duration of 235 seconds, a sampling rate of 19.98 KHz, an analogue-to-digital converter (A/D) with 16 bits, an anti-alias filter and no pre-emphasis stage. Fifteen noise types are included.                              |
|            DEMAND <br> [Dataset](https://zenodo.org/record/1227121#.YXtsyPlBxjU)            |                                                                                                            Multi-channel acoustic noise database for diverse environments.                                                                                                            |
|                ESC-50 <br> [Dataset](https://github.com/karolpiczak/ESC-50)                 | A tagged collection of 2000 environmental audios obtained from clips in Freesound.org, suitable for environmental sound classification. The dataset consists of 5-second-long recordings organised into 5 broad categories, each with 10 subcategories (40 examples per subcategory). |
| ESC <br> [Dataset](http://shujujishi.com/dataset/69b2bf03-d855-4f8b-ab96-1ec80e285863.html) |                                                                                                                       Including the ESC-50, ESC-10, and ESC-US.                                                                                                                       |
|            FSD50K <br> [Dataset](https://zenodo.org/record/4060432#.Y1kvcHZByUk)            |   An open dataset of human tagged sound events containing 51,197 Freesound clips totalling 108.3 hours of multi-labeled audio, unequally distributed across 200 classes from the AudioSet Ontology.                                                                                                          |

## <span id="ae">Audio Enhancement Methods</span>
|                                                                                                                                                                               Method 	                                                                                                                                                                               |                                                                Description 	                                                                 |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------:|
|                                                                                                                           SpecAugment <br> [Paper](https://arxiv.org/pdf/1904.08779.pdf)   [Code](https://github.com/DemisEom/SpecAugment)                                                                                                                           |                               Enhancement strategies include time warping, frequency masking and time masking                                |  
|                                                                                                                     WavAugment <br> [Paper](https://arxiv.org/abs/2007.00991)  [Code](https://github.com/facebookresearch/WavAugment)                                                                                                                     | Enhancement strategies include pitch randomization, reverberation, additive noise, time dropout (temporal masking), band reject and clipping | 
|                                                              RawBoost  <br> [Paper](https://arxiv.org/abs/2007.00991)      [Code](https://github.com/TakHemlata/RawBoost-antispoofing)                                                               | Enhancement strategies include linear and non-linear convolutive noise, impulsive signal-dependent additive noise and stationary signal-independent additive noise |    

# <span id="featureextraction">Feature Extraction</span>

## <span id="hf1">Handcrafted Feature-based Forgery Detection</span>
<table>
	<tr>
	    <td align="center" rowspan="2">Paper</td>
	    <td align="center" colspan="4" >Audio Deepfake Detection</td>
	    <td align="center" colspan="2">Results</td>  
	</tr >
	<tr >
        <td align="center">Data Augmentation</td>
        <td align="center">Feature Extraction</td>
        <td align="center">Network Framework</td>
        <td align="center">Loss Function</td>
        <td align="center">EER (%)</td>
        <td align="center">t-DCF</td>
	</tr>
	<tr>
	    <td align="center">Detecting spoofing attacks using VGG and SincNet: BUT-Omilia submission to ASVspoof 2019 challenge <br> <a href="https://arxiv.org/abs/1907.12908">Paper</a>  <a href="https://github.com/mravanelli/SincNet">Code</a></td>
	    <td align="center">—</td>
        <td align="center">CQT, Power Spectrum</td>
        <td align="center">VGG, SincNet</td>
        <td align="center">CE</td>
        <td align="center">LA: 8.01 (4)<br>PA: 1.51 (2)</td>
        <td align="center">LA: 0.208 (4)<br><b>PA: 0.037 (1)</b></td>
	</tr>
    <tr>
        <td align="center">Long-term high frequency features for synthetic speech detection <br> <a href="https://www.sciencedirect.com/science/article/pii/S1051200419301769#:~:text=The%20long-term%20information%20has%20been%20found%20to%20be,from%20the%20long-term%20constant-Q%20transform%20%28CQT%29%20based%20features.">Paper</a></td>
        <td align="center">Cafe, White and Street Noise</td>
        <td align="center">ICQC, ICQCC, ICBC, ICLBC</td>
        <td align="center">DNN</td>
        <td align="center">CE</td>
        <td align="center">LA: 7.78 (3)</td>
        <td align="center">LA: 0.187 (3)</td>
    </tr>
    <tr>
        <td align="center">Voice spoofing countermeasure for logical access attacks detection <br> <a href="https://ieeexplore.ieee.org/document/9638512">Paper</a></td>
        <td align="center">—</td>
        <td align="center">ELTP-LFCC</td>
        <td align="center">DBiLSTM</td>
        <td align="center">—</td>
        <td align="center"><b>LA: 0.74 (1)</b></td>
        <td align="center"><b>LA: 0.008 (1)</b></td>
    </tr>
    <tr>
        <td align="center">Voice spoofing detector: A unified anti-spoofing framework <br> <a href="https://www.sciencedirect.com/science/article/pii/S0957417422002330">Paper</a></td> 
        <td align="center">—</td>
        <td align="center">ATP-GTCC</td>
        <td align="center">SVM</td>
        <td align="center">Hamming <br> Distance</td>
        <td align="center">LA: 0.75 (2)<br><b>PA: 1.00 (1)</b></td>
        <td align="center">LA: 0.050 (2)<br>PA: 0.064 (2)</td>
    </tr>
</table>
Note: "—" indicates not mentioned in the paper. Values in brackets in the experimental results are the ranking of each column in the LA or PA scenario, and bolded values are the best results for that scenario.

## <span id="hf2">Hybrid Feature-based Forgery Detection</span>
<table>
	<tr>
	    <td align="center" rowspan="2">Paper</td>
	    <td align="center" colspan="4" >Audio Deepfake Detection</td>
	    <td align="center" colspan="2">Results</td>  
	</tr >
    <tr>
        <td align="center">Data Augmentation</td>
        <td align="center">Feature Extraction</td>
        <td align="center">Network Structure</td>
        <td align="center">Loss Function</td>
        <td align="center">EER (%)</td>
        <td align="center">t-DCF</td>
    </tr>
    <tr>
        <td align="center">Light convolutional neural network with feature genuinization for detection of synthetic speech attacks <br> <a href="https://arxiv.org/pdf/2009.09637.pdf">Paper</a></td>
        <td align="center">—</td>
        <td align="center">CQT-based LPS</td>
        <td align="center">LCNN</td>
        <td align="center">—</td>
        <td align="center">LA: 4.07 (11)</td>
        <td align="center">LA: 0.102 (10)</td>
    </tr>
    <tr>
        <td align="center">Siamese convolutional neural network using gaussian probability feature for spoofing speech detection <br> <a href="http://www.interspeech2020.org/uploadfile/pdf/Mon-3-2-9.pdf">Paper</a></td>
        <td align="center">—</td>
        <td align="center">LFCC</td>
        <td align="center">Siamese CNN</td>
        <td align="center">CE</td>
        <td align="center">LA: 3.79 (10)<br>PA: 7.98 (5)</td>
        <td align="center">LA: 0.093 (5)<br>PA: 0.195 (2)</td>
    </tr>
    <tr>
        <td align="center">Generalization of audio deepfake detection <br> <a href="https://www.researchgate.net/profile/Avrosh-Kumar/publication/345141913_Generalization_of_Audio_Deepfake_Detection/links/600cb38945851553a0678e07/Generalization-of-Audio-Deepfake-Detection.pdf">Paper</a></td>
        <td align="center">RIR and MUSAN</td>
        <td align="center">LFB</td>
        <td align="center">ResNet18</td>
        <td align="center">LCML</td>
        <td align="center">LA: 1.81 (4)</td>
        <td align="center">LA: 0.052 (4)</td>
    </tr>
    <tr>
        <td align="center">Continual learning for fake audio detection <br> <a href="https://arxiv.org/abs/2104.07286">Paper</a></td>
        <td align="center">—</td>
        <td align="center">LFCC</td>
        <td align="center">LCNN, DFWF</td>
        <td align="center">Similarity Loss</td>
        <td align="center">LA: 7.74 (15)<br>PA: 8.85 (6)</td>
        <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">Partially-connected differentiable architecture search for deepfake and spoofing detection <br> <a href="https://arxiv.org/abs/2104.03123v1">Paper</a> <a href="https://github.com/eurecom-asp/pc-darts-anti-spoofing">Code</a></td>
        <td align="center">Frequency Mask</td>
        <td align="center">LFCC</td>
        <td align="center">PC-DARTS</td>
        <td align="center">WCE</td>
        <td align="center">LA: 4.96 (12)</td>
        <td align="center">LA: 0.091 (8)</td>
    </tr>
    <tr>
        <td align="center">One-class learning towards synthetic voice spoofing detection <br> <a href="https://ieeexplore.ieee.org/abstract/document/9417604">Paper</a> <a href="https://github.com/yzyouzhang/AIR-ASVspoof">Code</a></td>
        <td align="center">—</td>
        <td align="center">LFCC</td>
        <td align="center">ResNet18</td>
        <td align="center">OC-Softmax</td>
        <td align="center">LA: 2.19 (7)</td>
        <td align="center">LA: 0.059 (5)</td>
    </tr>
    <tr>
        <td align="center">Replay and synthetic speech detection with res2net architecture <br> <a href="https://ieeexplore.ieee.org/abstract/document/9413828">Paper</a> <a href="https://github.com/lixucuhk/ASV-anti-spoofing-with-Res2Net">Code</a></td>
        <td align="center">—</td>
        <td align="center">CQT</td>
        <td align="center">SE-Res2Net50</td>
        <td align="center">BCE</td>
        <td align="center">LA: 2.50 (8)<br>PA: 0.46 (2)</td>
        <td align="center">LA: 0.074 (7)<br>PA: 0.012 (2)</td>
    </tr>
    <tr>
        <td align="center">An empirical study on channel effects for synthetic voice spoofing countermeasure systems <br> <a href="https://arxiv.org/abs/2104.01320">Paper</a> <a href="https://github.com/yzyouzhang/Empirical-Channel-CM">Code</a></td>
          <td align="center">Telephone Codecs, and Device/Room Impulse Responses (IRs).</td>
        <td align="center">LFCC</td>
        <td align="center">LCNN, ResNet-OC</td>
        <td align="center">OC-Softmax, CE</td>
        <td align="center">LA: 3.92 (10)</td>
        <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">Efficient attention branch network with combined loss function for automatic speaker verification spoof detection <br> <a href="https://link.springer.com/article/10.1007/s00034-023-02314-5">Paper</a> <a href="https://github.com/AmirmohammadRostami/ASV-anti-spoofingwith-EABN">Code</a></td>
        <td align="center">SpecAug, Attention Mask</td>
        <td align="center">LFCC</td>
        <td align="center">EfficientNet-A0, SE-Res2Net50</td>
        <td align="center">WCE, Triplet Loss</td>
        <td align="center">LA: 1.89 (6)<br>PA: 0.86 (4)</td>
        <td align="center">LA: 0.507 (11)<br>PA: 0.024 (4)</td>
    </tr>
    <tr>
        <td align="center">Resmax: Detecting voice spoofing attacks with residual network and max feature map <br> <a href="https://ieeexplore.ieee.org/document/9412165">Paper</a></td>
        <td align="center">—</td>
        <td align="center">CQT</td>
        <td align="center">ResMax</td>
        <td align="center">BCE</td>
        <td align="center">LA: 2.19 (7)<br><b>PA: 0.37 (1)</b></td>
        <td align="center">LA: 0.060 (6)<br><b>PA: 0.009 (1)</b></td>
    </tr>
    <tr>
        <td align="center">Synthetic voice detection and audio splicing detection using se-res2net-conformer architecture <br> <a href="https://ieeexplore.ieee.org/document/10037999">Paper</a></td>
        <td align="center">Adding noise according to a signal-to-noise ratio of 15dB or 25dB</td>
        <td align="center">CQT</td>
        <td align="center">SE-Res2Net34-Confromer</td>
        <td align="center">CE</td>
        <td align="center">LA: 1.85 (5)</td>
        <td align="center">LA: 0.060 (6)</td>
    </tr>
    <tr>
        <td align="center">Fastaudio: A learnable audio front-end for spoof speech detection <br> <a href="https://ieeexplore.ieee.org/document/9746722">Paper</a> <a href="https://github.com/magnumresearchgroup/Fastaudio">Code</a></td>
        <td align="center">—</td>
        <td align="center">L-VQT</td>
        <td align="center">L-DenseNet</td>
        <td align="center">NLLLoss</td>
        <td align="center">LA: 1.54 (3)</td>
        <td align="center">LA: 0.045 (3)</td>
    </tr>
    <tr>
        <td align="center">Learning from yourself: A self-distillation method for fake speech detection <br> <a href="https://arxiv.org/abs/2303.01211">Paper</a></td>
        <td align="center">—</td>
        <td align="center">LPS, F0</td>
        <td align="center">ECANet, SENet</td>
        <td align="center">A-Softmax</td>
        <td align="center">LA: 1.00 (2)<br>PA: 0.65 (3)</td>
        <td align="center">LA: 0.031 (2)<br>PA: 0.017 (3)</td>
    </tr>
    <tr>
        <td align="center">How to boost anti-spoofing with x-vectors <br> <a href="https://ieeexplore.ieee.org/document/10022504">Paper</a></td>
        <td align="center">—</td>
        <td align="center">LFCC, MFCC</td>
        <td align="center">TDNN, SENet34</td>
        <td align="center">LCML</td>
        <td align="center"><b>LA: 0.83 (1)</b></td>
        <td align="center"><b>LA: 0.024 (1)</b></td>
    </tr>
</table>
Note: "—" indicates not mentioned in the paper. Values in brackets in the experimental results are the ranking of each column in the LA or PA scenario, and bolded values are the best results for that scenario.


## <span id="ete">End-to-end Forgery Detection</span>

<table>
	<tr>
	    <td align="center" rowspan="2">Paper</td>
	    <td align="center" colspan="4" >Audio Deepfake Detection</td>
	    <td align="center" colspan="2">Results</td>  
	</tr >
    <tr>
        <td align="center">Data Augmentation</td>
        <td align="center">Feature Extraction</td>
        <td align="center">Network Structure</td>
        <td align="center">Loss Function</td>
        <td align="center">EER (%)</td>
        <td align="center">t-DCF</td>
    </tr>
    <tr>
        <td align="center">A light convolutional GRU-RNN deep feature extractor for asv spoofing detection <br> <a href="https://www.semanticscholar.org/paper/A-Light-Convolutional-GRU-RNN-Deep-Feature-for-ASV-Alan%C3%ADs-Peinado/a692a7c971238a24b2ae882a1b6925946ea5e498">Paper</a></td>
        <td align="center">—</td>
        <td align="center">LC-GRNN</td>
        <td align="center">PLDA</td>
        <td align="center">—</td>
        <td align="center">LA: 6.28 (13) <br> PA: 2.23</td>
        <td align="center">LA: 0.152 (10) <br> PA: 0.061</td>
    </tr>
    <tr>
        <td align="center">Rw-resnet: A novel speech anti-spoofing model using raw waveform <br> <a href="https://arxiv.org/abs/2108.05684v2">Paper</a></td>
        <td align="center">—</td>
        <td align="center">1D Convolution Residual Block</td>
        <td align="center">ResNet</td>
        <td align="center">CE</td>
        <td align="center">LA: 2.98 (11)</td>
        <td align="center">LA: 0.082 (9)</td>
    </tr>
    <tr>
        <td align="center">Raw differentiable architecture search for speech deepfake and spoofing detection <br> <a href="https://arxiv.org/abs/2107.12212">Paper</a> <a href="https://github.com/eurecom-asp/raw-pc-darts-anti-spoofing">Code</a></td>
        <td align="center">Masking Filter</td>
        <td align="center">Sinc Filter</td>
        <td align="center">PC-DARTS</td>
        <td align="center">P2SGrad</td>
        <td align="center">LA: 1.77 (10)</td>
        <td align="center">LA: 0.052 (7)</td>
    </tr>
    <tr>
        <td align="center">Towards end-to-end synthetic speech detection <br> <a href="https://arxiv.org/abs/2106.06341">Paper</a> <a href="https://github.com/ghua-ac/end-to-end-synthetic-speech-detection">Code</a></td>
        <td align="center">—</td>
        <td align="center">DNN</td>
        <td align="center">Res-TSSDNet, Inc-TSSDNet</td>
        <td align="center">WCE</td>
        <td align="center">LA: 1.64 (9)</td>
        <td align="center">LA: 0.048 (6)</td>
    </tr> 
    <tr>
        <td align="center">End-to-end anti-spoofing with RawNet2 <br> <a href="https://ieeexplore.ieee.org/abstract/document/9414234">Paper</a> <a href="https://github.com/eurecom-asp/rawnet2-antispoofing">Code</a></td>
        <td align="center">—</td>
        <td align="center">Sinc Filter</td>
        <td align="center">RawNet2</td>
        <td align="center">CE</td>
        <td align="center">LA: 1.12 (5)</td>
        <td align="center">LA: 0.033 (3)</td>
    </tr>
    <tr>
        <td align="center">Long-term variable Q transform: A novel time-frequency transform algorithm for synthetic speech detection <br> <a href="https://www.sciencedirect.com/science/article/pii/S1051200421002955">Paper</a></td>
        <td align="center">—</td>
        <td align="center">FastAudio filter</td>
        <td align="center">X-vector, ECAPA-TDNN</td>
        <td align="center">—</td>
        <td align="center">LA: 1.54 (7)</td>
        <td align="center">LA: 0.045 (5)</td>
    </tr>
    <tr>
        <td align="center">Fully automated end-to-end fake audio detection <br> <a href="https://arxiv.org/abs/2208.09618">Paper</a></td>
        <td align="center">Sinc Filter</td>
        <td align="center">Wav2Vec2</td>
        <td align="center">light-DARTS</td>
        <td align="center">Comparative loss</td>
        <td align="center">LA: 1.08 (4)</td>
        <td align="center">—</td>
    <tr>
        <td align="center">Audio anti-spoofing using a simple attention module and joint optimization based on additive angular margin loss and meta-learning <br> <a href="https://arxiv.org/abs/2211.09898">Paper</a></td>
        <td align="center">—</td>
        <td align="center">Sinc Filter</td>
        <td align="center">RawNet2, SimAM</td>
        <td align="center">AAM Softmax, MSE</td>
        <td align="center">LA: 0.99 (3)</td>
        <td align="center">LA: 0.029 (2)</td>
    </tr> 
    <tr>
        <td align="center">AASIST: Audio anti-spoofing using integrated spectro-temporal graph attention networks <br> <a href="https://arxiv.org/abs/2110.01200">Paper</a> <a href="https://github.com/clovaai/aasist">Code</a></td>
        <td align="center">—</td>
        <td align="center">Sinc Filter</td>
        <td align="center">RawNet2, MGO, HS-GAL</td>
        <td align="center">CE</td>
        <td align="center">LA: 0.83 (2)</td>
        <td align="center"><b>LA: 0.028 (1)</b></td>
    </tr>
    <tr>
        <td align="center">Ai-synthesized voice detection using neural vocoder artifacts <br> <a href="https://arxiv.org/abs/2304.13085">Paper</a> <a href="https://github.com/csun22/Synthetic-Voice-Detection-Vocoder-Artifacts">Code</a></td>
        <td align="center">Resampling, Noise Addition</td>
        <td align="center">Sinc Filter</td>
        <td align="center">RawNet2</td>
        <td align="center">CE, Softmax</td>
        <td align="center">LA: 4.54 (12)</td>
        <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">To-RawNet: Improving rawnet with tcn and orthogonal regularization for fake audio detection <br> <a href="https://arxiv.org/abs/2305.13701">Paper</a></td>
        <td align="center">RawBoost</td>
        <td align="center">Sinc Filter</td>
        <td align="center">RawNet2, TCN</td>
        <td align="center">CE, Orthogonal Loss</td>
        <td align="center">LA: 1.58 (8)</td>
        <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">Speaker-Aware Anti-spoofing <br> <a href="https://arxiv.org/abs/2303.01126">Paper</a></td> 
        <td align="center">—</td>
        <td align="center">Sinc Filter</td>
        <td align="center">AASIST, M2S Converter</td>
        <td align="center">CE</td>
        <td align="center">LA: 1.13 (6)</td>
        <td align="center">LA: 0.038 (4)</td>
    </tr>
    <tr>
        <td align="center">Spoofing attacker also benefits from self-supervised pretrained model <br> <a href="https://arxiv.org/abs/2305.15518">Paper</a></td>
        <td align="center">—</td>
        <td align="center">HuBERT, WavLM</td>
        <td align="center">Residual block, Conv-TasNet</td>
        <td align="center">AAM softmax</td>
        <td align="center"><b>LA: 0.44 (1)</b></td>
        <td align="center">—</td>
    </tr>
</table>
Note: "—" indicates not mentioned in the paper. Values in brackets in the experimental results are the ranking of each column in the LA scenario, and bolded values are the best results for that scenario.


## <span id="ff">Feature Fusion-based Forgery Detection</span>

<table>
	<tr>
	    <td align="center" rowspan="2">Paper</td>
	    <td align="center" colspan="3" >Audio Deepfake Detection</td>
	    <td align="center" >Results</td>  
	</tr >
    <tr>
        <td align="center">Feature Extraction</td>
        <td align="center">Network Structure</td>
        <td align="center">Loss Function</td>
        <td align="center">EER (%)</td>
    </tr>
    <tr>
        <td align="center">Voice spoofing countermeasure for synthetic speech detection <br> <a href="https://ieeexplore.ieee.org/document/9445238">Paper</a></td>
        <td align="center">GTCC, MFCC, Spectral Flux, Spectral Centroid</td>
        <td align="center">Bi-LSTM</td>
        <td align="center">—</td>
        <td align="center">LA: 3.05 (4)</td>
    </tr>
    <tr>
        <td align="center">Combining automatic speaker verification and prosody analysis for synthetic speech detection <br> <a href="https://arxiv.org/abs/2210.17222">Paper</a></td>
        <td align="center">MFCC, Mel-Spectrogram</td>
        <td align="center">ECAPA-TDNN, Prosody Encoder</td>
        <td align="center">BCE</td>
        <td align="center">LA: 5.39 (5)</td>
    </tr>
    <tr>
        <td align="center">Automatic speaker verification spoofing and deepfake detection using wav2vec 2.0 and data augmentation <br> <a href="https://arxiv.org/abs/2202.12233">Paper</a></td>
        <td align="center">Sinc Filter, Wav2Vec2</td>
        <td align="center">AASIST</td>
        <td align="center">Contrastive Loss, WCE</td>
        <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">Overlapped frequency-distributed network: Frequency-aware voice spoofing countermeasure <br> <a href="https://www.isca-speech.org/archive/pdfs/interspeech_2022/choi22c_interspeech.pdf">Paper</a></td>
        <td align="center">Mel-Spectrogram, CQT</td>
        <td align="center">LCNN, ResNet</td>
        <td align="center">—</td>
        <td align="center">LA: 1.35 (2)<br>PA: 0.35</td>
    </tr>
    <tr>
        <td align="center">Detection of cross-dataset fake audio based on prosodic and pronunciation features <br> <a href="https://arxiv.org/abs/2305.13700">Paper</a></td>
        <td align="center">Phoneme Feature, Prosody Feature, Wav2Vec2</td>
        <td align="center">LCNN, Bi-LSTM</td>
        <td align="center">CTC</td>
        <td align="center">LA: 1.58 (3)</td>
    </tr>
    <tr>
        <td align="center">Betray oneself: A novel audio deepfake detection model via mono-to-stereo conversion <br> <a href="https://arxiv.org/abs/2305.16353">Paper</a> <a href="https://github.com/AI-S2-Lab/M2S-ADD">Code</a></td>
        <td align="center">Sinc Filter</td>
        <td align="center">AASIST, M2S Converter</td>
        <td align="center">CE</td>
        <td align="center"><b>LA: 1.34 (1)</b></td>
    </tr>
</table>
Note: "—" indicates not mentioned in the paper. Values in brackets in the experimental results are the ranking of each column in the LA scenario, and bolded values are the best results for that scenario.

# <span id="nt">Network Training</span>
## <span id="ml">Multi-task Learning-based Forgery Detection</span>

<table>
	<tr>
	    <td align="center" rowspan="2">Paper</td>
	    <td align="center" colspan="3" >Audio Deepfake Detection</td>
	    <td align="center" colspan="2" >Results</td>  
	</tr >
    <tr>
        <td align="center">Feature Extraction</td>
        <td align="center">Network Structure</td>
        <td align="center">Loss Function</td>
        <td align="center">EER (%)</td>
        <td align="center">t-DCF</td>
    </tr>
    <tr>
        <td align="center">Multi-task learning in utterance-level and segmental-level spoof detection <br> <a href="https://arxiv.org/abs/2107.14132">Paper</a></td>
          <td align="center">LFCC</td>
          <td align="center">SELCNN, Bi-LSTM</td>
            <td align="center">P2SGrad</td>
            <td align="center">—</td>
            <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">SA-SASV: An end-to-end spoof-aggregated spoofing-aware speaker verification system <br> <a href="https://arxiv.org/abs/2203.06517">Paper</a> <a href="https://github.com/magnumresearchgroup/SA-SASV">Code</a></td>
          <td align="center">Fbanks, Sinc Filter</td>
          <td align="center">ECAPA-TDNN, ARawNet</td>
            <td align="center">BCE, AAM Softmax, CE</td>
            <td align="center">LA: 4.86 (4)</td>
            <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">STATNet: Spectral and temporal features based multi-task network for audio spoofing detection <br> <a href="https://ieeexplore.ieee.org/document/10007949">Paper</a></td>
        <td align="center">Sinc Filter</td>
        <td align="center">RawNet2, TCM, SCM</td>
        <td align="center">CE</td>
        <td align="center">LA: 2.45 (3)</td>
        <td align="center">LA: 0.062 (2)</td>
    </tr>
    <tr>
        <td align="center">A probabilistic fusion framework for spoofing aware speaker verification <br> <a href="https://arxiv.org/abs/2202.05253">Paper</a> <a href="https://github.com/yzyouzhang/SASV_PRF">Code</a></td>
        <td align="center">Mel Filter, Sinc Filter</td>
        <td align="center">ECAPA-TDNN, AASIST</td>
        <td align="center">BCE</td>
        <td align="center">LA: 1.53 (2)</td>
        <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">DSVAE: Interpretable disentangled representation for synthetic speech detection <br> <a href="https://arxiv.org/abs/2304.03323">Paper</a></td>
          <td align="center">Spectrogram</td>
          <td align="center">VAE</td>
            <td align="center">KL Divergence Loss, BCE</td>
            <td align="center">LA: 6.56 (5)</td>
            <td align="center">—</td>
    </tr>
    <tr>
        <td align="center">End-to-end dual-branch network towards synthetic speech detection <br> <a href="https://arxiv.org/abs/2205.12233">Paper</a> <a href="https://github.com/imagecbj/End-to-End-Dual-Branch-Network-Towards-Synthetic-Speech-Detection">Code</a></td>
          <td align="center">LFCC, CQT</td>
          <td align="center">Dual-Branch Network</td>
            <td align="center">Classification Loss, Fake Type Classification Loss</td>
            <td align="center"><b>LA: 0.80 (1)</b></td>
            <td align="center"><b>LA: 0.021 (1)</b></td>
    </tr>
</table>
Note: "—" indicates not mentioned in the paper. Values in brackets in the experimental results are the ranking of each column in the LA scenario, and bolded values are the best results for that scenario.

# Reference
More details about on the above, you may check the following this papers:
[//]:  (```python)

[//]: # (# @ARTICLE{xuyuxiong2023,)

[//]: # (# 	author={许裕雄},)

[//]: # (# 	journal={中国图象图形学报},)

[//]: # (# 	title={语音深度伪造检测研究进展},)

[//]: # (#  	year={2023},)

[//]: # (#   	volume={},)

[//]: # (#   	number={},)

[//]: # (#   	pages={},)

[//]: # (#   	doi={})

[//]: # (#    })

[//]: # (```)

# Statement
The purpose of this project is to establish a database based on  audio deepfake detection, solely for the purpose of communication and learning. All the content collected in this project is sourced from journals and the internet, and we express sincere gratitude to the researchers and authors who have published related research achievements.  In the event of a complaint of copyright infringement, the content will be removed as appropriate.

# Contact
We are glad to hear from you. If you have any questions, please feel free to contact <xuyuxiong2022@email.szu.edu.cn>.


