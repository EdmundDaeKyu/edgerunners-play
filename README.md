# Edgerunners — 웹 빌드

사이버펑크 2077을 탑다운 로그라이트로 재구성한 게임의 웹 빌드다.
`https://edmunddaekyu.github.io/edgerunners-play/`에서 바로 해 볼 수 있다.
소개와 기획서는 `https://edmunddaekyu.github.io/edgerunners/`에 있다.

게임 소스는 이 저장소에 없다. 여기에는 배포 설정만 있다.

## 올리는 법

게임 데이터(`index.pck`)가 100MB를 넘어 저장소에 커밋할 수 없다.
그래서 내보낸 파일을 릴리스 첨부 파일로 올리고, `.github/workflows/deploy.yml`이 그 파일을 받아 Pages로 배포한다.

```bash
# 게임 저장소에서 내보내기(web/에 index.html · .js · .wasm · .pck …)
bash tools/export_web.sh

# 릴리스로 올리면 배포가 저절로 돈다
gh release create build-YYYYMMDD web/index.* -R EdmundDaeKyu/edgerunners-play --title "빌드 YYYY-MM-DD" --notes "…"
```

예전 릴리스로 되돌리려면 Actions의 "배포"를 손으로 돌리며 태그를 넣는다.

**릴리스는 늘 이 저장소의 새 커밋 위에 만든다.** 태그가 앞 릴리스와 같은 커밋을 가리키면 배포 작업은 성공으로 끝나도 Pages가 예전 파일을 계속 내보낸다(2026-10-22 build-20261022-3에서 겪음).
그래서 웹 빌드를 올리기 전에 아래 "빌드 기록"에 한 줄을 넣어 커밋한다.

## Windows 판

웹 판은 브라우저 구동 한계로 처음 접속할 때 로딩이 1분 넘게 걸린다(셰이더를 처음 그릴 때 컴파일한다).
그래서 내려받아 실행하는 Windows 판을 같은 저장소의 `windows-YYYYMMDD` 릴리스로 올린다.
배포 작업은 `build-*` 릴리스만 배포하므로 Windows 판 릴리스는 사이트에 영향을 주지 않는다.

```bash
# 게임 저장소에서 내보내기(build/Edgerunners-windows.zip)
bash tools/export_windows.sh

gh release create windows-YYYYMMDD build/Edgerunners-windows.zip -R EdmundDaeKyu/edgerunners-play --latest=false --title "Windows 판 YYYY-MM-DD" --notes "…"
```

## 빌드 기록

- build-20261022-4: 정예 저격수 레이저 조준선
