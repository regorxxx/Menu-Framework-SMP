# Changelog

## [Table of Contents]
- [Unreleased](#unreleased)
- [1.1.0](#110---2021-05-19)
- [1.0.0](#100---2021-05-05)

## [Unreleased][]
### Added
### Changed
- This.newCheckMenu(menuName, entryTextA, entryTextB, idxFun) translates into CheckMenuItem(entryTextA, idxFun) when entryTextB is undefined and into CheckMenuRadioItem(entryTextA, entryTextB, idxFun) when both are defined, thus allowing both checking behaviour in the framework. (previously only the second one was allowed). Any checkMenu added with previous versions works without changes.
### Removed
### Fixed
- Check menus ids not being updated if entries are removed/added on every call. Now entry/menu arrays are cleared on every call (not only the entry list), which should prevent any possible error at other points too.

## [1.1.0] - 2021-05-19
### Added
- New examples.
- Allows calling a forced menu entry routine even without using mouse tracking. If it fails, logs to console. btn_up(x, y, \[object\], forcedEntry).
- Multiple menu concatenation using btn_up(x, y, \[object\], forcedEntry), where \[object\] may be another menu object or an array of menus. It should allow sharing the same menu code in multiple scripts easily (or optional menus).
### Changed
- Moved dependencies to main file.
### Removed
- helpers_xxx.js dependency.
### Fixed

## [1.0.0] - 2021-05-05
### Added
- First release.
### Changed
### Removed
### Fixed

[Unreleased]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/1f1ae22...v1.0.0
