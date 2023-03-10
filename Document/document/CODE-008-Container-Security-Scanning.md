# コンテナセキュリティスキャン (Container Security Scanning)

| ID             |
| -------------- |
| DSOVS-CODE-008 |

## 概要

コンテナセキュリティスキャンはコンテナのコンテンツを解析して、脆弱なコンポーネント、構成の問題、悪意のあるコードを検出するプロセスです。

開発者はコンテナ環境のセキュリティリスクを迅速に特定し、問題が発生する前に修正するための措置を講じることができるため、このプロセスは DevSecOps において重要です。

コンテナを定期的にスキャンすることで、組織は環境をセキュアかつ業界のベストプラクティスに準拠した状態に保ちながら、コンテナが提供する俊敏性とコストの利点を活用できます。

## レベル 0 - コンテナ脆弱性解析を実施するためのツールがない

このレベルでは、スキャンツールが存在せず、手遅れになるまで脆弱性が発見されない可能性があります。このレベルで運用している組織はサイバー攻撃の影響を受けやすく、業界標準への準拠を達成するのに苦労するでしょう。

## レベル 1 - オンデマンドスキャンを実行するツールを使用し、コンテナ脆弱性解析を実施している

オンデマンドスキャンでツールを使用すると、ある程度のセキュリティレベルを確保できますが、手動による介入が必要となり、脆弱性の検出に遅れが生じる可能性があります。このレベルは組織がセキュリティ問題を迅速に特定し対処するのに役立ちますが、継続的な保護を提供するには十分ではないかもしれません。


## レベル 2 - ビルドパイプラインにコンテナ脆弱性解析ツールを実装し、自動スキャンを実行し、ビルドのステータスをレポートしている

コンテナスキャンツールをビルドパイプラインに統合することで、セキュリティチェックが自動化され、開発プロセスの早い段階で脆弱性を検出できます。このレベルは組織が DevSecOps プラクティスを拡大し、ソフトウェア開発ライフサイクルにセキュリティが組み込まれることを確保します。

## レベル 3 - 発見された内容が自動的に一元管理された課題追跡システムに記録されており、ツールの有効性を定期的にレビューしている

このレベルでは、コンテナスキャンプロセスが自動化されているだけでなく、一元管理された課題追跡システムと統合され、セキュリティ問題の可視性が向上し、追跡が容易になります。スキャンツールの有効性を定期的にレビューすることで、組織はセキュリティ態勢を継続的に改善し、新たな脅威に先んじることができます。


# 注目すべきツール

⚠️ **免責事項**

OWASP の公式プロジェクトは別として、このセクションのツールはその実績のある機能のみに基づいて選択されており、DSOVS プロジェクトリーダーとそれらを保守する作成者やベンダーとの間には他の関係はありません。

注目すべきツールの提案がある場合には [💡 ツールを提案](https://github.com/OWASP/www-project-devsecops-verification-standard/discussions/categories/ideas) してください。

## [Trivy](https://github.com/aquasecurity/trivy)

Trivy はコンテナ、Kubernetes、コードリポジトリ、クラウドなどの脆弱性、設定ミス、シークレット、SBOM を検出するコンテナスキャンツールです。

<a href="https://github.com/aquasecurity/trivy-action"><img src="images/github.svg" width="20px"> GitHub Actions

```
name: build
on:
  push:
    branches:
      - master
  pull_request:
jobs:
  build:
    name: Build
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Build an image from Dockerfile
        run: |
          docker build -t docker.io/my-organization/my-app:${{ github.sha }} .
      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: 'docker.io/my-organization/my-app:${{ github.sha }}'
          format: 'table'
          exit-code: '1'
          ignore-unfixed: true
          vuln-type: 'os,library'
          severity: 'CRITICAL,HIGH'
```

<a href="https://aquasecurity.github.io/trivy/v0.18.3/integrations/gitlab-ci/"><img src="images/gitlab.svg" width="20px"> GitLab CI

```
Trivy_container_scanning:
  stage: test
  image:
    name: alpine:3.11
  variables:
    # Override the GIT_STRATEGY variable in your `.gitlab-ci.yml` file and set it to `fetch` if you want to provide a `clair-whitelist.yml`
    # file. See https://docs.gitlab.com/ee/user/application_security/container_scanning/index.html#overriding-the-container-scanning-template
    # for details
    GIT_STRATEGY: none
    IMAGE: "$CI_REGISTRY_IMAGE:$CI_COMMIT_SHA"
  allow_failure: true
  before_script:
    - export TRIVY_VERSION=${TRIVY_VERSION:-v0.19.2}
    - apk add --no-cache curl docker-cli
    - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD" $CI_REGISTRY
    - curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin ${TRIVY_VERSION}
    - curl -sSL -o /tmp/trivy-gitlab.tpl https://github.com/aquasecurity/trivy/raw/${TRIVY_VERSION}/contrib/gitlab.tpl
  script:
    - trivy --exit-code 0 --cache-dir .trivycache/ --no-progress --format template --template "@/tmp/trivy-gitlab.tpl" -o gl-container-scanning-report.json $IMAGE
  cache:
    paths:
      - .trivycache/
  artifacts:
    reports:
      container_scanning: gl-container-scanning-report.json
  dependencies: []
  only:
    refs:
      - branches
```

<a href="https://github.com/dvuln/devsecops/blob/test/containerscan/trivy-azure.yml"><img src="images/azure.svg" width="40px"> Azure DevOps </a>

```
trigger:
  - master

pool:
  vmImage: ubuntu-latest

parameters:
  - name: imageName
    displayName: Docker Image Name

steps:
  - script: |
      sudo apt-get install wget apt-transport-https gnupg lsb-release
      wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
      echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
      sudo apt-get update
      sudo apt-get install trivy
      trivy image  -f json --output '$(Build.ArtifactStagingDirectory)/trivy-result.json' ${{ parameters.imageName }}
    displayName: "Run Trivy"
```

## 🙏 クレジット

コミュニティへの素晴らしい貢献なしにはこれを実現できませんでした。使用された外部からのインスピレーションに感謝の意を表します。

* [Simar Singh](https://github.com/simar7)
* [Teppei Fukuda](https://github.com/knqyf263)
* [Yudhi Yudhistira](https://github.com/devsecurityops)
