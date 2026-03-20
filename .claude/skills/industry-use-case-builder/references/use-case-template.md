---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '25'
ht-degree: 4%

---
# 업계 사용 사례 섹션 템플릿

업계 개요 파일 내의 각 사용 사례는 이러한 정확한 구조를 따릅니다.

## 템플릿

```markdown
## {{Use Case Title}}

{{1-2 sentence description of the business scenario. Explain what the use case does and why it matters to the customer. Write from a business perspective, not technical.}}

### Business impact

{{Quantified business outcomes. Use specific metrics where possible. Format: "{Industry} organizations typically see {metric} when implementing {this use case}."}}

### How to implement

Use the [{{Pattern Name}}](/help/blueprints/use-case-patterns/{{category}}/{{pattern-file}}.md) pattern. {{1-2 sentences explaining why this pattern is the right fit for this use case.}}

### Technical considerations

- {{Data requirement or integration point}}
- {{Regulatory or compliance consideration if applicable}}
- {{Performance or latency consideration}}
- {{Channel coordination or suppression logic}}
{{4-8 bullet points total}}
```

## 예

### 기본 예(소매)

```markdown
## Abandoned Cart Email Recovery

Automatically send personalized email reminders to customers who abandoned their shopping cart, including the exact items left behind and relevant offers to encourage completion. Cart abandonment is one of the largest sources of lost revenue in retail, and timely follow-up can recover a significant share of those sales.

### Business impact

Effective cart recovery programs deliver a 25-35% cart recovery rate and can generate an additional $100,000 to $500,000 in monthly revenue depending on store volume.

### How to implement

Use the [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) pattern. This approach responds to a real-time cart abandon event, sending a timely reminder while the purchase intent is still high.

### Technical considerations

- Cart abandon detection requires defining a threshold for inactivity (commonly 30-60 minutes) before triggering the first reminder
- Email content must dynamically pull current product images, prices, and availability from the catalog at send time
- Frequency capping rules should prevent customers from receiving multiple abandon cart emails in a short period
- Consent and suppression lists must be checked before sending
```

### 새로운 예(헬스케어)

```markdown
## Medication Adherence Campaigns

Send personalized reminders to help patients stay on track with medications, including refill timing, dosage instructions, and pharmacy information.

### Business impact

Healthcare organizations implementing medication adherence programs see a 15-25% improvement in prescription refill rates and measurable reductions in hospital readmissions.

### How to implement

Use the [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) pattern. This multi-touch approach guides patients through a sequence of reminders that adapt based on their refill behavior and engagement.

### Technical considerations

- Patient medication data must be integrated from pharmacy or EHR systems with appropriate HIPAA safeguards
- Reminder cadence should align with prescription duration and refill windows
- Communications must comply with HIPAA and patient consent requirements
- Multiple channels (SMS, email, app push) should be available with patient channel preference honored
```
