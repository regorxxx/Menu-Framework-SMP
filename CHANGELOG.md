# Changelog

## [Table of Contents]
- [Unreleased](#unreleased)
- [1.1.0](#110---2021-05-19)
- [1.0.0](#100---2021-05-05)

## [Unreleased][]
### Added
### Changed
### Removed

## [1.1.0] - 2021-05-19
### Added
- New examples.
- Allows calling a forced menu entry routine even without using mouse tracking. If it fails, logs to console. btn_up(x, y, \[object\], forcedEntry).
- Multiple menu concatenation using btn_up(x, y, \[object\], forcedEntry), where \[object\] may be another menu object or an array of menus. It should allow sharing the same menu code in multiple scripts easily (or optional menus).
### Changed
- Moved dependencies to main file.
### Removed
- helpers_xxx.js dependency.

## [1.0.0] - 2021-05-05
### Added
- First release.

### Changed

### Removed

[Unreleased]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/1f1ae22...v1.0.0
