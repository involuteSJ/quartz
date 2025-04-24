---
CMDS: "[[103 Algorithm]]"
creation date: 2025-04-10 09:04
modification date: 2025-04-10 09:04:44
type:
  - note
tags:
  - "#KMP"
관련 문서:
  - "[[103.01 Basic Concepts]]"
category: content
---

# KMP

<center><i><b>K</b>nuth-<b>M</b>orris-<b>P</b>ratt Algorithm</i></center>

- 불일치가 발생한 앞 부분에 대하여 다시 비교하지 않고 수행

## 개요

KMP 알고리즘은 문자열 검색 알고리즘 중 하나로, 패턴 매칭을 효율적으로 수행하기 위해 고안되었습니다. 1977년 Donald Knuth, Vaughan Pratt, James H. Morris에 의해 개발되었으며, 최악의 경우에도 선형 시간 복잡도 \( O(n + m) \) 을 보장합니다. 여기서 \( n \)은 텍스트의 길이, \( m \)은 패턴의 길이입니다.

## 핵심 아이디어

- **불일치 발생 시 효율적인 재시작:** 불일치가 발생한 앞부분에 대해 다시 비교하지 않고, 미리 계산된 정보를 활용하여 비교를 이어갑니다.
- **접두사와 접미사의 활용:** 패턴 내에서 접두사이면서 동시에 접미사인 부분을 활용하여 불필요한 비교를 줄입니다.

## 작동 원리

### 1. 부분 일치 테이블 (LPS 배열) 생성

패턴에서 각 위치까지의 접두사와 접미사가 일치하는 최대 길이를 저장한 배열인 LPS(Longest Prefix Suffix) 배열을 미리 계산합니다. 이 배열을 통해 불일치 발생 시 어느 위치부터 다시 비교를 시작할지 결정합니다.

**예시: 패턴 "ABABCABAB"의 LPS 배열 계산**

| 인덱스 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|--------|---|---|---|---|---|---|---|---|---|
| 문자   | A | B | A | B | C | A | B | A | B |
| LPS    | 0 | 0 | 1 | 2 | 0 | 1 | 2 | 3 | 4 |

### 2. 패턴 매칭 과정

텍스트를 순회하면서 패턴과 일치하는 부분을 찾습니다. 불일치가 발생하면 LPS 배열을 활용하여 패턴을 적절히 이동시켜 불필요한 비교를 피합니다.

**알고리즘 단계:**

1. **초기화:** 텍스트 인덱스 \( i = 0 \), 패턴 인덱스 \( j = 0 \)
2. **비교:** 텍스트의 \( i \)번째 문자와 패턴의 \( j \)번째 문자를 비교
   - 일치하면 \( i \)와 \( j \)를 증가
   - \( j = m \)이 되면 패턴이 일치한 것이므로 결과 기록 후 \( j = lps[j-1] \)로 이동
3. **불일치 시:**
   - \( j \)가 0이면 \( i \)만 증가
   - \( j \)가 0이 아니면 \( j = lps[j-1] \)로 이동하여 재비교

## 장점

- **선형 시간 복잡도:** 최악의 경우에도 \( O(n + m) \)의 시간 복잡도를 유지
- **불필요한 비교 감소:** 불일치 발생 시 패턴 내부의 정보를 활용하여 비교를 최소화
- **효율적 메모리 사용:** 추가적인 메모리 사용이 패턴의 길이에 비례하여 효율적

## 예제

**텍스트:** "ABABDABACDABABCABAB"  
**패턴:** "ABABCABAB"

**매칭 과정:**

1. 텍스트와 패턴을 처음부터 비교
2. 불일치가 발생하면 LPS 배열을 참조하여 패턴을 적절히 이동
3. 매칭이 완료되면 매칭 위치를 기록

매칭 결과: 패턴이 텍스트의 인덱스 10에서 일치

## 구현 예시 (Python)

```python
def compute_lps(pattern):
    lps = [0] * len(pattern)
    length = 0  # 이전 LPS 길이
    i = 1
    while i < len(pattern):
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length != 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1
    return lps

def kmp_search(text, pattern):
    lps = compute_lps(pattern)
    i = j = 0  # 텍스트와 패턴 인덱스
    while i < len(text):
        if pattern[j] == text[i]:
            i += 1
            j += 1
        if j == len(pattern):
            print(f"패턴이 텍스트의 인덱스 {i - j}에서 발견됨")
            j = lps[j - 1]
        elif i < len(text) and pattern[j] != text[i]:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1

# 사용 예시
text = "ABABDABACDABABCABAB"
pattern = "ABABCABAB"
kmp_search(text, pattern)
```

**출력:**
```
패턴이 텍스트의 인덱스 10에서 발견됨
```

## 결론

KMP 알고리즘은 효율적인 패턴 매칭을 가능하게 하는 강력한 알고리즘입니다. 부분 일치 테이블을 활용하여 불일치 시 비교를 최소화함으로써 선형 시간 내에 패턴을 찾을 수 있습니다. 문자열 검색이 자주 필요한 분야에서 널리 사용되며, 이해하고 구현해 두면 다양한 문제 해결에 유용하게 활용할 수 있습니다.