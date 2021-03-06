### 데이터 형태 변환하기

> ### 문제 소개
- 서버에서 주어진 json 데이터를 주어진 방식으로 변형해야 함.

```
서버에서 받은 데이터 = [
  {
    '수학': 80,
    '영어': 90,
    '국어': 100,
    '이름': '철수'
  },
  {
    '수학': 90,
    '영어': 70,
    '국어': 80,
    '이름': '영희'
  },
  ...
]

변형하고자 하는 데이터의 형태 = [
  {
    과목: '수학',
    철수: 80,
    영희: 90,
    영수: 70
  },
  ...
]
```

<br />

> ### 해결 코드
- Object.keys()메서드를 활용
```
function test (arr) {
    let temp = [];                    // 객체들을 담을 배열
    let keys = Object.keys(arr[0]);   // 맨 앞의 객체를 이용해 key로 이루어진 배열 만듬.

    for (let i = 0; i < keys.length; i++) {     // 배열의 각 인덱스에 '과목': '과목명' 으로 이루어진 프로퍼티 갖는 객체 생성
            temp.push({ '과목': keys[i] });   
    }

    for (let i = 0; i < arr.length; i++) {
        let current = arr[i];                   // 데이터의 각 인덱스에 대하여 반복문 실행     

        for (let j = 0; j < keys.length; j++) {     // 한 객체 내에서의 반복문을 실행하기 위해 key 배열을 대상으로 반복문 실행
            temp[j] = { …temp[j], [current.이름]: current[keys[j]]}    // 각 인덱스에 현재 학생(current에 할당된 학생)의 점수들을 뿌려 줌
        }
    }



    return temp.filter(el => el.과목 !== '이름');   // 모든 키에 대해 반복문을 실행했으므로 과목의 키 값이 이름인 객체가 존재, 따라서 해당 객체만 제거
}
```
