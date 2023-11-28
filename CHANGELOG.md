# Changelog

## [Table of Contents]
- [Unreleased](#unreleased)
- [2.6.0](#260---2023-11-28)
- [2.5.0](#250---2023-09-26)
- [2.4.0](#240---2023-03-08)
- [2.3.0](#230---2023-02-24)
- [2.2.0](#220---2023-01-28)
- [2.1.0](#210---2022-05-19)
- [2.0.1](#201---2021-12-23)
- [2.0.0](#200---2021-10-14)
- [1.2.2](#122---2021-06-07)
- [1.2.1](#121---2021-05-28)
- [1.2.0](#120---2021-05-26)
- [1.1.0](#110---2021-05-19)
- [1.0.0](#100---2021-05-05)

## [Unreleased][]
### Added
### Changed
### Removed
### Fixed

## [2.5.0] - 2023-09-26
### Added
- New method .newCheckMenuLast(boolFunc),sShorthand for .newCheckMenu(menuName, entryTextA, void(0), boolFunc), where the entry is automatically retrieved from the last one added to the menu.
### Changed
### Removed
### Fixed
- "menuName.indexOf is not a function" error at newMenu() due to typo on variable type checks.
- concat() not working properly with menu objects with sub-menus or menu checks.
- btn_up(x, y, object, ....) not working properly with menu objects with sub-menus or menu checks.

## [2.5.0] - 2023-09-26
### Added
- New argument 'bLogEntries' on menu object creation which allows to enable/disable the logging of clicked menu entries.
- New argument 'bInit'. Set to false to directly replace with a contextual/main menu obj.
- New method retry() to call last entry with configurable arguments.
- New method isSeparator() and isNotSeparator() to be used along newCheckMenu(), when checking the index of an array of options (so it filters the separators). Looks for properties named 'entryText' or 'name. For ex:
```
const options = [{name: 'My entry', val: true}, {name: 'sep'}, {name: 'My other entry', val: true}];
options.forEach(() => ...); // Create menu entries, etc.
menu.newCheckMenu(menuName, options[0].name, options[options.length - 1].name, () => {return options.filter(menu.isNotSeparator).findIndex((opt) => opt.val === val;});
```
### Changed
- Improved contextual menu for handle lists with a header at top (playlist name + # tracks).
- Exposed getNextId() method, to retrieve invisible Ids.
- Improved error reporting for check menus.
### Removed
### Fixed

## [2.4.0] - 2023-03-08
### Added
- Support for [contextual menus](https://theqwertiest.github.io/foo_spider_monkey_panel/assets/generated_files/docs/html/ContextMenuManager.html) and [main menus](https://theqwertiest.github.io/foo_spider_monkey_panel/assets/generated_files/docs/html/MainMenuManager.html) at newMenu(menuName, subMenuFrom, flags, context /*{type, playlistIdx}*/, main /*{type}*/) method, by setting the 'context' or 'main' arguments. Type may be either 'handlelist', 'playlist', or 'nowplaying' in the case of contextual menus; for main menus, type must be one of the following: 'file', 'view', 'edit', 'playback', 'library', 'help'. All ids are handled under the hood. Creating a contextual menu is as easier as:
```
// If no playlistIdx is given then it uses the active playlist
menu.newMenu('Items...', void(0), void(0), {type: 'handlelist', playlistIdx: plman.FindPlaylist(pls.nameId)});
```
### Changed
### Removed
### Fixed
- Objects not properly parsed at error logging.
- Entry name not properly set -to the function name- when entryText was a function at addToMenu() method.

## [2.3.0] - 2023-02-24
### Added
- New method getMenuNameFrom() which allows to partial match a submenu from a parent menu using the name minus the invisible ID (at the end). i.e hasMenu() would always fail if not providing the exact ID, but the former would work fine as long as the submenu and parent names are known.
- New method findOrNewMenu() which can now be used along invisible IDs to create or retrieve a (sub)menu without need to check if the menu already exists. i.e. if the menu 'Genre' has a submenu called 'Edit' with invisible Ids, instead of storing the name + ID in a variable, findOrNewMenu('Edit', 'Genre') will either create that submenu or retrieve the existing one. It's obviously a shortcut to getMenuNameFrom() or newMenu() within a single line of code.
### Changed
- Code cleanup. Moved most helpers to private context.
### Removed
### Fixed

## [2.2.0] - 2023-01-28
### Added
- Added new argument to _attachedMenu() named 'popup' which may be used to avoid calling attached menu. It's expected to return true when calling popup.isEnabled() to do so.
- Added 'onBtnUp' callback called after processing mouse btn_up. Respects the value of this inside the function, if any. It may be used to do something according to the processing of the menu.
### Changed
- When trying to add multiple (sub)menus with same name (and different parent), an invisible ID may be added to allow it. '.newMenu()' will return the final name in such case. Set 'bAddInvisibleIds' on menu creation for this. It's now the default behavior. The IDs are stripped at the menu drawing step, to ensure they are not incorrectly rendered by some fonts (usually on Wine). In other words, this ensures every entry has an unique idx in SMP terms, while working with just entry names and allowing 'name' duplication as long as the parent differs. The best of both worlds.
### Removed
### Fixed

## [2.1.1] - 2022-10-01
### Added
### Changed
- Reworked separator identification with regexp instead of string matching in all instances, case insensitive.
- Separator entries passed to 'newCheckMenu' will be skipped; not requiring additional code anymore to split menu creation for standard entries and separators.
- Improved error reporting.
### Removed
### Fixed
- Crash on btn_up() when multiple submenus with same name where added using newMenu(). Now warns about it when calling newMenu() and aborts the addition to avoid later crashing.

## [2.1.0] - 2022-05-19
### Added
- iMaxTabLen: similar to 'iMaxEntryLen' menu can be initialized with a fixed entry text length for displaying purposes. This variable will cut anything found after '\t', usually used to display additional values or tips on menus. Menu entry names are now split by '\t' before applying iMaxMenuLen and iMaxTabLen max length to both parts. Default value is Infinity, i.e. it will use the full entry name. For ex: 'Allows only these tags on the pool...\tRock, Folk, Blues, Opera' -> 'Allows only these tags on the pool...\tRock, ...'
- bindArgs: added new argument 'bindArgs' to .initMenu(object, bindArgs = null /*{pos: -1, args: null}*/). Works the same than the one at .btn_up(), but the former applies to conditional entries calling. Could be used to run specific conditional entries only on demand.
### Changed
- iMaxMenuLen: renamed to iMaxEntryLen. Default value is now Infinity, i.e. it will use the full entry name.
- iMaxMenuLen and iMaxTabLen: string cutting now looks for ')', ']', '}' and ':' at the end of both strings to add it again after cutting. Previously it only did so for ':'. For ex: 'Allows only these tags on the pool...\t(Rock, Folk, Blues, Opera)' -> 'Allows only these tags on the pool...\t(Rock, ...)'
- All entry and menu names passed as arguments to menu construction (newMenu, newEntry, newCheckMenu, newCondEntry) are converted automatically to strings whenever a number/array/object/boolean variable is used. In the case of being a function, it's evaluated just before menu tracking (addToMenu) -i.e. maintains the previous behavior-; the returned value is given the previous treatment, but if a function is returned, then its name (function.name) is used as entry name. Although it's recommended to only pass strings to the menus, this ensures passing arrays, lists or other output from functions which can be converted to string still create valid menu entries. Passing any other value type will throw an error and report the failed entry.
### Removed
### Fixed

## [2.0.1] - 2021-12-23
### Added
- iMaxMenuLen: menu can be initialized with a fixed entry text length for displaying purposes. Entries will be cut to such length and added '...' to the end when they are cut. ':' is also maintained at the end when edited. For ex: 'Varied Styles/Genres mix, within a decade' - > 'Varied Styles/Genres mix, ...'. 'Check errors on current playlist:' - > 'Check errors on current...:'. Internal names preserve the original full length string, and that's what's used to call the menu entry or when reporting it to console.
### Changed
- hasMenu: allows a second argument pointing to its main menu (subMenuFrom). Leave it blank to look for the menu at any place. hasMenu(menuName, subMenuFrom = '')
### Removed
### Fixed
- hasMenu: not working as expected, always returning false.

## [2.0.0] - 2021-10-14
### Added
- Menu framework: added bool variable (bExecute) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0, bindArgs = null) which allows to simulate the menu without executing any related entry function. 
- Menu framework: added func variable (replaceFunc) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0, bindArgs = null) which allows to replace the related entry function with a custom one, whenever bExecute is also false. Can be used to paste to clipboard entry names easily simulating the menu usage.
- Menu framework: added flag variable (flag) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0, bindArgs = null) which allows to set SMP TrackPopupMenu's flag.
- Menu framework: added arg variable (bindArgs) to .btn_up(x, y, object, forcedEntry = '', bExecute = true, replaceFunc = null, flag = 0, bindArgs = null) which allows to call the function associated to the entry with an additional bound argument. bindArgs = {pos: -1, args: null}, where 'pos' denotes the place where it will be added (all other arguments will be filled with void(0) to use defaults) and 'args' is passed as is.
### Changed
- Menu framework: .initMenu and .btn_up are now 2 separate functions. i.e. the menu can be recreated without having to create the UI elements using .initMenu instead of .btn_up (which also calls .initMenu).
### Removed
### Fixed
- Menu framework: '&' char not showing (or making next char underscored) on created dynamic menus (when it was part of a playlist name for ex.), since they were not doubled. Now the framework automatically checks for names with '&' and doubles them ('&&' are skipped), so they are displayed right.
- Menu framework: Menu entry checks were not being cleared properly when forcing a reset ('menu.clear(true)'), usually used on menus which are created and deleted every time they are called. This was only a problem when the menu entries' names changed on consecutive calls, for ex. when adding invisible chars at menu names.

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

[Unreleased]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.5.0...HEAD
[2.5.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.4.0...v2.5.0
[2.4.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.3.0...v2.4.0
[2.3.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.2.0...v2.3.0
[2.2.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.1.1...v2.2.0
[2.1.1]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.1.0...v2.1.1
[2.1.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.0.1...v2.1.0
[2.0.1]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v2.0.0...v2.0.1
[2.0.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.2.2...v2.0.0
[1.2.2]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/regorxxx/Menu-Framework-SMP/compare/1f1ae22...v1.0.0