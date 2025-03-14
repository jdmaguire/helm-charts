# Fluentd Aggregator Helm Chart Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

<!-- ## [vX.Y.Z] - UNRELEASED
### Highlights
### All Changes
- Added
- Updated
- Changed
- Fixed
- Deprecated
- Removed -->

## [v3.6.0] - 2023-01-10

### All Changes

- Updated _Fluentd Aggregator_ OCI image to [v2.6.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.6.0) (_Fluentd_ [v1.15.3](https://github.com/fluent/fluentd/releases/tag/v1.15.3)).
- Changed liveness probe to start later and be less sensitive.
- Changed readiness probe to start later and be less sensitive.

## [v3.5.0] - 2022-12-06

### All Changes

- Updated _Fluentd Aggregator_ OCI image to [v2.5.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.5.0) (_Fluentd_ [v1.15.3](https://github.com/fluent/fluentd/releases/tag/v1.15.3)).

## [v3.4.2] - 2022-11-28

### All Changes

- Fixed internal labelling pattern to work correctly.
- Fixed `ServiceMonitor` port.
- Moved debug filter to above global filters.

## [v3.4.1] - 2022-11-28

### All Changes

- Fixed route copy bug.

## [v3.4.0] - 2022-11-28

### All Changes

- Updated _Fluentd Aggregator_ OCI image to [v2.4.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.4.0) (_Fluentd_ [v1.15.3](https://github.com/fluent/fluentd/releases/tag/v1.15.3)).
- Fixed missing use of `configuration.system.rootDir` to set the mount path; this means that the buffer paths can be kept as `/fluentd/buffers` when migrating from `v2`.
- Fixed bug in creating dashboards.
- Fixed missing service annotations in template.

## [v3.3.0] - 2022-11-15

### All Changes

- Updated _Fluentd Aggregator_ OCI image to [v2.3.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.3.0) (_Fluentd_ [v1.15.3](https://github.com/fluent/fluentd/releases/tag/v1.15.3)).

## [v3.2.0] - 2022-11-02

### All Changes

- Updated _Fluentd Aggregator_ OCI image to [v2.2.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.2.0) (_Fluentd_ [v1.15.3](https://github.com/fluent/fluentd/releases/tag/v1.15.3)).

## [v3.1.0] - 2022-11-02

### All Changes

- Updated _Fluentd Aggregator_ OCI image to [v2.1.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.1.0) (_Fluentd_ [v1.15.2](https://github.com/fluent/fluentd/releases/tag/v1.15.2)).

## [v3.0.2] - 2022-10-12

### All Changes

- Added a new `serviceAccount.labels` value to add labels to the `ServiceAccount`.

## [v3.0.1] - 2022-10-12

### All Changes

- Added support for setting an IPv6 bind address.

## [v3.0.0] - 2022-10-06

### Highlights

> **Info**
> This release contains a number of breaking changes, please check out the full list of changes for the values which have been removed as well as taking note that the root directory mounted to the `PersistentVolume` has changed so buffer paths will need to be changed accordingly.

This release introduces a new strongly typed configuration mode which isn't compatible with the previous `v2` versions as well as updating the Fluentd image and adding new capabilities to the chart.

#### Structured Configuration

The Fluentd configuration is now much more structured to make it much harder to break chart functionality while configuring Fluentd. This change starts with the replacement of `config` with `configuration` and is founded on the new `routes` sub-value which is used to set up message routing in a strongly typed way. This design reduces the raw Fluentd configuration inputs to the `filters` value for global filters and the nested `config` value for each route.

### All Changes

- Updated _Fluentd Aggregator_ Docker image to [v2.0.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v2.0.0) (_Fluentd_ [v1.15.2](https://github.com/fluent/fluentd/releases/tag/v1.15.2)).
- Added explicit namespace declaration in templates.
- Added `imagePullSecrets` value.
- Added `serviceAccount.automountToken` to default token binding to `false`.
- Added `service.clusterIP` to enable making the `Service` headless.
- Added `serviceMonitor` value to replace `metrics.serviceMonitor`.
- Added `topologySpreadConstraints` value.
- Added `persistence.legacy` value to support migrating from `v2` chart versions.
- Added `configuration` value to support a strongly typed configuration pattern.
- Changed `PersistentVolume` mount point to `/fluentd/state`; use this path for buffers.
- Removed `image.pullSecrets` as they've been replaced by `imagePullSecrets`.
- Removed `service.ports` value as the ports are now part of the `configuration` value.
- Removed `metrics` value, see `serviceMonitor` and `configuration.metrics`.
- Removed `debug` value as it's been replaced by `configuration.debug`.
- Removed `config` value as configuration is now handled via the more strongly typed `configuration` value.

## [v2.7.1] - 2022-05-03

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.10](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.10) (_Fluentd_ [v1.14.6](https://github.com/fluent/fluentd/releases/tag/v1.14.6)).

## [v2.7.0] - 2022-04-01

### Added

- Added `commonLabels` to allow the addition of labels to all resources.
- Added `metrics.serviceMonitor.endpointConfig` to allow customisation of the `ServiceMonitor` endpoint.
- Added `extraVolumes` and `extraVolumeMounts`.

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.9](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.9) (_Fluentd_ [v1.14.6](https://github.com/fluent/fluentd/releases/tag/v1.14.6)).

### Deprecated

- Deprecated `metrics.serviceMonitor.interval` in favour of `metrics.serviceMonitor.endpointConfig.interval`.

### Removed

- Removed chart default for `metrics.serviceMonitor.interval`, the interval should be the _Prometheus_ default if not overridden.

## [v2.6.9] - 2022-02-10

### Added

- Added `arm64` support as the `stevehipwell/fluentd-aggregator` image is now multi-arch.

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.8](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.8) (_Fluentd_ [v1.14.5](https://github.com/fluent/fluentd/releases/tag/v1.14.5)).

## [v2.6.8] - 2022-01-21

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.6](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.6) (_Fluentd_ `v1.14.4`).

## [v2.6.7] - 2022-01-07

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.5](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.5) (_Fluentd_ `v1.14.4`).

## [v2.6.6] - 2021-11-29

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.4](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.4) (_Fluentd_ `v1.14.3`).

## [v2.6.5] - 2021-11-11

### Changed

- Move debug config after filters config so filters can be debugged.

## [v2.6.4] - 2021-10-29

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.3](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.3) (_Fluentd_ `v1.14.2`).

## [v2.6.3] - 2021-10-28

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.2](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.2) (_Fluentd_ `v1.14.1`) to support _OpenSearch_.

## [v2.6.2] - 2021-10-04

### Changed

- Bump version.

## [v2.6.1] - 2021-10-04

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.1](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.1) (_Fluentd_ `v1.14.1`).

## [v2.6.0] - 2021-08-31

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.14.0](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.14.0) (_Fluentd_ `v1.14.0`).
- Use the `policy/v1` API for `PodDisruptionBudget` if the K8s version supports it.

## [v2.5.3] - 2021-08-11

### Changed

- Improved documentation.

## [v2.5.2] - 2021-07-27

### Changed

- Update _Fluentd Aggregator_ Docker image to [v1.13.3](https://github.com/stevehipwell/fluentd-aggregator/releases/tag/v1.13.3) (_Fluentd_ `v1.13.3`)

## [v2.5.1] - 2021-07-13

### Changed

- Update _Fluentd Aggregator_ Docker image to `v1.13.2` (_Fluentd_ `v1.13.2`)

## [v2.5.0] - 2021-06-24

### Changed

- Update _Fluentd Aggregator_ Docker image to `v1.13.1` (_Fluentd_ `v1.13.1`)
- Add _PodDisruptionBudget_ support

## [v2.4.0] - 2021-06-24

### Changed

- Update _Fluentd Aggregator_ Docker image to `v1.13.0` (_Fluentd_ `v1.13.0`)

## [v2.3.1] - 2021-06-17

### Changed

- Fix notes if ingress is enabled

## [v2.3.0] - 2021-06-16

### Changed

- Update _Fluentd_ Docker image to `v1.12.5` (_Fluentd_ `v1.12.4`)
- Modify how ports are defined
- Support K8s v1.18 ingress changes

## [v2.2.0] - 2021-05-19

### Changed

- Upgrade _Fluentd_ Docker image to `v1.12.4` (_Fluentd_ `v1.12.3`)

## [v2.1.1] - 2021-05-11

### Changed

- Upgrade _Fluentd_ Docker image to `v1.12.3` (_Fluentd_ `v1.12.2`)

## [v2.1.1] - 2021-04-23

### Changed

- Fixed default routing implementation

## [v2.1.0] - 2021-04-22

### Changed

- Added separate route config via `config.route`

## [v2.0.0] - 2021-04-06

### Changed

- Upgraded to _Fluentd_ `v1.12.2`
- Removed `@mainstream` label from default input

## [v1.2.1] - 2021-04-06

### Added

- Support `podLabels` configuration value

## [v1.2.0] - 2021-04-06

### Added

- _Grafana_ dashboard
- _Prometheus_ input metrics

### Changed

- Hide metrics and health check logs

## [v1.1.3] - 2021-03-31

### Changed

- Update default config

## [v1.1.2] - 2021-03-31

### Changed

- Update default config

## [v1.1.1] - 2021-03-31

### Changed

- Update default config

## [v1.1.0] - 2021-03-30

### Changed

- Upgraded _Fluentd Aggregator_ image to `v1.11.5`

## [v1.0.5] - 2021-02-16

### Changed

- Fix host label for metrics

## [v1.0.4] - 2021-01-27

### Changed

- Updated default config

## [v1.0.3] - 2021-01-20

### Changed

- Fix metrics port in config

## [v1.0.2] - 2021-01-15

### Added

- Dynamic probe configuration

## [v1.0.1] - 2021-01-07

### Changed

- Use `fsGroup: 2000`

## [v1.0.0] - 2021-01-06

### Added

- Initial release
