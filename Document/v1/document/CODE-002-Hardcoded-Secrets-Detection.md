# ハードコードされたシークレットの検出 (Hardcoded Secrets Detection)

| ID             |
| -------------- |
| DSOVS-CODE-002 |

## 概要

ハードコードされたシークレットのスキャンは DevSecOps で使用されるセキュリティプロセスであり、ハードコードされたパスワード、トークン、その他の識別情報のコードなどをスキャンします。

ハードコードされたシークレットのスキャンの目的は、セキュアではなく保存されているクレデンシャルやシークレットを特定して置き換えることです。これらは悪意のあるアクターによって悪用される可能性があります。

このプロセスでは一般的にソースコード、構成ファイル、その他の関連するアーティファクトをスキャンしてシークレットを探し出し、適切なレベルのアクセスコントロールであることをチェックします。

セキュアではないと判断されたシークレットは関係者に報告され、よりセキュアな代替手段で置き換えます。

## レベル 0 - ハードコードされたシークレットのスキャンを実施するためのツールがない

このレベルでのセキュリティ成熟度では、シークレットスキャンを実行できるツールはありません。

## レベル 1 - オンデマンドスキャンを実行するツールを使用し、ソースコード内にハードコードされたシークレットを特定している

このステージでは、シークレット検出ツールが存在しますが、スキャンはケースバイケースで実行されます。自動化されておらず、結果は報告や記録されない場合があります。

## レベル 2 - ビルドパイプラインにハードコードされたシークレットのスキャンツールを実装し、自動スキャンを実行し、ビルドのステータスをレポートしている

ここでは、ソフトウェアビルドパイプラインにシークレットスキャンが実装されています。つまり、ビルドが実行されるたびに、自動シークレットスキャンがトリガーされ、結果が報告されます。

## レベル 3 - 発見された内容が自動的に一元管理された課題追跡システムに記録されており、ツールの有効性を定期的にレビューしている

シークレットスキャンのレベル 3 はレベル 2 と同じですが、特定されたすべてのセキュリティ脆弱性が一元管理された課題追跡システムに記録され、シークレット検出ツールの有効性を評価するために定期的にレビューされることが追加されています。つまり、同じタイプの自動スキャンが実行されていますが、将来の使用と改善のために結果が収集、追跡、分析されているのです。

# 注目すべきツール

⚠️ **免責事項**

OWASP の公式プロジェクトは別として、このセクションのツールはその実績のある機能のみに基づいて選択されており、DSOVS プロジェクトリーダーとそれらを保守する作成者やベンダーとの間には他の関係はありません。

注目すべきツールの提案がある場合には [💡 ツールを提案](https://github.com/OWASP/www-project-devsecops-verification-standard/discussions/categories/ideas) してください。

## [Gitleaks](https://github.com/awslabs/git-secrets)

Gitleaks は git リポジトリ内のパスワード、API キー、トークンなどのハードコードされたシークレットを検出および防止するための SAST ツールです。Gitleaks は過去や現在のコード内のシークレットを検出するための使いやすいオールインワンのソリューションです。

<a href="https://github.com/gitleaks/gitleaks-action"><img src="images/github.svg" width="20px"> GitHub Actions

```
name: gitleaks
on:
  pull_request:
  push:
  workflow_dispatch:
  schedule:
    - cron: "0 4 * * *" # run once a day at 4 AM
jobs:
  scan:
    name: gitleaks
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          GITLEAKS_LICENSE: ${{ secrets.GITLEAKS_LICENSE}} # Only requir
```

<a href="https://badshah.io/experiment/adding-gitleaks-to-gitlab-pipeline/"><img src="images/gitlab.svg" width="20px"> GitLab CI

```
stages:
  - secrets-detection

gitleaks:
  stage: secrets-detection
  image: 
    name: "zricethezav/gitleaks"
    entrypoint: [""]
  script: gitleaks -v --pretty --repo-path . --commit-from=$CI_COMMIT_SHA --commit-to=$CI_COMMIT_BEFORE_SHA --branch=$CI_COMMIT_BRANCH
```

<a href="https://github.com/JoostVoskuil/azure-devops-gitleaks"><img src="images/azure.svg" width="40px"> Azure DevOps </a>

```
name: '2.0$(rev:.r)'

trigger:
- main
- feature/*
- features/*
- bugfix/*

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: 'Build'
  displayName: 'Build'
  jobs:
  - job: 
    steps:
    - task: NodeTool@0
      inputs:
        versionSpec: '16.x'
      displayName: 'Install Node.js'
    
    - template: build-and-test.yml
      parameters:
        path: task/v2
        name: Gitleaks V2
  
    - task: TfxInstaller@3
      displayName: 'Use Node CLI for Azure DevOps'
      inputs:
        version: '0.9.x'
        checkLatest: true

    - task: PackageAzureDevOpsExtension@3
      displayName: 'Package Extension: $(Build.SourcesDirectory)'
      name: 'packageStep'
      inputs:
        rootFolder: '$(Build.SourcesDirectory)'
        outputPath: '$(Build.ArtifactStagingDirectory)/foxholenl-gitleaks.vsix'
        publisherId: 'foxholenl'
        extensionId: 'Gitleaks'
        extensionName: 'Gitleaks'
        extensionTag: '-build'
        extensionVersion: '$(Build.BuildNumber)'
        extensionVisibility: private

    - task: PublishPipelineArtifact@1
      displayName: 'Publish vsix'
      inputs:
        publishLocation: pipeline
        targetPath: '$(packageStep.Extension.OutputPath)'
        artifact: 'vsix'
      condition: succeededOrFailed()

- stage: Test
  displayName: 'Publish to Marketplace (private)'
  condition: and(succeeded(), ne(variables['Build.Reason'], 'PullRequest'))
  dependsOn: 'Build'
  jobs:
    - deployment: 
      environment: Test
      strategy: 
        runOnce:
         deploy:
          steps:

          - task: TfxInstaller@3
            displayName: 'Use Node CLI for Azure DevOps'
            inputs:
              version: '0.9.x'
              checkLatest: true

          - task: PublishAzureDevOpsExtension@3
            name: 'PublishTest'
            inputs:
              connectTo: 'VsTeam'
              connectedServiceName: 'Marketplace'
              fileType: 'vsix'
              vsixFile: '$(Pipeline.Workspace)/vsix/foxholenl-gitleaks.vsix'
              publisherId: 'foxholenl'
              extensionId: 'Gitleaks'
              extensionTag: '-dev'
              updateTasksVersion: false
              extensionVisibility: 'privatepreview'
              shareWith: 'foxholenl'
              noWaitValidation: true

- stage: Production
  displayName: 'Publish to Marketplace (Public)'
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
  dependsOn: 'Test'
  jobs:
    - deployment: 
      environment: Production
      strategy: 
        runOnce:
          deploy:
            steps:
            - task: TfxInstaller@3
              displayName: 'Use Node CLI for Azure DevOps'
              inputs:
                version: '0.9.x'
                checkLatest: true

            - task: PublishAzureDevOpsExtension@3
              name: 'PublishProd'
              inputs:
                connectTo: 'VsTeam'
                connectedServiceName: 'Marketplace'
                fileType: 'vsix'
                vsixFile: '$(Pipeline.Workspace)/vsix/foxholenl-gitleaks.vsix'
                publisherId: 'foxholenl'
                extensionId: 'Gitleaks'
                updateTasksVersion: false
                extensionVisibility: 'public'
                noWaitValidation:  true
```

## 🙏 クレジット

コミュニティへの素晴らしい貢献なしにはこれを実現できませんでした。使用された外部からのインスピレーションに感謝の意を表します。

* [Joost Voskuil](https://github.com/JoostVoskuil)
* [Chandrapal Badshah](https://www.linkedin.com/in/bnchandrapal/?originalSubdomain=in)
