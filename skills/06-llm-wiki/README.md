# 06-llm-wiki · LLM Wiki

배포본 폴더명: `06 LLM 위키-수집·조회·점검` · 스킬 4개

| 스킬 | 소개 | 책에서 다루는 곳 | 설치 파일 |
|---|---|---|---|
| [wiki-research](./wiki-research/SKILL.md) | 위키용 자료 조사. 원문을 보존하고 출처를 확인 | 부록 B | [wiki-research.skill](../../dist/06-llm-wiki/wiki-research.skill) |
| [wiki-ingest](./wiki-ingest/SKILL.md) | 자료 → 위키 페이지. 흩어진 노트를 찾아 쓰는 형태로 저장 | 28장 | [wiki-ingest.skill](../../dist/06-llm-wiki/wiki-ingest.skill) |
| [wiki-activate](./wiki-activate/SKILL.md) | 위키 → 글·강의·책 원고. 쌓아 둔 위키를 소스로 활용 | 28장·29장 | [wiki-activate.skill](../../dist/06-llm-wiki/wiki-activate.skill) |
| [wiki-audit](./wiki-audit/SKILL.md) | 위키 점검. 중복·충돌·오래된 내용 정리 | 28장 | [wiki-audit.skill](../../dist/06-llm-wiki/wiki-audit.skill) |

폴더 안의 `SKILL.md`가 스킬 본체이고, `references/` 등 하위 폴더는 SKILL.md가 단계별로 읽는 참조 파일입니다. 설치는 [`INSTALL.md`](../../INSTALL.md)를 따릅니다.
