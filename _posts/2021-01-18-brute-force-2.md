---
layout: post
title: '완전탐색 문제풀이 #2'
subtitle: '프로그래머스 소수찾기 C++'
categories: algorithm
tags: problem
comments: true
---

## 문제 설명
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

## 제한사항
- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

## 입출력 예

| numbers   |    return     |
|-----------|:-------------:|
|   "17"    |       3       |
|   "011"   |       2       |

## 입출력 예 설명
### 입출력 예 #1
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

### 입출력 예 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.
- 11과 011은 같은 숫자로 취급합니다.


```cpp
#include <vector>
#include <cmath>
#include <algorithm>
using namespace std;

vector<int> primes;

bool isPrime(int n){
    if (n <= 1) return false;
    else if (n == 2 || n == 3) return true;
    else if (n % 2 == 0 || n % 3 == 0) return false;
    for (uint i = 5; i <= n / i; i++)
    {
        if (n % i == 0 || n % (i + 2) == 0) return false;
    }
    return true;
}

void ifPrimeAddNumber(vector<int> &picked, string numbers){
    int outout = 0;
    for (int i = 0; i < picked.size(); ++i){
        outout += pow(10, i) * (numbers[picked[i]] - '0');
    }
    if (isPrime(outout) && find(primes.begin(), primes.end(), outout) == primes.end()){
        primes.push_back(outout);
    }
}

void pickNumbers(string numbers, vector<int> &picked, int toPick){
    // 기저사례: 더 이상 고를 원소가 없을 때, primes에 고른 숫자를 넣고 반환한다.
    if (toPick == 0) {
        ifPrimeAddNumber(picked, numbers);
        return;
    }
    // 뽑지 않은 원소를 선택하여 재귀적으로 picked에 넣는다.
    for (int i = 0; i < numbers.size(); ++i){
        if (find(picked.begin(), picked.end(), i) != picked.end())
            continue;
        picked.push_back(i);
        pickNumbers(numbers, picked, toPick - 1);
        picked.pop_back();
    }
}

int solution(string numbers) {
    primes.clear();
    sort(numbers.begin(), numbers.end());
    for (int i = 1; i <= numbers.size(); ++i){
        vector<int> picked;
        pickNumbers(numbers, picked, i);
    }
    int answer = (int)primes.size();
    return answer;
}
```
