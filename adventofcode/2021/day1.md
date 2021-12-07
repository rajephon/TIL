# --- Day 1: Sonar Sweep ---

[Link](https://adventofcode.com/2021/day/1)

## part 1

```python
def main(filename):
    cnt = 0
    with open(filename) as file:
        lines = [int(i) for i in file.readlines()]
        for i in range(len(lines)):
            if i == 0:
                continue
            if lines[i] > lines[i-1]:
                cnt += 1
    print('result: ', cnt)


if __name__ == '__main__':
    main("./input")
```

- 지문이 길지만 결론은 이전 값보다 큰 경우가 몇 번 있는지 카운트하라는 것이다.  
- 파일을 줄 단위로 읽어와 정수형으로 변환한다.
- 루프를 돌며 이전 값보다 클 경우 카운트를 증가한다.

## part 2

```python
def main(filename):
    cnt = 0
    with open(filename) as file:
        lines = [int(i) for i in file.readlines()]
        first = lines[0] + lines[1] + lines[2]
        second = lines[1] + lines[2] + lines[3]
        i = 1
        while True:
            if first < second:
                cnt += 1
            if i+3 >= len(lines):
                break
            first = second
            second = second - lines[i] + lines[i+3]
            i += 1

    print('result: ', cnt)


if __name__ == '__main__':
    main('./input')
```

- 이번엔 _three-measurement sliding window_ 의 합을 비교한다. TCP/IP의 슬라이딩 윈도우를 생각하면 된다.
  - 연속된 3개의 수를 더한 값을 한 칸씩 이동하면서 서로 비교해 주면 된다. 

```text
199  A      
200  A B    
208  A B C  
210    B C D
200  E   C D
207  E F   D
240  E F G  
269    F G H
260      G H
263        H
```

- A와 B, B와 C, C와 D... 이런 식으로 연속된 3개 수를 계속 비교하며, 값이 커진 경우 카운트를 1 더한다.
- 전체 루프를 돌며 3개 수의 합을 계속 구하며 돌아도 되지만, 앞의 값을 빼고 뒤에 새로 더해주면서 계산해 보고 싶어 해당 방식으로 진행했다.