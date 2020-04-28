# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.6.1] - 2020-04-13
### Changed
- Updated monolog dependency to allow newer versions to be downloaded in update
- Added `composer.lock` into `.gitignore` file.

## [1.6.0] - 2020-03-05
### Breaking Changes
To prevent ordered arguments and increasing use-cases, we are moving all optional arguments into a combined argument(Associative Array).

- customVariables argument in APIs: `activate`, `getVariation`, `track`, `isFeatureEnabled`, and `getFeatureVariableValue` have been moved into `options`.
- `revenueValue` parameter in `track` API is now moved into `options` argument.

#### Before

```php
// activae API
$vwoClient->activate($campaignKey, $userId, $customVariables);
// getVariation API
$vwoClient->getVariation($campaignKey, $userId, $customVariables);
// track API
$vwoClient->track($campaignKey, $userId, $goalIdentifier, $revenueValue, $customVariables);
// isFeatureEnabled API
$vwoClient->isFeatureEnabled($campaignKey, $userId, $customVariables);
// getFeatureVariableValue API
$vwoClient->getFeatureVariableValue($campaignKey, $variableKey, $userId, $customVariables);
```

#### After

```php

$options = [];
$options["customVariables"] = [];
  // Optional, neeeded for Forced Variation
$options["variationTargetingVariables"] = [];

// activae API
$vwoClient->activate($campaignKey, $userId, $options);
// getVariation API
$vwoClient->getVariation($campaignKey, $userId, $options);
// track API
  // Optional, needed to track revenue goal with revenue value
$options["revenueValue"] = 1000.12;
$vwoClient->track($campaignKey, $userId, $goalIdentifier, options);
// isFeatureEnabled API
$vwoClient->isFeatureEnabled($campaignKey, $userId, $options);
// getFeatureVariableValue API
$vwoClient->getFeatureVariableValue($campaignKey, $variableKey, $userId, $options);
```

### Added
Forced Variation capabilites
- Introduced `Forced Variation` to force certain users into specific variation. Forcing can be based on User IDs or custom variables defined.
### Changed
- All existing APIs to handle variation-targeting-variables as an option for forcing variation
- Code refactored to support Whitelisting.

## [1.5.2] - 2020-01-24
### Changed
- Update endpoint to use `https` protocol instead of `http`
- Update UserStorage `set` function to properly validate user-data structure before setting

## [1.5.1] - 2020-01-23
### Changed
- Move "squizlabs/php_codesniffer" from dependencies to dev-dependencies in `composer.json`
- Add `.gitattributes` file for smaller downloads i.e. only required files and folders when downloaded

## [1.5.0] - 2019-12-17
### Added
- Feature Rollout and Feature Test capabilities
- Pre and Post segmentation capabilites
  Introduced new Segmentation service to evaluate whether user is eligible for campaign based on campaign pre-segmentation conditions and passed custom-variables
### Changed
- Existing APIs to handle new type of campaigns i.e. feature-rollout and feature-test
- All existing APIs to handle custom-variables for tageting audience
- Code refactored to support feature-rollout, feature-test, campaign tageting and post segmentation

## [1.3.0] - 2019-11-21
### Changed
- Change MIT License to Apache-2.0
- Added apache copyright-header in each file
- Add NOTICE.txt file complying with Apache LICENSE
- Give attribution to the third-party libraries being used and mention StackOverflow

## [1.0.4] - 2019-11-01
### Changed
- Fix: Update schema validation when no campaigns are running

## [1.0.3] - 2019-10-13
### Changed
- Fix: show error log if goal is revenue type but no revenue value is passed in `track` API

## [1.0.2] - 2019-08-12
### Added
- Added more unit test cases
### Changed
- Update params that are sent to VWO server when track API is used

## [1.0.1] - 2019-07-32
### Changed
- Added `.travis.yml` file for running automated test cases on supported PHP versions

## [1.0.0] - 2019-07-30
### Added
- First release with Server-side A/B capabilities