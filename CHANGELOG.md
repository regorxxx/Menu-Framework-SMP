# Changelog

## [Table of Contents]
- [Unreleased](#unreleased)
- [1.2.2](#122---2021-06-07)
- [1.2.1](#121---2021-05-28)
- [1.2.0](#120---2021-05-26)
- [1.1.0](#110---2021-05-19)
- [1.0.0](#100---2021-05-05)

## [Unreleased][]
### Added
- Menu framework: added bool variable (bExecute) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0) which allows to simulate the menu without executing any related entry function. 
- Menu framework: added func variable (replaceFunc) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0) which allows to replace the related entry function with a custom one, whenever bExecute is also false. Can be used to paste to clipboard entry names easily simulating the menu usage.
- Menu framework: added flag variable (flag) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0) which allows to set SMP TrackPopupMenu's flag.
### Changed
- Menu framework: .initMenu and .btn_up are now 2 separate functions. i.e. the menu can be recreated without having to create the UI elements using .initMenu instead of .btn_up (which also calls .initMenu).
### Removed
### Fixed
- Menu framework: '&' char not showing (or making next char underscored) on created dynamic menus (when it was part of a playlist name for ex.), since they were not doubled. Now the framework automatically checks for names with '&' and doubles them ('&&' are skipped), so they are displayed right.

## [1.2.2] - 2021-06-07
### Added
### Changed
- 'entryMap' now stores menu names with anything after tabs '\t' stripped. i.e. you can add extra variable info tabbed to the right (like shortcuts) to the menu names without it being reflected on .lastCall. Makes easier to work with macros or shortcuts, since changing that part of the string will still output the same "entry name". menu.btn_up(void(0), void(0), void(0), 'Playlist History\\Previous playlist') and menu.btn_up(void(0), void(0), void(0), 'Playlist History\\Previous playlist\tCtrl + R') would be equivalent.
### Removed
- helpers_xxx.js file.
### Fixed

## [1.2.1] - 2021-05-28
### Added
- This.getMenus() returns the entire list of menus attached to the menu instance (useful to swith menus on/off on demand).
- This.lastCall is sent to console on every menu call.
### Changed
- Macros: This.lastCall now omits ('main\' or the main menu name) when the entry resides on the main menu. i.e. just use the entry name for main menu entries, and submenu\entry name for the rest.
- Minor code cleanup.
### Removed
### Fixed

## [1.2.0] - 2021-05-26
### Added
- Macros: This.lastCall stores the last menu entry name clicked on. (Meant to be used with macros or forced entries)
### Changed
- Macros: entryMap now contains entries named according to the menu they reside (menu + '\\' + entryName). That allows to call entries with same name but placed on different submenus at the same time. (Meant to be used with macros or forced entries)
- This.clear() has as default argument bForce = false; i.e. to totally clear all set menus, must be set to true.
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

[Unreleased]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.2.2...HEAD
[1.2.2]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/1f1ae22...v1.0.0
