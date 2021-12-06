# --- Day 1: Sonar Sweep ---

[Link](https://adventofcode.com/2021/day/1)

지문이 길지만 결론은 이전 값보다 큰 경우가 몇 번 있는지 카운트하라는 말이다.  
파일을 줄 단위로 읽어와 정수형으로 변환 후 이전 값과 비교하면 끝끝  

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

익숙치 않은 언어로도 연습해보자.