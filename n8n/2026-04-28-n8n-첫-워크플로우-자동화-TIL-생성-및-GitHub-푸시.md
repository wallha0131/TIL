### Context

n8n을 사용하여 첫 번째 워크플로우 자동화를 구축하는 과정을 기록합니다. 이 자동화는 디스코드 메시지 수신을 트리거로 하여, 수신된 내용을 TIL(Today I Learned) 형식의 마크다운 문서로 변환하고, 이를 GitHub 저장소에 자동으로 푸시하는 것을 목표로 합니다. 푸시 완료 후에는 인덱스를 업데이트하고 최종 완료 메시지를 발송합니다.

### Core

*   **Trigger**: Discord 메시지 수신
    *   n8n의 Discord 노드를 사용하여 특정 채널 또는 DM에서 메시지를 감지합니다.
*   **Agent Execution**: 메시지 내용을 TIL 형식으로 변환
    *   수신된 텍스트를 기반으로 `YYYY-MM-DD-제목.md` 형식의 파일명과 TIL 구조(Context, Core, Insight)에 맞는 마크다운 콘텐츠를 생성합니다.
    *   제목은 메시지 내용을 요약하여 결정하며, 필요시 간단한 프롬프트 엔지니어링을 통해 최적화할 수 있습니다.
*   **GitHub Push**: 생성된 TIL 마크다운 파일을 GitHub 저장소에 푸시
    *   n8n의 GitHub 노드를 사용하여 Git 저장소에 연결하고, 생성된 마크다운 파일을 커밋 및 푸시합니다.
*   **Index Update**: 푸시된 파일의 인덱스 추가
    *   자동화된 인덱스 파일(예: `README.md` 또는 별도의 인덱스 파일)을 업데이트하여 새로 추가된 TIL을 추적합니다.
*   **Completion Message**: 완료 메시지 발송
    *   모든 작업이 성공적으로 완료되면, Discord 채널에 완료 알림 메시지를 전송합니다.

### Insight

n8n을 처음 사용해보았는데, 직관적인 인터페이스와 다양한 노드 연동성을 통해 복잡한 워크플로우를 비교적 쉽게 구축할 수 있다는 점이 매우 인상 깊었습니다. 특히 코드 몇 줄 작성하는 것보다 n8n을 통해 시각적으로 워크플로우를 설계하고 자동화하는 것이 훨씬 효율적이라는 것을 체감했습니다. 이번 자동화는 디스코드 메시지를 TIL로 변환하여 GitHub에 기록하는 과정을 자동화함으로써, 학습한 내용을 체계적으로 관리하는 데 큰 도움을 줄 것으로 기대됩니다.

**출처:**
*   [n8n Documentation](https://docs.n8n.io/)
*   [GitHub Actions Documentation](https://docs.github.com/en/actions)
*   [Discord API Documentation](https://discord.com/developers/docs/intro)