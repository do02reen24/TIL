# 📚 이미지 파일 형식의 차이

## 📌 GIF(Graphics Interchange Format)

- GIF는 비트맵 그래픽 파일 포맷이다.
- 최대 256색까지 저장할 수 있는 비손실 압축 형식이다.
- 1개의 파일에 여러 개의 이미지를 저장할 수 있어 간단한 애니메이션 효과를 낼 수 있다.

## 📌 JPEG(Joint Photographic Experts Group)

- 정지 화상을 위해서 만들어진 손실 압축 방법 표준이다.
- 압축률을 높이면 파일 크기는 작아지지만 이미지 품질은 더욱 떨어진다.

## 📌 PNG(Portable Network Graphics)

- 비손실 그래픽 파일 포맷 중 하나
- GIF의 포맷의 문제를 해결하고 개선하기 위해 고안되었다.

### GIF와 비교

- 대부분의 경우 PNG가 GIF에 비해 압축률이 높다.
- GIF의 단색 투명층과 달리 PNG는 8비트 알파 채널을 이용한 다양한 투명층을 지원한다.
- 256색까지 지원하는 GIF와 달리 PNG는 트루컬러(24비트에 해당하는 색으로 16,777,216개의 색상을 지원)를 지원한다.
- GIF에서 제공되는 애니메이션을 PNG는 지원하지 않음

### JPEG와의 비교

- JPEG는 사진에 특화된 손실 압축 알고리즘을 사용하므로 PNG에 비해 더 작은 파일을 만들 수 있다.
- 문자나 날카로운 경계가 있는 그림은, JPEG에서 뭉개지는 현상이 쉽게 생길 수 있으므로 PNG를 쓰는 것이 좋다.
- 나중에 고화질의 재편집을 해야 한다면 PNG로 저장해 놓는 것이 낫다. JPEG를 사용할 때는 저장을 하면 할수록 손실이 누적될 수 있다.

## 💌 학습링크

- PNG(https://ko.wikipedia.org/wiki/PNG)
- GIF(https://ko.wikipedia.org/wiki/GIF)
- JPEG(https://ko.wikipedia.org/wiki/JPEG)
