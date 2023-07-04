[//]: # (# 语音深度伪造检测研究进展 Research progress on audio deepfake detection)
[//]: # (***)

>The related contents of this review will be updated next.

# Table of contents
- [Speech Large Model](#Speech Large Model)
- [Datasets](#Datasets)
- [Audio Deepfake Detection](#Audio Deepfake Detection)
    - [Audio Preprocessing](##Audio Preprocessing)
      - [Commonly Used Noise Datasets](###Commonly Used Noise Datasets)
      - [Audio Enhancement Methods](###Audio Enhancement Methods)
    - [Feature Extraction](###Feature Extraction)
      - [Handcrafted Feature-based Forgery Detection](####Handcrafted Feature-based Forgery Detection)
      - [Hybrid Feature-based Forgery Detection](####Hybrid Feature-based Forgery Detection)
      - [End-to-End Forgery Detection](####End-to-End Forgery Detection)
      - [Feature-level Fusion Forgery Detection](####Feature-level Fusion Forgery Detection)
    - [Network Training](###Network Training)
      - [Supervised Learning-based Forgery Detection](####Supervised Learning-based Forgery Detection)
      - [Adversarial Training-based Forgery Detection](####Adversarial Training-based Forgery Detection)
      - [Multi-task Learning-based Forgery Detection](####Multi-task Learning-based Forgery Detection)
- [References](##References)
- [Statement](##Statement)
- [Contact](##Contact)

# <span id="Speech Large Model">Speech Large Model</span>
***
|                             Model 	                              | Publisher 	 | Achievable Tasks                                                                                                                                                                            |
|:----------------------------------------------------------------:|:-----------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       VoiceBox   <br>  [Website](https://voicebox.metademolab.com/) 	        |   Meta 	    | 1. Synthesize speech across six languages<br> 2. Remove transient noise<br> 3. Edit content<br> 4. Transfer audio style within and across languages<br>5. Generate diverse speech samples 	 |
| SpeechGPT <br>  [Code](https://github.com/0nutation/SpeechGPT) 	 | Fudan University | 1. Perceive and generate multi-modal contents <br> 2. Spoken dialogue LLM with strong human instruction                                                                                     |
|    USM  <br>  [Website](https://sites.research.google/usm/) 	    |  Google 	   | 1. ASR beyond 100 languages<br> 2. Downstream ASR tasks <br> 3. Automated Speech Translation (AST)                                                                 |

# Datasets
***
|  Attack Types   |                                                  Dataset 	                                                  |          Number of Audio  <br>（Subdataset：Real/Fake） 	          |     Language 	     |
|:---------------:|:-----------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------:|:------------------:|
|      TTS 	      | WaveFake    <br> [Dataset](https://zenodo.org/record/5642694)   [Paper](https://arxiv.org/abs/2111.02813) 	 |                         16283/117985 	                          | English/Japanese 	 |
|      TTS 	      |                                                    HAD 	    <br>   [Paper](https://arxiv.org/abs/2104.03617)  	                                                                          |                         53612/107224 	                          |     Chinese 	      |
|      TTS 	      |                                                 ADD 2022 	<br>   [Paper](https://arxiv.org/pdf/2202.08433v2.pdf) 	                                                                       |   LF: 5619/46067  <br>PF: 5319/46419  <br>FG-D: 5319/46206 	    |        Chinese 	        |
|      TTS 	      |                      CMFD   <br>  [Dataset](https://github.com/WuQinfang/CMFD)     [Paper](https://ieeexplore.ieee.org/document/9921343) 	                                                                    |           Chinese: 1800/1000 <br>English: 1800/1000 	           |      English/Chinese 	       |
|      TTS 	      |                  In-the-Wild  <br>  [Dataset](https://deepfake-demo.aisec.fraunhofer.de/in_the_wild)        [Paper](https://arxiv.org/abs/2203.16263) 	                                                                        |                          19963/11816 	                          |        English 	        |
|      TTS 	      |                     FAD      <br>  [Dataset](https://zenodo.org/record/6635521#.Ysjq4nZBw2x)        [Paper](https://arxiv.org/abs/2207.12308#:~:text=FAD%20dataset%20can%20be%20used%20not%20only%20for,remain%20challenging.%20The%20FAD%20dataset%20is%20publicly%20available.) 	        |                         115800/115800 	                         |        Chinese 	        |
|    Replay 	     |                     ASVspoof 2017 <br>  [Dataset](https://datashare.ed.ac.uk/handle/10283/3055) 	      [Paper](https://www.asvspoof.org/asvspoof2017overview_cameraReady.pdf) 	                                                         |                          3565/14465 	                           |        English 	        |
|    TTS和VC 	     |                         ReMASC     <br>  [Dataset](https://github.com/YuanGongND/ReMASC) 	                  [Paper](https://arxiv.org/abs/1904.03365) 	                                                                         |                          9240/45472 	                           |    English/Chinese/Hindi 	     |
|    TTS和VC 	     |                            AVspoof  <br>  [Dataset](https://zenodo.org/record/4081040) 	                             [Paper](https://ieeexplore.ieee.org/document/7358783) 	                                                                  |             LA: 15504/120480  <br>PA: 15504/14465 	             |        English 	        |
|    TTS和VC 	     |                          ASVspoof 2015  <br>  [Dataset](http://dx.doi.org/10.7488/ds/298) 	             [Paper](https://datashare.ed.ac.uk/bitstream/handle/10283/853/ASVspoof2015_evaluation_plan.pdf?sequence=2&isAllowed=y) 	                                    |                         16651/246500 	                          |        English 	        |
|    TTS和VC 	     |                          FMFCC-A   <br>  [Dataset](https://github.com/Amforever/FMFCC-A) 	           [Paper](https://arxiv.org/abs/2110.09441#:~:text=The%20FMFCC-A%20dataset%20is%20by%20far%20the%20largest,10%2C000%20genuine%20Mandarin%20utterances%20collected%20from%2058%20speakers.) 	 |                          10000/40000 	                          |        Chinese 	        |
|    TTS和VC 	     |                     SceneFake  <br>  [Dataset](https://zenodo.org/record/7663324#.Y_XKMuPYuUk) 	      [Paper](https://arxiv.org/abs/2211.06073) 	                                                                          |                          19838/64642 	                          |        English 	        |
|    TTS和VC 	     |                                                  EmoFake    <br>           [Paper](http://arxiv.org/abs/2211.05363) 	                                                                          |                          35000/53200 	                          |      English/Chinese 	       |
|    TTS和VC 	     |                     PartialSpoof <br>  [Dataset](https://zenodo.org/record/4817532#.YLd8Yi2l1hF) 	             [Paper](https://arxiv.org/abs/2104.02518)	                                                                         |                         12483/108978 	                          |        English 	        |
|    TTS和VC 	     |                                                 ADD 2023  <br>      [Paper](https://arxiv.org/abs/2305.13774)	                                                                          | FG-D: 172819/113042  <br>RL: 55468/65449  <br>AR: 14907/95383 	 |        Chinese 	        |
|    TTS和VC 	     |                         DECRO  <br>  [Dataset](https://github.com/petrichorwq/DECRO-dataset) 	   [Paper](https://dl.acm.org/doi/10.1145/3543507.3583222) 	                                                                   |         Chinese: 21218/41880 <br>English: 12484/42799 	         |      English/Chinese 	       |
| TTS、VC和Replay 	 |                      ASVspoof 2019 <br>  [Dataset](https://datashare.ed.ac.uk/handle/10283/3336) 	          [Paper](https://arxiv.org/abs/1904.05441)	                                                                        |            LA: 12483/108978  <br>PA: 28890/189540 	             |        English 	        |
| TTS、VC和Replay 	 |                       ASVspoof 2021  <br>  [Dataset](https://www.asvspoof.org/index2021.html) 	                    [Paper](https://arxiv.org/abs/2109.00535) 	                                                                        | LA: 18452/163114  <br>PA: 126630/816480  <br>PF: 14869/519059 	 |        English 	        |

[^1]:https://arxiv.org/abs/2111.02813
# Audio Deepfake Detection
***

## Audio Preprocessing
***

### Commonly used Noise Datasets
***
|                                       Dataset 	                                        |                                                                                                                                     Description 	                                                                                                                                     |
|:--------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                      MUSAN [Dataset](https://www.openslr.org/17/)                      |       A corpus of music, speech and noise                      |
|                       RIR [Dataset](https://www.openslr.org/28/)                       |   A database of simulated and real room impulse responses, isotropic and point-source noises. The audio files in this data are all in 16k sampling rate and 16-bit precision.  |
|           NOIZEUS [Dataset](https://ecs.utdallas.edu/loizou/speech/noizeus/)           |       Contains 30 IEEE sentences (generated by three male and three female speakers) corrupted by eight different real-world noises at different SNRs. Noises include suburban train noise, murmur, car, exhibition hall, restaurant, street, airport and train station noise.        |
|               NoiseX-92  [Dataset](http://spib.linse.ufsc.br/noise.html)               |                             All noises are obtained with a duration of 235 seconds, a sampling rate of 19.98 KHz, an analogue-to-digital converter (A/D) with 16 bits, an anti-alias filter and no pre-emphasis stage. Fifteen noise types are included.                              |
|            DEMAND [Dataset](https://zenodo.org/record/1227121#.YXtsyPlBxjU)            |                                                                                                            Multi-channel acoustic noise database for diverse environments.                                                                                                            |
|                ESC-50 [Dataset](https://github.com/karolpiczak/ESC-50)                 | A tagged collection of 2000 environmental audios obtained from clips in Freesound.org, suitable for environmental sound classification. The dataset consists of 5-second-long recordings organised into 5 broad categories, each with 10 subcategories (40 examples per subcategory). |
| ESC [Dataset](http://shujujishi.com/dataset/69b2bf03-d855-4f8b-ab96-1ec80e285863.html) |                                                                                                                       Including the ESC-50, ESC-10, and ESC-US.                                                                                                                       |
|            FSD50K [Dataset](https://zenodo.org/record/4060432#.Y1kvcHZByUk)            |   An open dataset of human tagged sound events containing 51,197 Freesound clips totalling 108.3 hours of multi-labeled audio, unequally distributed across 200 classes from the AudioSet Ontology.                                                                                                          |

### Audio Enhancement Methods
|                                                                                                                                                                               Method 	                                                                                                                                                                               |                                                                Description 	                                                                 |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------:|
|                                                                                                                           SpecAugment <br> [Paper](https://arxiv.org/pdf/1904.08779.pdf)   [Code](https://github.com/DemisEom/SpecAugment)                                                                                                                           |                               Enhancement strategies include time warping, frequency masking and time masking                                |  
|                                                                                                                     WavAugment <br> [Paper](https://arxiv.org/abs/2007.00991)  [Code](https://github.com/facebookresearch/WavAugment)                                                                                                                     | Enhancement strategies include pitch randomization, reverberation, additive noise, time dropout (temporal masking), band reject and clipping | 
|                                                              RawBoost  <br> [Paper](https://arxiv.org/abs/2007.00991)      [Code](https://github.com/TakHemlata/RawBoost-antispoofing)                                                               | Enhancement strategies include linear and non-linear convolutive noise, impulsive signal-dependent additive noise and stationary signal-independent additive noise |    

## Feature Extraction
***

### Handcrafted Feature-based Forgery Detection
***
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
	    <td align="center">Detecting spoofing attacks using VGG and SincNet: BUT-Omilia submission to ASVspoof 2019 challenge <a href="https://arxiv.org/abs/1907.12908">Paper</a> and <a href="https://github.com/mravanelli/SincNet">SincNet Code</a></td>
	    <td align="center">—</td>
        <td align="center">CQT, power spectrum</td>
        <td align="center">VGG, SincNet</td>
        <td align="center">CE</td>
        <td align="center">LA: 8.01 (4)<br>PA: 1.51 (2)</td>
        <td align="center">LA: 0.208 (4)<br><b>PA: 0.037 (1)</b></td>
	</tr>
    <tr>
        <td align="center">Long-term high frequency features for synthetic speech detection <a href="https://www.sciencedirect.com/science/article/pii/S1051200419301769#:~:text=The%20long-term%20information%20has%20been%20found%20to%20be,from%20the%20long-term%20constant-Q%20transform%20%28CQT%29%20based%20features.">Paper</a></td>
        <td align="center">Cafe, white and street noise</td>
        <td align="center">ICQC, ICQCC, ICBC, ICLBC</td>
        <td align="center">DNN</td>
        <td align="center">CE</td>
        <td align="center">LA: 7.78 (3)</td>
        <td align="center">LA: 0.187 (3)</td>
    </tr>
    <tr>
        <td align="center">Voice spoofing countermeasure for logical access attacks detection <a href="https://ieeexplore.ieee.org/document/9638512">Paper</a></td>
        <td align="center">—</td>
        <td align="center">ELTP-LFCC</td>
        <td align="center">DBiLSTM</td>
        <td align="center">—</td>
        <td align="center"><b>LA: 0.74 (1)</b></td>
        <td align="center"><b>LA: 0.008 (1)</b></td>
    </tr>
    <tr>
        <td align="center">Voice spoofing detector: A unified anti-spoofing framework <a href="https://www.sciencedirect.com/science/article/pii/S0957417422002330">Paper</a></td> 
        <td align="center">—</td>
        <td align="center">ATP-GTCC</td>
        <td align="center">SVM</td>
        <td align="center">Hamming <br> Distance</td>
        <td align="center">LA: 0.75 (2)<br><b>PA: 1.00 (1)</b></td>
        <td align="center">LA: 0.050 (2)<br>PA: 0.064 (2)</td>
    </tr>
</table>

### Hybrid Feature-based Forgery Detection
***
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
        <td align="center">Light convolutional neural network with feature genuinization for detection of synthetic speech attacks <a href="https://arxiv.org/pdf/2009.09637.pdf">FG-LCNN Paper</a></td>
        <td align="center">-</td>
        <td align="center">CQT-based LPS</td>
        <td align="center">LCNN</td>
        <td align="center">-</td>
        <td align="center">LA: 4.07 (11)</td>
        <td align="center">LA: 0.102 (10)</td>
    </tr>
    <tr>
        <td align="center">Siamese convolutional neural network using gaussian probability feature for spoofing speech detection <a href="http://www.interspeech2020.org/uploadfile/pdf/Mon-3-2-9.pdf">Siamese CNN Paper</a></td>
        <td align="center">-</td>
        <td align="center">LFCC</td>
        <td align="center">Siamese CNN</td>
        <td align="center">CE</td>
        <td align="center">LA: 3.79 (10)<br>PA: 7.98 (5)</td>
        <td align="center">LA: 0.093 (5)<br>PA: 0.195 (2)</td>
    </tr>
    <tr>
        <td align="center">Generalization of audio deepfake detection <a href="https://www.researchgate.net/profile/Avrosh-Kumar/publication/345141913_Generalization_of_Audio_Deepfake_Detection/links/600cb38945851553a0678e07/Generalization-of-Audio-Deepfake-Detection.pdf">ResNet18-LCML-FM Paper</a></td>
        <td align="center">RIR and MUSAN</td>
        <td align="center">LFB</td>
        <td align="center">ResNet18</td>
        <td align="center">LCML</td>
        <td align="center">LA: 1.81 (4)</td>
        <td align="center">LA: 0.052 (4)</td>
    </tr>
    <tr>
        <td align="center">(Ma et al., 2021)</td>
        <td align="center">-</td>
        <td align="center">LFCC</td>
        <td align="center">LCNN, DFWF</td>
        <td align="center">Similarity Loss</td>
        <td align="center">LA: 7.74 (15)<br>PA: 8.85 (6)</td>
        <td align="center">-</td>
    </tr>
    <tr>
        <td align="center">(Ge et al., 2021)</td>
        <td align="center">Frequency Mask</td>
        <td align="center">LFCC</td>
        <td align="center">PC-DARTS</td>
        <td align="center">WCE</td>
        <td align="center">LA: 4.96 (12)</td>
        <td align="center">LA: 0.091 (8)</td>
    </tr>
    <tr>
        <td align="center">(Zhang et al., 2021)</td>
        <td align="center">-</td>
        <td align="center">LFCC</td>
        <td align="center">ResNet18</td>
        <td align="center">OC-Softmax</td>
        <td align="center">LA: 2.19 (7)</td>
        <td align="center">LA: 0.059 (5)</td>
    </tr>
    <tr>
        <td align="center">(Li et al., 2021)</td>
        <td align="center">-</td>
        <td align="center">CQT</td>
        <td align="center">SE-Res2Net50</td>
        <td align="center">BCE</td>
        <td align="center">LA: 1.81 (4)<br>PA: 0.46 (2)</td>
        <td align="center">LA: 0.074 (7)<br>PA: 0.012 (2)</td>
    </tr>
    <tr>
        <td align="center">(Zhang et al., 2021)</td>
        <td align="center">RIR dataset noise addition, call coding, and device coding</td>
        <td align="center">LFCC</td>
        <td align="center">LCNN, ResNet-OC</td>
        <td align="center">OC-Softmax, CE</td>
        <td align="center">LA: 3.92 (10)</td>
        <td align="center">-</td>
    </tr>
    <tr>
        <td align="center">(Rostami et al., 2021)</td>
        <td align="center">specAug, Attention Mask</td>
        <td align="center">LFCC</td>
        <td align="center">EfficientNet-A0, SE-Res2Net50</td>
        <td align="center">WCE, Triplet Loss</td>
        <td align="center">LA: 1.89 (6)<br>PA: 0.86 (4)</td>
        <td align="center">LA: 0.507 (11)<br>PA: 0.024 (4)</td>
    </tr>
    <tr>
        <td align="center">(Kwak et al., 2021)</td>
        <td align="center">-</td>
        <td align="center">CQT</td>
        <td align="center">ResMax</td>
        <td align="center">BCE</td>
        <td align="center">LA: 2.19 (7)<br><b>PA: 0.37 (1)</b></td>
        <td align="center">LA: 0.060 (6)<br><b>PA: 0.009 (1)</b></td>
    </tr>
    <tr>
        <td align="center">(Wang et al., 2022)</td>
        <td align="center">Adding noise according to a signal-to-noise ratio of 15dB or 25dB</td>
        <td align="center">CQT</td>
        <td align="center">SE-Res2Net34-Confromer</td>
        <td align="center">CE</td>
        <td align="center">LA: 1.85 (5)</td>
        <td align="center">LA: 0.060 (6)</td>
    </tr>
    <tr>
        <td align="center">(Li et al., 2022)</td>
        <td align="center">-</td>
        <td align="center">L-VQT</td>
        <td align="center">L-DenseNet</td>
        <td align="center">NLLLoss</td>
        <td align="center">LA: 1.54 (3)</td>
        <td align="center">LA: 0.045 (3)</td>
    </tr>
    <tr>
        <td align="center">(Xue et al., 2023)</td>
        <td align="center">-</td>
        <td align="center">LPS, F0</td>
        <td align="center">ECANet, SENet</td>
        <td align="center">A-Softmax</td>
        <td align="center">LA: 1.00 (2)<br>PA: 0.65 (3)</td>
        <td align="center">LA: 0.031 (2)<br>PA: 0.017 (3)</td>
    </tr>
    <tr>
        <td align="center">(Ma et al., 2023)</td>
        <td align="center">-</td>
        <td align="center">LFCC, MFCC</td>
        <td align="center">TDNN, SENet34</td>
        <td align="center">LCML</td>
        <td align="center"><b>LA: 0.83 (1)</b></td>
        <td align="center"><b>LA: 0.024 (1)</b></td>
    </tr>
</table>

### End-to-end Forgery Detection
***

### Feature-level Fusion Forgery Detection
***

## Network Training
***
### Self-supervised Learning-based Forgery Detection
***
### Adversarial Training-based Forgery Detection
***
### Multi-task Learning-based Forgery Detection
***



# Reference
***
More details about on the above, you may check the following this papers:
```python
# @ARTICLE{xuyuxiong2023,
# 	author={许裕雄},
# 	journal={中国图象图形学报},
# 	title={语音深度伪造检测研究进展},
#  	year={2023},
#   	volume={},
#   	number={},
#   	pages={},
#   	doi={}
#    }
```

# Statement
***
The purpose of this project is to establish a database based on  audio deepfake detection, solely for the purpose of communication and learning. All the content collected in this project is sourced from journals and the internet, and we express sincere gratitude to the researchers and authors who have published related research achievements.  In the event of a complaint of copyright infringement, the content will be removed as appropriate.

# Contact
***
We are glad to hear from you. If you have any questions, please feel free to contact <xuyuxiong2022@email.szu.edu.cn>.


