# PNG

## 매직넘버

`89 50 4E 47 0D 0A 1A 0A`

`50 4E 47` 이 ASCII로 `PNG`

## Chunk

| Length  | Chunk type | Chunk data   | CRC     |
|---------|------------|--------------|---------|
| 4 bytes | 4 bytes    | Length bytes | 4 bytes |

### Chunk type

총 18가지 타입의 청크가 있으며, 아래의 4개는 PNG 파일에서 중요하며 올바르게 해석되어야 하는 청크 타입이다.

- IHDR : 이미지 헤더
- PLTE : 팔레트 테이블
- IDAT : 이미지 데이터
- IEND : 파일의 끝

기타 청크 타입들
- `tRNS`, `cHRM`, `gAMA`, `iCCP`, `sBIT`, `sRGB`, `iTXt`, `tEXt`, `zTXt`, `bKGD`, `hIST`, `pHYs`, `sPLT`, `tIME`


### ETC

메타데이터 등에 이상한(?) 데이터를 넣기 좋으므로, 이미지를 업로드 받아 사용할 경우 sanitization이 필요하다.


## Reference
- [PNG 파일 구조 - ryanking13](https://ryanking13.github.io/2018/03/24/png-structure.html)
- [매직넘버 - Wikipedia](https://en.wikipedia.org/wiki/File_format#Magic_number)
- [PNG - w3.org](https://www.w3.org/TR/PNG/#4Concepts.EncodingChunking)