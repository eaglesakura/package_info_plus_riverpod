A package that provides providers for using `package_info_plus` with Riverpod. This package enables synchronous access to basic application information (app name, package name, version, etc.) through Riverpod.

## Features

- Provides basic application information as Riverpod Providers
- Access to app name, package name, version, build number, build signature, and installer store information
- Access to application installation time and update time
- Dependency injection support through asynchronous initialization
- Provider generation from existing `PackageInfo` objects

## Getting started

This is an internal dependency package. To use it, add the following dependency to your target package's `pubspec.yaml`:

```yaml
dependencies:
  package_info_plus_riverpod: ^1.1.0
```

## Usage

You can retrieve application information as follows:

```dart
// Resolve dependencies asynchronously
final overrides = await PackageInfoPlusProviders.inject();

// Apply overrides with ProviderScope
ProviderScope(
  overrides: overrides,
  child: MyApp(),
)

// Use each property with Consumer
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

This package is developed as part of the `flutter_armyknife` project and supports state management using Riverpod in Flutter applications.

Available Providers:

- `appName`: Application name
- `packageName`: Package name
- `version`: Version
- `buildNumber`: Build number
- `buildSignature`: Build signature
- `installerStore`: Installer store information
- `installTime`: Application installation time
- `updateTime`: Application last update time
