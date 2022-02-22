# Github Actions

## 버전 태그가 푸시되었을 때만 동작하게 하려면?

```yaml
on:
  push:
    tags:
      - '[0-9]+.[0-9]+.[0-9]+'
```

## 태그를 가져오기

```yaml
${{ github.ref_name }}
```

- [`github` context](https://docs.github.com/en/actions/learn-github-actions/contexts#github-context)
- 워크플로우를 동작시킨 브랜치 or 태그 이름

## 이전 job 가동이 끝나면 동작하도록 설정하기

```yaml
jobs:
  first-job:
    name: First job
    steps:
      - name: first hello
        run: echo "Hello first Job"
  second-job:
    name: Second job
    needs: first-job
    steps:
      - name: second hello
        run: echo "Hello second Job"
```

- `needs`로 지정.
- `needs: [job1, job2]` 처럼 배열 지정도 가능

## 빌드 매트릭스

```yaml
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    strategy:
      matrix:
        fruit: [banana, apple, cherry, kiwi]
    steps:
      - run: echo ${{ matrix.fruit }}
```

- job 의 여러 값에 대한 처리를 진행할 수 있음.

