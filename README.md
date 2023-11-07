# [Sketch Simplification](https://esslab.jp/~ess/research/sketch/)

![Example result](/example_fig01_eisaku.png?raw=true "Example result of the provided model.")
제공된 모델의 예시 결과.  

이미지는 Eisaku Kubonouchi의 저작권 소유이며 ([@EISAKUSAKU](https://twitter.com/eisakusaku)), 비상업적 연구 용도로만 허용됩니다.

## 개요

이 코드는 다음 연구 논문에서 사용된 사전 학습 모델을 제공합니다:

```
   "Learning to Simplify: Fully Convolutional Networks for Rough Sketch Cleanup"
   Edgar Simo-Serra*, Satoshi Iizuka*, Kazuma Sasaki, Hiroshi Ishikawa (* 동등한 기여)
   ACM Transactions on Graphics (SIGGRAPH), 2016
```

그리고

```
   "Mastering Sketching: Adversarial Augmentation for Structured Prediction"
   Edgar Simo-Serra*, Satoshi Iizuka*, Hiroshi Ishikawa (* 동등한 기여)
   ACM Transactions on Graphics (TOG), 2018
```

더 자세한 정보는 [프로젝트 페이지](https://esslab.jp/~ess/research/sketch_master/)를 참조하세요.



## 종속성(Dependencies)

- [PyTorch](http://pytorch.org/) (버전 0.4.1) [torchvision](http://pytorch.org/docs/master/torchvision/)
- [pillow](http://pillow.readthedocs.io/en/latest/index.html)

모든 패키지는 표준 PyTorch 설치의 일부여야 합니다. PyTorch를 설치하는 방법에 대한 정보는 [torch 웹사이트](http://pytorch.org/)를 참조하세요.



## 사용법

첫 사용 전에 모델을 다음과 같이 다운로드해야 합니다:

```bash
bash download_models.sh
```

다음으로 다음과 같이 모델을 테스트할 수 있습니다:

```bash
python simplify.py
```

이제 `out.png`라는 파일이 생성되어 모델의 출력이 표시됩니다.

응용 프로그램 옵션은 다음과 같이 볼 수 있습니다:

```bash
python simplify.py --help
```



## 연필 드로잉 생성

동일한 인터페이스를 사용하여 연필 드로잉 생성을 수행할 수 있습니다. 이 경우 입력은 깨끗한 선 드로잉이어야 하며, 선 드로잉은 다음과 같이 생성할 수 있습니다:

```bash
python simplify.py --img test_line.png --out out_rough.png --model model_pencil2.t7
```

이렇게 하면 `test_line.png`의 굵은 버전인 `out_rough.png`이 생성됩니다. 모델을 변경하여 생성되는 굵은 스케치의 유형을 변경할 수 있습니다.



## 모델

- `model_mse.t7`: MSE 손실만 사용하여 훈련된 모델 (SIGGRAPH 2016 모델).
- `model_gan.t7`: GAN 손실 및 지도 및 비지도 학습 데이터를 사용하여 훈련된 모델 (TOG 2018 모델).
- `model_pencil1.t7`: 작가 1을 기반으로 한 연필 드로잉 생성을 위한 모델 (더러운 흐린 연필 선).
- `model_pencil2.t7`: 작가 2를 기반으로 한 연필 드로잉 생성을 위한 모델 (더 명확한 겹쳐진 연필 선).



## 논문 그림 복제

재현 가능성을 위해 논문의 그림을 복제하는 코드가 포함되어 있습니다. 모델을 다운로드한 후 다음과 같이 실행할 수 있습니다:

```bash
./figs.sh
```

이렇게 하면 `figs/`의 입력 이미지가 변환되어 `out/`에 결과가 저장됩니다. torch/pytorch 구현의 하드웨어 차이와 작은 차이로 인해 논문의 결과와 약간 다를 수 있음을 주의해야 합니다. 또한 결과는 본 문서 하단의 참고 사항에서 언급된 후 처리 없이 표시됩니다.

해당 문서의 이미지 저작권은 Eisaku Kubonoichi ([@EISAKUSAKU](https://twitter.com/eisakusaku))에 있으며, 일반적으로 비상업적 연구 용도만 허용됩니다. 특히, `fig16_eisaku.png`, `fig06_eisaku_robo.png`, `fig06_eisaku_joshi.png`, `fig01_eisaku.png`은 Eisaku Kubonoichi의 저작권입니다. 이미지 `fig14_pepper.png`와 `fig06_pepper.png`는 David Revoy ([www.davidrevoy.com](http://www.davidrevoy.com/))의 CC-by 4.0 라이선스하에 있습니다.



## 훈련

[훈련 readme](https://chat.openai.com/c/train/TRAIN.md)을 참조하세요.



## 참고 사항

- 모델은 Torch7 형식으로 제공되며 PyTorch 레거시 코드를 사용하여로드됩니다.
- 이는 2015년 말에서 2016년 말까지 다양한 기기에서 개발 및 테스트되었습니다.
- 제공된 모델은 비상업적 크리에이티브 커먼즈 라이선스 하에 제공됩니다.
- 후처리가 수행되지 않습니다. `convert out.png bmp:- | mkbitmap - -t 0.3 -o - | potrace --svg --group -t 15 -o - > out.svg`를 사용하여 수동으로 수행할 수 있습니다.



## 인용

이 모델을 사용하는 경우 다음과 같이 인용하십시오:

```scss
@Article{SimoSerraSIGGRAPH2016,
   author    = {Edgar Simo-Serra and Satoshi Iizuka and Kazuma Sasaki and Hiroshi Ishikawa},
   title     = {{Learning to Simplify: Fully Convolutional Networks for Rough Sketch Cleanup}},
   journal   = "ACM Transactions on Graphics (SIGGRAPH)",
   year      = 2016,
   volume    = 35,
   number    = 4,
}
```

그리고

```scss
@Article{SimoSerraTOG2018,
   author    = {Edgar Simo-Serra and Satoshi Iizuka and Hiroshi Ishikawa},
   title     = {{Mastering Sketching: Adversarial Augmentation for Structured Prediction}},
   journal   = "ACM Transactions on Graphics (TOG)",
   year      = 2018,
   volume    = 37,
   number    = 1,
}
```



## 감사의 말

본 작업은 JST CREST Grant Number JPMJCR14D1 와 JST ACT-I Grant Numbers JPMJPR16UD 와 JPMJPR16U3의 부분적인 지원을 받았습니다.



## 라이선스

이 스케치 단순화 코드는 무료 비상업적 사용을 위해 자유롭게 제공되며 이러한 조건 하에 재배포될 수 있습니다. 자세한 내용은 [라이선스](https://chat.openai.com/LICENSE)를 참조하세요.
