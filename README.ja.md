`package_info_plus` を Riverpod から使用するためのプロバイダーを提供するパッケージです。アプリケーションの基本情報（アプリ名、パッケージ名、バージョン等）を同期的に Riverpod 経由で取得することが可能です。

## Features

- アプリケーションの基本情報を Riverpod の Provider として提供
- アプリ名、パッケージ名、バージョン、ビルド番号、ビルド署名、インストーラーストア情報へのアクセス
- アプリケーションのインストール時刻・更新時刻へのアクセス
- 非同期初期化による依存注入サポート
- 既存の `PackageInfo` オブジェクトからの Provider 生成

## Getting started

このパッケージは内部依存です。使用するには、対象パッケージの `pubspec.yaml` に以下の依存関係を追加してください：

```yaml
dependencies:
  package_info_plus_riverpod: ^1.1.0
```

## Usage

以下のようにしてアプリケーション情報を取得できます：

```dart
// 非同期で依存を解決
ainal overrides = await PackageInfoPlusProviders.inject();

// ProviderScope で Override を適用
ProviderScope(
  overrides: overrides,
  child: MyApp(),
)

// Consumer で各プロパティを使用
Consumer(
  builder: (context, ref, child) {
    final appName = ref.watch(PackageInfoPlusProviders.appName);
    final version = ref.watch(PackageInfoPlusProviders.version);
    final packageName = ref.watch(PackageInfoPlusProviders.packageName);
    final installTime = ref.watch(PackageInfoPlusProviders.installTime);
    final updateTime = ref.watch(PackageInfoPlusProviders.updateTime);

    return Text('$appName v$version ($packageName)');
  },
)
```

## Additional information

このパッケージは `flutter_armyknife` プロジェクトの一部として開発されており、Flutter アプリケーションでの Riverpod を使用した状態管理を支援します。

利用可能な Provider：

- `appName`: アプリケーション名
- `packageName`: パッケージ名
- `version`: バージョン
- `buildNumber`: ビルド番号
- `buildSignature`: ビルド署名
- `installerStore`: インストーラーストア情報
- `installTime`: アプリケーションのインストール時刻
- `updateTime`: アプリケーションの最終更新時刻
