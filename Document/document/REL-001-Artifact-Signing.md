# 成果物署名 (Artifact Signing)

| ID            |
| ------------- |
| DSOVS-REL-001 |

## 概要

成果物署名は開発者によってリリースされる成果物やバイナリの完全性を保証するセキュリティプロセスです。

これは成果物が改竄されておらず、悪意のあるコードが混入されていないことを確認するために、暗号化およびデジタル署名技術を使用して行われます。

組織は本番環境にデプロイする前にソフトウェアやアプリケーションの信頼性を迅速かつ簡単に検証できるため、成果物署名は DevSecOps にとって重要です。最近ではサプライチェーンセキュリティ攻撃によりコード署名が人気を博し、パイプラインを構築するためのセキュリティを適用する方法の一つとして使用されています。

また、アプリケーションがセキュアで信頼できるものであることを保証する手段を提供し、顧客の信頼とロイヤルティを構築するのに役立ちます。

## レベル 0 - パッケージやコードの署名プロセスを定めていない

このレベルでは、ソフトウェア成果物はデジタル署名されていないため、認可されていないコードアクセスに対して脆弱なままです。ソフトウェアを後押しする監査可能性や完全性の保証はありません。このレベルで運用している組織は重大なセキュリティリスクに直面し、コードの真正性を検証する手段がありません。

## レベル 1 - 自己管理鍵での基本的なコード署名

このステージでは、ソフトウェア成果物は署名されますが、ツールやプロセスは断片化されています。開発者は自分自身の秘密鍵を一元管理せずに扱う可能性があり、鍵の誤用や侵害につながる可能性があります。ある程度のセキュリティは導入されますが、包括的なコードの完全性、真正性、改竄不可能性を確保するには不十分であり、改ざん防止にはなりません。

## レベル 2 - 鍵セキュリティを強化して一元管理されたコード署名

レベル 2 にはコード署名ポリシー、ワークフロー、監査可能性のための一元管理されたプラットフォームの使用を含みます。また、安全なハードウェアセキュリティモジュール (HSM) での機密性の高い署名鍵の保護を重要視しています。しかし、このステージでは、コード署名はまだ CI/CD プロセスやワークフローと完全に統合されておらず、すべてのユースケースがカバーされているわけではありません。このレベルではセキュリティが向上していますが、DevSecOps に必要な完全な自動化と統合はまだ欠落しています。一般的にこのレベルでは、組織は AWS KMS や HashiCorp Vault などの鍵管理ソリューションを活用します。

## レベル 3 - 完全に CI/CD に統合されたコード署名とガバナンス

このコード署名成熟度モデルの最高レベルでは、組織は CI/CD プロセスにコード署名の完全な統合を達成しています。これは、すべてのコンテナ、アーティファクト、ソフトウェア成果物が署名されていることを意味します。この実装はネイティブの署名ツールとワークフローとシームレスに統合され、すべての署名プロセスに対する完全な監査可能性とガバナンスを確保します。このレベルでは最高レベルのセキュリティ、コードの完全性、真正性を提供し、最新の DevSecOps プラクティスの要求を満たします。一般的にこのレベルでは、組織はキーレス署名 (有効期間の長い署名鍵を扱わない新しい署名技法) を採用します。

# 注目すべきツール

⚠️ **免責事項**

OWASP の公式プロジェクトは別として、このセクションのツールはその実績のある機能のみに基づいて選択されており、DSOVS プロジェクトリーダーとそれらを保守する作成者やベンダーとの間には他の関係はありません。

注目すべきツールの提案がある場合には [💡 ツールを提案](https://github.com/OWASP/www-project-devsecops-verification-standard/discussions/categories/ideas) してください。

## [cosign](https://github.com/sigstore/cosign)

cosign は、コンテナイメージや BLOB ファイル (つまり、.zip ファイルにバンドルされた AWS Lambda コードやさまざまなタイプのソフトウェアアーティファクト) などのソフトウェアアーティファクトに署名するためのオープンソースの CLI ユーティリティです。


<a href="https://aquasecurity.github.io/trivy/v0.18.3/integrations/gitlab-ci/"><img src="images/gitlab.svg" width="20px"> GitLab CI

```
container_scan:
  stage: devsecops 
  script:
    - trivy image --scanners vuln $IMAGE_NAME --format cyclonedx  > trivy-output-$DATE-cyclonedx.json
  artifacts:
    when: always 
    paths:
      - trivy-output-$DATE-cyclonedx.json

generate_sbom:
  stage: devsecops
  script:
    - syft $IMAGE_NAME -o cyclonedx-json  > sbom-$DATE.syft.json
  artifacts:
    when: always 
    paths:
        - sbom-$DATE.syft.json

signing_and_attestation: 
  stage: publish
  id_tokens:
    SIGSTORE_ID_TOKEN:
      aud: sigstore
  variables:
    RUNNER_GENERATE_ARTIFACTS_METADATA: "true"
  script: 
    - IMAGE_DIGEST=`docker inspect --format='{{index .RepoDigests 0}}' $IMAGE_NAME` # Grab image digest, rather than image tag 
    - cosign sign $IMAGE_DIGEST --key $COSIGN_KEY_NAME # Sign the container image 
    - cosign attest --key $COSIGN_KEY_NAME  --type vuln --predicate trivy-output-$DATE-cyclonedx.json $OCI_IMAGE_DIGEST # Sign and create an attestation for our Trivy scan 
    - cosign attest --key $COSIGN_KEY_NAME  --type cyclonedx --predicate sbom-$DATE.syft.json $OCI_IMAGE_DIGEST # Sign and create an attestation for our SBOM 
  needs: 
    - devsecops
  artifacts:
    when: always 
    paths:
      - "artifacts*.json"
```

<a href="https://github.com/aquasecurity/trivy-action"><img src="images/github.svg" width="20px"> GitHub Actions

```
jobs:
  build-image:
    runs-on: ubuntu-latest

    permissions:
      contents: read
      packages: write
      id-token: write # needed for signing the images with GitHub OIDC Token

    name: build-image
    steps:
      - uses: actions/checkout@v3.5.2
        with:
          fetch-depth: 1

      - name: Install Cosign
        uses: sigstore/cosign-installer@v3.1.1

      - name: Set up QEMU
        uses: docker/setup-qemu-action@v2.1.0

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2.5.0

      - name: Login to GitHub Container Registry
        uses: docker/login-action@v2.1.0
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - id: docker_meta
        uses: docker/metadata-action@v4.4.0
        with:
          images: ghcr.io/sigstore/sample-honk
          tags: type=sha,format=long

      - name: Build and Push container images
        uses: docker/build-push-action@v4.0.0
        id: build-and-push
        with:
          platforms: linux/amd64,linux/arm/v7,linux/arm64
          push: true
          tags: ${{ steps.docker_meta.outputs.tags }}

      # https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions#using-an-intermediate-environment-variable
      - name: Sign image with a key
        run: |
          cosign sign --yes --key env://COSIGN_PRIVATE_KEY "${TAGS}@${DIGEST}"
        env:
          TAGS: ${{ steps.docker_meta.outputs.tags }}
          COSIGN_PRIVATE_KEY: ${{ secrets.COSIGN_PRIVATE_KEY }}
          COSIGN_PASSWORD: ${{ secrets.COSIGN_PASSWORD }}
          DIGEST: ${{ steps.build-and-push.outputs.digest }}

      - name: Sign the images with GitHub OIDC Token
        env:
          DIGEST: ${{ steps.build-and-push.outputs.digest }}
          TAGS: ${{ steps.docker_meta.outputs.tags }}
        run: cosign sign --yes "${TAGS}@${DIGEST}"

```

## 参考情報

- GHA from: https://github.com/marketplace/actions/cosign-installer 
