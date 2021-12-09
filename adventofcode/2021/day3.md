# --- Day 3: Binary Diagnostic ---

[Link](https://adventofcode.com/2021/day/3)

## part 1

```python
def main(filename):
    gamma = 0
    epsilon = 0
    with open(filename) as file:
        lines = file.read().splitlines()
        cnt = [0] * len(lines[0])
        for line in lines:
            for i in range(len(line)):
                cnt[i] += 1 if line[i] == '1' else -1

        for i in range(len(cnt)):
            power = pow(2, len(cnt)-i-1)
            if cnt[i] > 0:
                gamma += power
            else:
                epsilon += power

    print('result: ', cnt)
    print('gamma: {}, epsilon: {}, multiply: {}'.format(gamma, epsilon, gamma*epsilon))


if __name__ == '__main__':
    main('./input')

```

- 입력 값의 같은 위치의 비트가 1이 더 많으면 1, 0이 더 많으면 0으로 구한 다음 10진수로 바꿨을 때의 값이 `gamma rate`, `gamma rate`의 비트를 뒤집을 경우 `epsilon rate`이 된다.
- 입력 값의 길이만큼의 빈 리스트 `cnt`를 만들고, 루프를 돌면서 같은 위치에 1을 만나면 1을, 0을 만나면 -1을 더한다.
- cnt를 값이 구해지면, 2진수 값을 구한다. cnt의 자릿값이 0보다 크면 1, 작으면 0이라 가정한다.
- `epsilon rate`는 `gamma rate`와 반대이므로, `gamma rate`의 값이 더해지지 않을 때 더한다.


## part 2

```python
def rating(lines, pos, most_common, result):
    if len(lines) == 0 or len(lines[0]) == pos:
        return result
    if len(lines) == 1:
        return lines[0]

    zeros = []
    ones = []
    choice = '0'
    for line in lines:
        if line[pos] == '0':
            zeros.append(line)
        else:
            ones.append(line)

    if most_common:
        if len(zeros) <= len(ones):
            choice = '1'
    else:
        if len(zeros) > len(ones):
            choice = '1'

    return rating(ones if choice == '1' else zeros, pos+1, most_common, result+choice)


def main(filename):
    with open(filename) as file:
        lines = file.read().splitlines()
        oxygen = int(rating(lines, 0, True, ''), 2)
        co2 = int(rating(lines, 0, False, ''), 2)
    print(oxygen, co2, oxygen * co2)


if __name__ == '__main__':
    main('./input')
```

- part 1을 살짝 비튼 문제다. `oxygen generator rating`은 같은 자리에 0 혹은 1중에 더 많이 나오는 수의 값의 원소를 이어간다. 단, 0과 1의 카운트가 같을 경우 1로 시작하는 원소를 선택한다.
- `CO2 scrubber rating`은 반대다. 같은 자리에 0과 1중에 더 적게 나온 원소를 선택한다. 단, 0과 1의 빈도가 같을 경우 0으로 시작하는 원소를 선택한다.
- 이번에는 재귀함수로 쫓아가는게 나을 것 같아 사용했다. 매 호출마다, 지정된 자리의 값을 확인한다.
- 자릿값이 0이면 `zeros`에, 1이면 `ones`에 추가한다.
  - 사실 이 부분의 필터링은 다음과 같은 두 줄로 작성할 수도 있다.
    ```python
    zeros = [item for item in lines if item[pos] == '0']
    ones = [item for item in lines if item[pos] == '1']
    ```
- 이후, 0과 1이 나온 횟수를 비교해서 각 상황(더 많이 나온 값을 구하는 경우인지, 나온 횟수가 같은지)에 따라 자릿값이 0인 경우의 리스트 혹은 1인 경우의 리스트를 다음 호출로 전달한다.
