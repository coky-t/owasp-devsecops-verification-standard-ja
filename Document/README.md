# OWASP DevSecOps Verification Standard

<img width="180px" align="right" style="float: right;" src="v1/document/images/logo.svg"></a>

OWASP DevSecOps 検証標準 (OWASP DevSecOps Verification Standard, DSOVS) はあらゆるソフトウェアプロジェクトや組織におけるベースライン要件を定義するオープンソースフレームワークです。DSOVS は以下の目的で使用できます。


* 🧐 **ギャップ分析 (Gap Analysis)** 
    * DSOVS はソフトウェア開発ライフサイクルのすべてのステップをカバーする明確に定義されたカテゴリを内外のアナリストに提供することにより、単一または複数のソフトウェアプロジェクト内に存在するギャップを特定するために使用できます。

* 🗺️ **成熟度ロードマップ (Maturity Roadmap)** 
    * DSOVS は開発者、アーキテクト、セキュリティ担当者、その他誰でも、既存の DevSecOps の成熟度を特定し、より高い成熟度に向けた取り組みのための明確な道筋を描くために使用できます。

* ⚠️ **サードパーティのリスク評価時 (During Third-party Risk Asessments)** 
    * DSOVS はサードパーティのソフトウェア開発ライフサイクル (SDLC) 成熟度の監査に使用できます。サードパーティのソフトウェア開発プロセスに耐性があることを保証し、人、プロセス、ソフトウェアに起因する潜在的な脆弱性を特定するのに役立つため、これは重要です。

## 🥇 DSOVS 支持者 (DSOVS Advocates)

DSOVS 支持者は OWASP DSOVS を支援し、プロジェクトの推進に大量のリソースを捧げ、重大かつ一貫した貢献をし、業界全体にプロジェクトを促進してきた業界の専門家です。

## 💬 連絡先
<li><a href="https://owasp.slack.com/messages/project-devsecops-verification-standard/details/"><img src="v1/document/images/slack_logo.png" width="14px">  #project-devsecops-verification-standard</a></li>
<li><a href="https://linkedin.com/realjvo"><img src="v1/document/images/linkedin.svg" width="14px"> @realjvo </a> (Jamieson Vincenti O'Reilly, プロジェクトリーダー)</li><li><a href="https://linkedin.com/realjvo"><img src="v1/document/images/linkedin.svg" width="14px"> @yudhiy </a> (Yudhi Yudhistira, プロジェクトリーダー)</li>


## 🎉 参加するには
プロセスやテクノロジが絶えず変化する中で、あなたの貢献が DSOVS の進化に役立ちます。

DSOVS をより良いオープンソースプロジェクトにするために、あらゆる種類の貢献やフィードバックを歓迎します。

今すぐコミュニティに参加して、旅の仲間になりましょう。

* 🐞 [エラー (誤植、文法) を報告する](https://github.com/OWASP/www-project-devsecops-verification-standard/issues)
* 🛠️ [プルリクエストを使用して、エラーの修正や変更を提案する](https://github.com/OWASP/www-project-devsecops-verification-standard/pulls)
* 🙋 [質問する](https://github.com/OWASP/www-project-devsecops-verification-standard/discussions/categories/q-a)
* 💡 [新しいアイデア](https://github.com/OWASP/www-project-devsecops-verification-standard/discussions/categories/ideas)

## ✍🏽 DSOVS の翻訳

`main` にベースプロジェクトができたら、翻訳に取り掛かるでしょう。

## 📖 目次 (Table-of-Contents)

### 組織 (Organisation) フェーズ
🚧 [ORG-001 リスク評価 (Risk Assessment)](v1/document/ORG-001-Risk-Assessment.md)

🚧 [ORG-002 セキュリティトレーニング (Security Training)](v1/document/ORG-002-Security-Training.md)

🚧 [ORG-003 セキュリティ担当者 (Security Champion)](v1/document/ORG-003-Security-Champion.md)

🚧 [ORG-004 セキュリティレポート (Security Reporting)](v1/document/ORG-004-Security-Reporting.md)

### 要件 (Requirements) フェーズ
🚧 [REQ-001 セキュリティポリシーと規制遵守 (Security Policy and Regulatory Compliance)](v1/document/REQ-001-Security-Policy-and-Regulatory-Compliance.md)

🚧 [REQ-002 セキュリティ要件と標準 (Security Requirements and Standards)](v1/document/REQ-002-Security-Requirements-and-Standards.md)

🚧 [REQ-003 セキュリティユーザーストーリーと受け入れ基準 (Security User Stories and Acceptance Criterias)](v1/document/REQ-003-Security-User-Stories-and-Acceptance-Criteria.md)

🚧 [REQ-004 セキュリティ課題の追跡 (Security Issues Tracking)](v1/document/REQ-004-Security-Issues-Tracking.md) 

### 設計 (Design) フェーズ
🚧 [DES-001 セキュリティアーキテクチャ設計レビュー (Security Architecture Design Reviews)](v1/document/DES-001-Secure-Architecture-Design-Reviews.md)

🚧 [DES-002 脅威モデリング (Threat Modelling)](v1/document/DES-002-Threat-Modelling.md)


### コード/ビルド (Code/Build) フェーズ
🚧 [CODE-001 セキュア開発環境 (Secure Development Environment)](v1/document/CODE-001-Secure-Development-Environment.md)

✅ [CODE-002 ハードコードされたシークレットの検出 (Hardcoded Secrets Detection)](v1/document/CODE-002-Hardcoded-Secrets-Detection.md)

🚧 [CODE-003 手動セキュアコードレビュー (Manual Secure Code Review)](v1/document/CODE-003-Manual-Secure-Code-Review.md)

🚧 [CODE-004 静的アプリケーションセキュリティテスト (Static Application Security Testing, SAST)](v1/document/CODE-004-Static-Application-Security-Testing-SAST.md)

🚧 [CODE-005 ソフトウェアコンポジション解析 (Software Composition Analysis, SCA)](v1/document/CODE-005-Software-Composition-Analysis-SCA.md)

🚧 [CODE-006 ソフトウェアライセンスコンプライアンス (Software License Compliance)](v1/document/CODE-006-Software-License-Compliance.md)

🚧 [CODE-007 インライン IDE セキュアコード解析 (Inline IDE Secure Code Analysis)](v1/document/CODE-007-Inline-IDE-Secure-Code-Analysis.md)

🚧[CODE-008 コンテナセキュリティスキャン (Container Security Scanning)](v1/document/CODE-008-Container-Security-Scanning.md)

🚧 [CODE-009 セキュア依存関係管理 (Secure Dependency Management)](v1/document/CODE-009-Secure-Dependency-Management.md)

### テスト (Test) Phase
🚧 [TEST-001 セキュリティテスト管理 (Security Test Management)](v1/document/TEST-001-Security-Test-Management.md)

✅ [TEST-002 動的アプリケーションセキュリティテスト (Dynamic Application Security Testing, DAST)](v1/document/TEST-002-Dynamic-Application-Security-Testing-DAST.md)

🚧 [TEST-003 インタラクティブアプリケーションセキュリティテスト (Interactive Application Security Testing, IAST)](v1/document/TEST-003-Interactive-Application-Securit-Testing-IAST.md)

🚧 [TEST-004 ペネトレーションテスト (Penetration Testing)](v1/document/TEST-004-Penetration-Testing.md)

🚧 [TEST-005 セキュリティテストカバレッジ (Security Test Coverage)](v1/document/TEST-005-Security-Test-Coverage.md)

### リリース/デプロイ (Release/Deploy) フェーズ
🚧 [REL-001 成果物署名 (Artifact Signing)](v1/document/REL-001-Artifact-Signing.md)

🚧 [REL-002 セキュア成果物管理 (Secure Artifact Management)](v1/document/REL-002-Secure-Artifact-Management.md)

🚧 [REL-003 シークレット管理 (Secret Management)](v1/document/REL-003-Secret-Management.md)

🚧 [REL-004 セキュアコンフィグレーション (Secure Configuration)](v1/document/REL-004-Secure-Configuration.md)

🚧 [REL-005 セキュリティポリシーの実施 (Security Policy Enforcement)](v1/document/REL-005-Security-Policy-Enforcement.md)

🚧 [REL-006 Infrastructure-as-Code (IaC) セキュアデプロイメント (Infrastructure-as-Code (IaC) Secure Deployment)](v1/document/REL-006-Infrastructure-as-Code-Secure-Deployment.md)

🚧 [REL-007 コンプライアンススキャン (Compliance Scanning)](v1/document/REL-007-Compliance-Scanning.md)

🚧 [REL-008 セキュアリリース管理 (Secure Release Management)](v1/document/REL-008-Secure-Release-Management.md)

### 運用/監視 (Operate/Monitor) フェーズ
🚧 [OPR-001 環境の堅牢化 (Environment Hardening)](v1/document/OPR-001-Environment-Hardening.md)

🚧 [OPR-002 アプリケーションの堅牢化 (Application Hardening)](v1/document/OPR-002-Application-Hardening.md)

🚧 [OPR-003 環境セキュリティログ記録 (Environment Security Logging)](v1/document/OPR-003-Environment-Security-Logging.md)

🚧 [OPR-004 アプリケーションセキュリティログ記録 (Application Security Logging)](v1/document/OPR-004-Application-Security-Logging.md)

✅ [OPR-005 脆弱性の開示 (Vulnerability Disclosure)](v1/document/OPR-005-Responsible-Disclosure.md)

🚧 [OPR-006 証明書管理 (Certificate Management)](v1/document/OPR-006-Certificate-Management.md)

🚧 [OPR-007 攻撃対象領域管理 (Attack Surface Management)]()