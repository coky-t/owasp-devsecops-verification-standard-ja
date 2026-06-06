# コンプライアンススキャン (Compliance Scanning)

| ID            |
| ------------- |
| DSOVS-REL-007 |

## 概要

コンプライアンススキャンはシステムソフトウェアやアプリケーションをスキャンして、特定の標準や規制に準拠していることを確認するプロセスです。開発者はコードに潜在するコンプライアンスの問題を迅速に特定し、問題になる前に対処できるため、DevSecOps の重要な部分です。

また、コンプライアンススキャンを通じて、開発者は攻撃者によって悪用される可能性のあるセキュリティ脆弱性がないかコードを調べることもできます。

コンプライアンススキャンは最終的に開発、テスト、本運用ステージでアプリケーションやシステムの全体的なセキュリティと信頼性を向上させるのに役立ちます。

## レベル 0 - コンプライアンスチェックを実施するためのツールがない

At this level the organisation has no tooling or defined process for checking systems, hosts, or deployments against compliance benchmarks. Any assessment of whether infrastructure aligns with standards such as CIS Benchmarks, PCI DSS, or internal hardening baselines is carried out manually, if at all, and the results are neither consistent nor repeatable.

Without an automated compliance check, drift from a secure baseline goes unnoticed, misconfigurations accumulate over time, and the organisation cannot demonstrate to auditors or stakeholders that its environments meet the required controls.

## レベル 1 - オンデマンドスキャンを実行するツールを使用し、セキュリティコンプライアンスチェックを実施している

At this stage a compliance scanning tool has been adopted and is run on demand against systems or deployments to evaluate them against a chosen benchmark. An engineer might, for example, execute Chef InSpec, OpenSCAP, or a cloud posture scanner such as Prowler against a host or account and review the resulting report.

Because the scans are triggered manually and on a case-by-case basis, coverage is uneven and results may not be retained or acted upon in a structured way. The capability nonetheless gives teams a concrete, tool-backed view of their compliance posture at a point in time.

```mermaid
graph LR; Engineer-- on-demand scan -->System-- evaluated against -->Benchmark-Check-- results -->Report;
```

## レベル 2 - コンプライアンススキャンツールをスケジュールし、自動スキャンを実行し、一元管理された課題追跡システムを通じてシステム所有者にステータスをレポートしている

At this level compliance scanning is automated and integrated into the delivery pipeline or run on a regular schedule, so every relevant build or environment is assessed without human intervention. The scan executes as a pipeline stage or scheduled job and its pass or fail status is reported back automatically.

Findings are routed to the responsible system owner through a centralised issue tracking system, ensuring that compliance gaps are captured, assigned, and tracked through to resolution rather than being lost in ad-hoc reports. This gives the organisation continuous, consistent visibility of its compliance state across all in-scope systems.

```mermaid
graph LR; CICD-Pipeline-- automated scan -->System-- evaluated against -->Benchmark-Check-- results -->Issue-Tracker;
```

## レベル 3 - 脆弱性が特定された時点で自動修復を自動的に適用するメカニズムが存在する

At the highest level the organisation not only detects compliance violations automatically but also remediates them. When a scan identifies a deviation from the benchmark, an automated remediation mechanism, such as a configuration-management playbook, policy-as-code controller, or remediation pipeline, brings the affected system back into a compliant state without manual effort.

Compliance results and remediation actions are centrally tracked and measured, and the effectiveness of the benchmarks, scanning rules, and remediation logic is reviewed periodically and continuously improved. This closes the loop between detection and correction, keeping environments aligned with the required standards over time.

```mermaid
graph LR; CICD-Pipeline-- automated scan -->System-- evaluated against -->Benchmark-Check-- results -->Central-Tracker-- auto remediate -->System; Central-Tracker-- periodic review -->Continuous-Improvement;
```

# Notable Tools 

⚠️ **Disclaimer**

Apart from official OWASP Projects, the tools in this section have been chosen on the basis of their proven capabilities alone and there is no other relationship between the DSOVS project leaders and the creators or vendors who maintain them. 

If you have a suggestion for a notable tool please [💡 Suggest a Tool](https://github.com/OWASP/www-project-devsecops-verification-standard/discussions/categories/ideas) 

## [Chef InSpec](https://github.com/inspec/inspec)

Chef InSpec is an open source framework for describing compliance and security requirements as human-readable code. Controls can be run against servers, containers, and cloud resources to test them against benchmarks such as the CIS Benchmarks, and the same profiles can be executed locally or from a pipeline.

<a href="https://github.com/inspec/inspec"><img src="images/github.svg" width="20px"> GitHub Actions

```
name: compliance-scan
on:
  push:
  workflow_dispatch:
jobs:
  inspec:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install InSpec
        run: curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P inspec
      - name: Run CIS compliance profile
        run: |
          inspec exec https://github.com/dev-sec/linux-baseline \
            --chef-license accept-silent \
            --reporter cli json:inspec-report.json
      - name: Upload report
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: inspec-report
          path: inspec-report.json
```

## [OpenSCAP](https://github.com/OpenSCAP/openscap)

OpenSCAP is an open source implementation of the Security Content Automation Protocol (SCAP). Using the `oscap` command line tool together with SCAP Security Guide content, it evaluates a host against standardised profiles (for example a PCI DSS or CIS profile) and can generate both machine-readable results and an HTML report.

```
# Evaluate the host against the PCI-DSS profile from the SCAP Security Guide
oscap xccdf eval \
  --profile xccdf_org.ssgproject.content_profile_pci-dss \
  --results scan-results.xml \
  --report scan-report.html \
  /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml
```

## [Prowler](https://github.com/prowler-cloud/prowler)

Prowler is an open source security and compliance tool for cloud environments such as AWS, Azure, Google Cloud, and Kubernetes. It ships with checks mapped to frameworks including CIS, PCI DSS, and others, making it well suited to automated cloud compliance scanning in a pipeline.

```
# Scan an AWS account against the CIS benchmark and emit JSON + HTML output
prowler aws \
  --compliance cis_2.0_aws \
  --output-formats json-ocsf html \
  --output-directory ./prowler-output
```
