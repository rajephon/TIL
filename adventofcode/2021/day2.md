# --- Day 2: Dive! ---

[Link](https://adventofcode.com/2021/day/2)


## part 1

```python
def main(filename):
    depth = 0
    horizontal = 0
    with open(filename) as file:
        lines = file.readlines()

        for line in lines:
            cmd = line.split()
            direction = cmd[0]
            distance = int(cmd[1])

            if direction == 'forward':
                horizontal += distance
            elif direction == 'down':
                depth += distance
            elif direction == 'up':
                depth -= distance

    print('result: ', depth * horizontal)


if __name__ == '__main__':
    main("./input")
```

- 한 줄에 하나의 명령이 들어온다.
- 명령어는 `forward`, `down`, `up` 이렇게 세 종류가 존재한다.
- 수평 위치 `horizontal`와, 깊이 `depth`를 계산해야한다.
  - forward X 는 수평 위치를 더해준다.
  - down X 는 깊이를 더해준다.
  - up X 는 깊이를 **감소**한다.
- 모든 줄에 대해 순차적으로 계산한 값을 최종적으로 `horitontal`과 `depth`을 곱한다.

## part 2

```python
def main(filename):
    depth = 0
    horizontal = 0
    aim = 0
    with open(filename) as file:
        lines = file.readlines()

        for line in lines:
            cmd = line.split()
            direction = cmd[0]
            val = int(cmd[1])

            if direction == 'forward':
                horizontal += val
                depth += aim * val
            elif direction == 'down':
                aim += val
            elif direction == 'up':
                aim -= val

    print('result: ', depth * horizontal)


if __name__ == '__main__':
    main("./input")
```

- part 1에서 구한 값을 살짝 비틀어준 것이다.
- `depth`와 `horizontal`은 모두 `forward`에서 계산되며, `down`과 `up`은 `aim` 값을 조절한다.
- 예시를 따라 차근하게 동작을 파악하면 손쉽게 구할 수 있다.

