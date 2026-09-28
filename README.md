# Burnrail AI bill merger

Merge your OpenAI and Anthropic cost reports in one offline HTML file, and see the three places where a cheaper model would have saved the most (an estimate).

- **What it is**: a single HTML file (`burnrail-preview.html`). Open it in a browser, choose the cost-report JSON files you downloaded from each provider, and it shows the combined total, the total per project or workspace, and the top 3 estimated savings.
- **Private by design**: the file reads your JSON inside the browser and sends nothing anywhere. Its Content Security Policy (`default-src 'none'; form-action 'none'; base-uri 'none'`) blocks background requests such as fetch, XHR, images and fonts, and form submission. The only way out is the waitlist link at the bottom, which navigates only when you click it. Project, key and workspace ids are masked by default.
- **Totals are the provider's numbers**: the combined total is the sum of what each provider reports. The price table is used only for the savings estimate.

## How to use
1. Download `burnrail-preview.html` from the [latest release](../../releases/latest). Check it against `burnrail-preview.html.sha256` in the same release (`shasum -a 256 -c burnrail-preview.html.sha256`).
2. Get your cost reports as JSON. Admin API keys are needed for these endpoints; the keys never go into this tool.
   - OpenAI: `GET /v1/organization/costs` with `group_by=line_item` (for per-model rows) and optionally `group_by=project_id`.
   - Anthropic: `GET /v1/organizations/cost_report` with `group_by[]=description` (for per-model rows) and optionally `group_by[]=workspace_id`.
   - If a response says `has_more: true`, save the next pages too and select them all.
3. Open `burnrail-preview.html`, pick the files (several at once is fine), and optionally enter a KRW exchange rate.
4. Try it first with the fake files in [`examples/provider/`](examples/provider).

## Method and limits
- **Totals**: summed exactly in integer micro-cents from the provider's reported amounts. When a KRW rate is entered, each row is rounded separately, so rows may differ from the total by about ₩1.
- **Estimated savings**: for each large model, the tool shows the next cheaper model at the same provider and at the other provider, where both input and output token prices are lower. **Quality is not checked.** Test with your own data before switching.
- **Model detection**: OpenAI's `line_item` is assumed to look like `"<model>, input"` / `"<model>, output"`. This format is not documented in the API spec. Rows that do not match are counted in the total as "unknown model". The report shows what share of spend it could attribute to a model.
- **Early-access link (v0.2.0)**: below the waitlist link, the report shows one more link, "monthly automatic report and spend alerts — early access". The line next to it says the feature **does not exist yet, its price is under consideration, and nothing is sold or charged**. Each time the file opens, it picks one example monthly price (USD 29, 79 or 199) with a local random number and adds it to the link as `utm_content=paid-<price>`, so we can count which example price people click. Picking the price makes no network request; the link, like the waitlist link, navigates only when clicked.
- **Scope**: OpenAI and Anthropic cost-report JSON only. Other providers, CSV exports and usage (token) endpoints are not read. The interface text is in Korean in v0.1.0.

## Data sources and licenses
- Code: MIT ([LICENSE](LICENSE)).
- Model prices: LiteLLM price table at a pinned commit, MIT. Details and the full license text are in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
- Example files in `examples/provider/` are made up. They are not real customer data.

## Requests and feedback
- Want another provider or file type, or a feature after merging? Open an issue with the [provider request](../../issues/new?template=provider-request.yml) or [what should come next](../../issues/new?template=paid-interest.yml) form. Spend and price questions are optional ranges. Nothing is for sale; answers are counted to decide what to build. There is no promise of a reply or schedule.
- Issues are public. **Do not paste company names, account or key ids, or any part of a real bill or cost report.**

## Updates
- Changes are listed in [CHANGELOG.md](CHANGELOG.md). A price-table update is a new release.
- Contact: hello@burnrail.com · Updates: [burnrail.com](https://burnrail.com/?utm_source=gh-release&utm_medium=tool&utm_campaign=ai-bill-merge-v0.2.0)

## 한국어

OpenAI·Anthropic 비용 보고서를 오프라인 HTML 파일 하나에서 합치고, 더 싼 모델을 썼다면 가장 많이 아꼈을 곳 3개(추정)를 보여 줍니다.

- **무엇인가**: HTML 파일 하나(`burnrail-preview.html`)입니다. 브라우저로 열고 공급사에서 내려받은 비용 보고서 JSON을 고르면, 합친 금액, 프로젝트·워크스페이스별 금액, 추정 절감이 큰 3곳을 보여 줍니다.
- **내 컴퓨터에서만 읽음**: 파일은 브라우저 안에서만 읽히고 어디에도 보내지 않습니다. 콘텐츠 보안 정책(`default-src 'none'; form-action 'none'; base-uri 'none'`)이 fetch·XHR·이미지·폰트 같은 백그라운드 요청과 폼 전송을 막습니다. 밖으로 나가는 길은 맨 아래 대기자 링크 하나이고, 누를 때만 이동합니다. 프로젝트·키·워크스페이스 id는 기본으로 가립니다.
- **합계는 공급사가 청구한 금액**: 합계는 각 공급사가 보고한 금액을 더한 값입니다. 단가표는 절감 추정에만 씁니다.

### 쓰는 법
1. [최신 릴리스](../../releases/latest)에서 `burnrail-preview.html`을 받고, 같은 릴리스의 `burnrail-preview.html.sha256`으로 확인합니다(`shasum -a 256 -c burnrail-preview.html.sha256`).
2. 비용 보고서를 JSON으로 받습니다. 이 엔드포인트에는 관리자 API 키가 필요합니다. 키는 이 도구에 넣지 않습니다.
   - OpenAI: `GET /v1/organization/costs`, 모델별로 보려면 `group_by=line_item`(프로젝트별은 `group_by=project_id` 추가).
   - Anthropic: `GET /v1/organizations/cost_report`, 모델별로 보려면 `group_by[]=description`(워크스페이스별은 `group_by[]=workspace_id` 추가).
   - 응답에 `has_more: true`가 있으면 다음 페이지도 저장해 함께 고릅니다.
3. `burnrail-preview.html`을 열고 파일을 고릅니다(여러 개 가능). 원화 환율은 선택입니다.
4. 먼저 [`examples/provider/`](examples/provider)의 가짜 파일로 해 볼 수 있습니다.

### 방법과 한계
- **합계**: 공급사가 보고한 금액을 정수(마이크로센트)로 정확히 더합니다. 원화 환율을 넣으면 줄마다 반올림하므로 줄의 합이 합계와 1원쯤 다를 수 있습니다.
- **추정 절감**: 금액이 큰 모델마다, 같은 공급사와 다른 공급사에서 입력·출력 단가가 둘 다 싼 한 단계 아래 모델을 보여 줍니다. **품질은 검증하지 않았습니다.** 바꾸기 전에 자기 데이터로 확인하세요.
- **모델 알아내기**: OpenAI의 `line_item`이 `"<모델>, input"`·`"<모델>, output"` 꼴이라고 가정합니다. API 스펙에 적힌 형식이 아닙니다. 이 꼴이 아닌 줄은 "모델 미상"으로 합계에만 넣고, 모델을 알아낸 금액 비율을 화면에 표시합니다.
- **조기 신청 링크(v0.2.0)**: 대기자 링크 아래에 "월간 자동 리포트·지출 알림 — 조기 신청" 링크가 하나 더 있습니다. 바로 옆 문구에 이 기능은 **아직 없고, 가격은 검토 중이며, 지금 결제·판매는 없다**고 적혀 있습니다. 파일을 열 때마다 예시 월 가격(29·79·199달러) 하나를 로컬 난수로 고르고, 링크에 `utm_content=paid-<가격>`으로 붙여 어떤 예시 가격에서 누르는지 셉니다. 가격 고르기는 네트워크 요청을 하지 않고, 링크는 대기자 링크처럼 누를 때만 이동합니다.
- **범위**: OpenAI·Anthropic 비용 보고서 JSON만 읽습니다. 다른 공급사, CSV, 사용량(토큰) 엔드포인트는 읽지 않습니다. v0.1.0의 화면 문구는 한국어입니다.

### 자료 출처와 라이선스
- 코드: MIT([LICENSE](LICENSE)).
- 모델 단가: 커밋 고정된 LiteLLM 단가표, MIT. 자세한 출처와 라이선스 전문은 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)에 있습니다.
- `examples/provider/`의 예시 파일은 지어낸 값입니다. 실제 고객 데이터가 아닙니다.

### 요청과 의견
- 다른 공급사·파일 형식이나 합산 다음 기능을 원하면 [공급사 요청](../../issues/new?template=provider-request.yml) 또는 [다음에 필요한 것](../../issues/new?template=paid-interest.yml) 양식으로 이슈를 남겨 주세요. 지출·가격 질문은 선택 범위입니다. 판매하는 것은 없고, 답은 무엇을 만들지 정하는 데 집계합니다. 응답·일정은 약속하지 않습니다.
- 이슈는 공개됩니다. **회사명·계정·키 id·청구서 원문(일부 포함)을 붙이지 마세요.**

### 갱신
- 변경 기록은 [CHANGELOG.md](CHANGELOG.md)에 있습니다. 단가표 갱신도 새 릴리스로 냅니다.
- 연락: hello@burnrail.com · 소식: [burnrail.com](https://burnrail.com/?utm_source=gh-release&utm_medium=tool&utm_campaign=ai-bill-merge-v0.1.3)
