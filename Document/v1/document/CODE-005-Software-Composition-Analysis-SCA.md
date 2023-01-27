# ソフトウェアコンポジション解析 (Software Composition Analysis, SCA)

| ID             |
| -------------- |
| DSOVS-CODE-005 |

## 概要

ソースコンポジション解析 (Source Composition Analysis, SCA) はソースコードをスキャンし、アプリケーションで使用されているライブラリ、依存関係、およびその他のサードパーティコンポーネントを特定するセキュリティテクノロジです。

アプリケーションのすべてのコンポーネントがセキュアかつ最新であることを保証するのに役立つため、DevSecOps の重要な部分となっています。

既知の脆弱性や古いバージョンのコードを検出することで、サードパーティコンポーネントが使用されている場合でも、SCA はアプリケーションがセキュアであり続けることを確保するのに役立ちます。

さらに、SCA は開発者に新しいバージョンのコードを知らせることができるため、開発者はそれに応じてアプリケーションを更新できます。

これにより最新のセキュリティパッチやアップデートが確実に適用され、アプリケーションのセキュリティをさらに向上できます。

## レベル 0 - サードパーティ依存関係解析を実施するためのツールがない

lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

## レベル 1 - オンデマンドスキャンを実行するツールを使用し、アプリケーションで使用されている古いまたはセキュアでないサードパーティコンポーネントを特定している

lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

## レベル 2 - ビルドパイプラインにサードパーティコンポーネント脆弱性のスキャンツールを実装し、自動スキャンを実行し、ビルドのステータスをレポートしている

lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

## レベル 3 - 発見された内容が自動的に一元管理された課題追跡システムに記録されており、ツールの有効性を定期的にレビューしている

lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

## 参考情報
