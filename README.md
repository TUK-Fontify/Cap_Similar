# Font Recommender

이미지를 입력하면 유사한 폰트를 추천해주는 CLIP 기반 추론 모듈입니다.

## 필요한 파일

아래 파일들을 별도로 전달받아 같은 폴더에 위치시켜 주세요.

```
font_recommender.py
clip_embeddings.h5
font_index.faiss
```

## 라이브러리 설치

```bash
pip install torch torchvision
pip install git+https://github.com/openai/CLIP.git
pip install faiss-cpu
pip install h5py
pip install Pillow
pip install numpy
```

## 사용법

```python
from font_recommender import FontRecommender

recommender = FontRecommender(
    emb_path="./clip_embeddings.h5",
    index_path="./font_index.faiss"
)

results = recommender.recommend("이미지.png", top_k=10)
```

## 반환 형태

```json
[
    {"rank": 1, "font": "gwendolyn/Gwendolyn-Bold", "similarity": 68.03},
    {"rank": 2, "font": "imperialscript/ImperialScript-Regular", "similarity": 67.84}
]
```

## 이미지 입력 방식

```python
# 1. 파일 경로
recommender.recommend("image.png", top_k=10)

# 2. PIL Image
from PIL import Image
img = Image.open("image.png")
recommender.recommend(img, top_k=10)

# 3. base64
recommender.recommend("data:image/png;base64,...", top_k=10)
```
