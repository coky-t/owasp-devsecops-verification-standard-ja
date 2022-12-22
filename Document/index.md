---

layout: col-sidebar
title: OWASP DevSecOps 検証標準
tags: DSOVS
level: 2
type: documentation
pitch: DSOVS はソフトウェア開発ライフサイクルの中でセキュリティを実装しようとする際のギャップを特定するためのフレームワークです

---

OWASP DevSecOps 検証標準 (OWASP DevSecOps Verification Standard, DSOVS) はサイバーセキュリティの専門家がソフトウェア開発業務におけるソフトウェアセキュリティのギャップを特定するためのオープンソースフレームワークです。DSOVS は組織がソフトウェア開発ライフサイクルにおける要員、プロセス、ツールの面から品質向上の機会を強調するのに役立ちます。DSOVS は単にセキュリティツールを実装するだけでなく、セキュリティプラクティスを定着させる能力を成熟させることに重点を置いています。したがって、DSOVS は技術にとらわれず、特定のソフトウェア開発手法に縛られることはありません。

OWASP DevSecOps 検証標準には七つのフェーズがあり、ほとんどのソフトウェアエンジニアリングプラクティスにおけるフェーズと整合しています。
* 組織 (Organisation)
* 要件 (Requirement)
* 設計 (Design)
* コード/ビルド (Code/Build)
* テスト (Test)
* リリース/デプロイ (Release/Deploy)
* 運用/監視 (Operate/Monitor)

各フェーズには DSOVS が評価するストリームがあります。
* 組織 (Organisation)
  * ORG-001 リスク評価 (Risk Assessment)
  * ORG-002 セキュリティトレーニング (Security Training)
  * ORG-003 セキュリティ担当者 (Security Champion)
  * ORG-004 セキュリティレポート (Security Reporting)
* 要件 (Requirement)
  * REQ-001 セキュリティポリシーと規制遵守 (Security Policy and Regulatory Compliance)
  * REQ-002 セキュリティ要件と標準 (Security Requirements and Standards)
  * REQ-003 セキュリティユーザーストーリーと受け入れ基準 (Security User Stories and Acceptance Criterias)
  * REQ-004 セキュリティ課題の追跡 (Security Issues Tracking)
* 設計 (Design)
  * DES-001 セキュリティアーキテクチャ設計レビュー (Security Architecture Design Reviews)
  * DES-002 脅威モデリング (Threat Modelling)
  * DES-003 セキュアドキュメント (Secure Documentation)
* コード/ビルド (Code/Build)
  * CODE-001 セキュア開発環境 (Secure Development Environment)
  * CODE-002 ハードコードされたシークレットの検出 (Hardcoded Secrets Detection)
  * CODE-003 手動セキュアコードレビュー (Manual Secure Code Review)
  * CODE-004 静的アプリケーションセキュリティテスト (Static Application Security Testing, SAST)
  * CODE-005 ソフトウェアコンポジション解析 (Software Composition Analysis, SCA)
  * CODE-006 ソフトウェアライセンスコンプライアンス (Software License Compliance)
  * CODE-007 インライン IDE セキュアコード解析 (Inline IDE Secure Code Analysis)
  * CODE-008 コンテナセキュリティスキャン (Container Security Scanning)
  * CODE-009 セキュア依存関係管理 (Secure Dependency Management)
* テスト (Test)
  * TEST-001 セキュリティテスト管理 (Security Test Management)
  * TEST-002 動的アプリケーションセキュリティテスト (Dynamic Application Security Testing, DAST)
  * TEST-003 インタラクティブアプリケーションセキュリティテスト (Interactive Application Security Testing, IAST)
  * TEST-004 ペネトレーションテスト (Penetration Testing)
  * TEST-005 セキュリティテストカバレッジ (Security Test Coverage)
* リリース/デプロイ (Release/Deploy)
  * REL-001 成果物署名 (Artifact Signing)
  * REL-002 セキュア成果物管理 (Secure Artifact Management)
  * REL-003 シークレット管理 (Secret Management)
  * REL-004 セキュアコンフィグレーション (Secure Configuration)
  * REL-005 セキュリティポリシーの実施 (Security Policy Enforcement)
  * REL-006 Infrastructure-as-Code (IaC) セキュアデプロイメント (Infrastructure-as-Code (IaC) Secure Deployment)
  * REL-007 コンプライアンススキャン (Compliance Scanning)
  * REL-008 セキュアリリース管理 (Secure Release Management)
* 運用/監視 (Operate/Monitor)
  * OPR-001 環境の堅牢化 (Environment Hardening)
  * OPR-002 アプリケーションの堅牢化 (Application Hardening)
  * OPR-003 環境セキュリティログ記録 (Environment Security Logging)
  * OPR-004 アプリケーションセキュリティログ記録 (Application Security Logging)
  * OPR-005 脆弱性の開示 (Vulnerability Disclosure)
  * OPR-006 証明書管理 (Certificate Management)
  * OPR-007 攻撃対象領域管理 (Attack Surface Management)
