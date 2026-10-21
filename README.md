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
gh release create build-YYYYMMDD web/index.* web/*.png -R EdmundDaeKyu/edgerunners-play --title "빌드 YYYY-MM-DD" --notes "…"
```

예전 릴리스로 되돌리려면 Actions의 "배포"를 손으로 돌리며 태그를 넣는다.
