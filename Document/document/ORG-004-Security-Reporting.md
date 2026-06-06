# セキュリティレポート (Security Reporting)

| ID            |
| ------------- |
| DSOVS-ORG-004 |

## 概要

セキュリティレポートは組織内のセキュリティ関連の活動に関するデータを収集および分析する継続的なプロセスです。

組織のセキュリティ態勢に関する重要な洞察を提供し、意思決定者が既存の脅威と潜在的な脅威をより正確に特定および評価できるようにし、組織がサイバーセキュリティインシデントに迅速かつ適切に対応できるようにするため、セキュリティレポートは DevSecOps の重要な部分となっています。

また、セキュリティレポートは組織がより優れたセキュリティポリシー、プラクティス、手順を開発し、データ保護やその他の法的要件および規制要件の遵守を確実にするのにも役立ちます。

## レベル 0 - セキュリティに関する調査結果は多くのシステムやツールで分かれている

Security findings are scattered across numerous disconnected systems and tools, with each scanner, tracker, or assessment maintaining its own isolated view. There is no consolidated reporting, so leadership has no coherent picture of the organisation's security posture and cannot reliably understand where risk concentrates. Because the data is fragmented and never brought together, trends go unnoticed, duplicate issues are common, and decisions about prioritisation and investment are made without an accurate evidence base.

## レベル 1 - 複数の情報源から得られたセキュリティ調査結果は手作業で一つのレポートにまとめている

Findings from the various sources are manually gathered and combined into a single report, giving the organisation its first unified view of security issues. This collation is typically performed periodically by individuals who export, deduplicate, and summarise results by hand, which makes it possible to communicate an overall position to stakeholders. The process is labour-intensive and prone to inconsistency and delay, so while it is a clear improvement over completely siloed data, the report quickly becomes stale and its accuracy depends heavily on the diligence of whoever assembles it.

```mermaid
graph LR; Source-A & Source-B-- manually collated -->Single-Report-- reported to -->Leadership;
```

## レベル 2 - 複数の情報源から得られたセキュリティ調査結果は一元管理されたダッシュボードに定期的に追加されている

Findings from multiple sources are now fed into a centralised dashboard on a regular, repeatable basis, replacing manual report assembly with a defined and consistent process. Leadership and delivery teams can view a common, up-to-date representation of findings, severities, and ownership, which supports more reliable prioritisation and clearer accountability. Because the dashboard is populated on a schedule rather than continuously, the information still lags behind reality between refresh cycles, but the consistency and shared visibility represent a substantial step beyond hand-built reports.

```mermaid
graph LR; Source-A & Source-B-- periodically populated -->Centralised-Dashboard-- reported to -->Leadership;
```

## レベル 3 - 一元管理されたダッシュボードがリアルタイムにデータを取得し表示している

The centralised dashboard captures and represents data in real time, so the organisation's security posture is reflected as findings are discovered, triaged, and resolved. Leadership has continuous visibility into key metrics, KPIs, trends, and emerging risk, enabling timely, data-driven decisions and meaningful tracking of improvement over time. With reporting measured and continuously refined, the organisation can detect changes in its risk profile quickly, validate the effectiveness of its security efforts, and align investment with the areas of greatest exposure.

```mermaid
graph LR; Source-A & Source-B-- real-time capture -->Centralised-Dashboard-- live metrics and KPIs -->Leadership;
```

## Further reading
- [OWASP SAMM](https://owaspsamm.org/) - The Software Assurance Maturity Model, including the metrics and measurement practices that underpin meaningful security reporting.
- [OWASP DevSecOps Maturity Model (DSOMM)](https://owasp.org/www-project-devsecops-maturity-model/) - A maturity model that describes how to measure and improve security activities across the DevSecOps lifecycle.
- [NIST Secure Software Development Framework (SSDF), SP 800-218](https://csrc.nist.gov/projects/ssdf) - Guidance on the practices and outcomes that security reporting and metrics should help organisations demonstrate.
