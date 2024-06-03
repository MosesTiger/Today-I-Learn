### TF-IDF 설명과 예제 코드

TF-IDF(Term Frequency-Inverse Document Frequency)는 문서 내 단어의 중요도를 평가하는 데 사용되는 통계적 수치입니다. TF-IDF는 주로 정보 검색과 텍스트 마이닝에 사용되며, 텍스트 데이터에서 중요한 단어를 찾아내는 데 유용합니다.

#### TF-IDF 구성 요소

1. **Term Frequency (TF)**: 특정 단어가 문서에서 얼마나 자주 등장하는지를 나타냅니다.
   [
   TF(t, d) = frac{text{특정 단어 t의 문서 d 내 등장 횟수}}{text{문서 d 내 모든 단어의 등장 횟수}}
   ]

2. **Inverse Document Frequency (IDF)**: 단어가 문서 전체에서 얼마나 일반적이거나 드문지를 나타냅니다.
   [
   IDF(t, D) = \log \left( \frac{\text{전체 문서 수}}{\text{단어 t가 등장하는 문서 수}} \right)
   ]

3. **TF-IDF 계산**:
   \[
   TF\text{-}IDF(t, d, D) = TF(t, d) \times IDF(t, D)
   \]

#### TF-IDF의 작동 원리

- **TF**는 특정 문서에서 단어의 빈도를 측정합니다.
- **IDF**는 단어가 전체 문서에서 얼마나 드문지를 측정합니다.
- **TF-IDF**는 두 값을 곱하여 단어의 중요도를 계산합니다. 높은 TF-IDF 값은 단어가 해당 문서에 중요하지만 전체 문서 집합에서는 드물다는 것을 의미합니다.

#### 예시

가령, 다음과 같은 세 개의 문서가 있다고 가정해 보겠습니다:

1. 문서1: "고양이와 강아지가 놀고 있다"
2. 문서2: "강아지가 공을 가져왔다"
3. 문서3: "고양이가 공을 가져왔다"

"강아지"라는 단어의 TF-IDF를 계산해 보겠습니다.

1. **TF**:
   - 문서1: 1/5 = 0.2
   - 문서2: 1/4 = 0.25
   - 문서3: 0/4 = 0.0

2. **IDF**:
   - "강아지"는 3개의 문서 중 2개 문서에 등장합니다.
   [
   IDF(\text{"강아지"}) = \log \left( \frac{3}{2} \right) \approx 0.176
   ]

3. **TF-IDF**:
   - 문서1: 0.2 * 0.176 ≈ 0.035
   - 문서2: 0.25 * 0.176 ≈ 0.044
   - 문서3: 0.0 * 0.176 = 0.0

이 예시를 통해 TF-IDF 값이 어떻게 계산되고, 어떤 단어가 문서 내에서 중요한지 평가하는 데 어떻게 사용되는지 이해할 수 있습니다.

#### Python 예제 코드

```python
from sklearn.feature_extraction.text import TfidfVectorizer

# 문서 데이터
documents = [
    "고양이와 강아지가 놀고 있다",
    "강아지가 공을 가져왔다",
    "고양이가 공을 가져왔다"
]

# TF-IDF 벡터라이저 초기화
vectorizer = TfidfVectorizer()

# TF-IDF 행렬 계산
tfidf_matrix = vectorizer.fit_transform(documents)

# 결과 출력
print(tfidf_matrix.toarray())
print(vectorizer.get_feature_names_out())
