# Menu-Framework-SMP
[![version][version_badge]][changelog]
[![CodeFactor][codefactor_badge]](https://www.codefactor.io/repository/github/regorxxx/Menu-Framework-SMP/overview/main)
[![CodacyBadge][codacy_badge]](https://www.codacy.com/gh/regorxxx/Menu-Framework-SMP/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=regorxxx/Playlist-Tools-SMP&amp;utm_campaign=Badge_Grade)
![GitHub](https://img.shields.io/github/license/regorxxx/Menu-Framework-SMP)  
A helper script for [Spider Monkey Panel](https://theqwertiest.github.io/foo_spider_monkey_panel) and [foobar2000](https://www.foobar2000.org) which allows to easily create customizable menus on demand which can be easily refactored, moved or edited without working with static ids. A lifesaver.

## Features
- Creates menus on demand on panels without needing to create specific methods for every script, calculate IDs, etc.  
- Menus are pushed to a list and created automatically on demand, linking the entries to their idx without needing a 'switch' block or leaving holes to ensure idx get enough numbers to expand the script.  
- The main utility of this helper is greatly reducing coding for simple menus and having both, the menu logic creation and the menus' functions on the same place. Creation order is done following entry/menus addition.
- Can concatenate multiple menus on btn_up().

## Usage
First create the menu object. That's the main one and also includes a 'main menu' to append items to it:
```javascript
const menu = new _menu();
menu.newEntry({menu, entryText: 'hello', func: () => {console.log('hello')}}); // Shorthand notation
menu.newEntry({entryText: 'hello2', func: () => {console.log('hello2')}}); // Or omit the menu, to append directly to main one
menu.newEntry({entryText: 'sep'}); // You can also add a separator
```

Then, you may want to create sub-menus linked to it. To do that, just create a new menu entry within the object:
```javascript
const subMenu = menu.newMenu('This is a submenu'); // It will be added just after the last declared entry!
menu.newEntry({menuName: subMenu, entryText: 'This is my func', func: yourFunc);
```

Sub-menus can also be dynamically created:
```javascript
var bSubMenu = true;
const funct = () => {return (bSubMenu) ? 'SubMenu 1' : 'SubMenu 2';};
menu.newMenu(funct);
menu.newEntry({menuName: funct, entryText: 'Change SubMenu', func: () => {bSubMenu = !bSubMenu}});
menu.newEntry({m
enuName: funct, entryText:'Hola 3', func: () => {console.log('Hola3')}, flags: () => {return (bSubMenu) ? MF_STRING : MF_GRAYED}});
```

Finally, lets call it with a callback:
```javascript
function on_mouse_rbtn_up(x, y) {return menu.btn_up(x, y);}
```

There are more usage examples and full documentation on the header of 'menu_xxx.js'.

## Other implementations
 1. [Playlist-Tools-SMP](https://github.com/regorxxx/Playlist-Tools-SMP): Different tools for [foobar2000](https://www.foobar2000.org). The dynamic configurable menu is built using this.
 2. [Playlist-Manager-SMP](https://github.com/regorxxx/Playlist-Manager-SMP): A playlist manager for [foobar2000](https://www.foobar2000.org). The static menus use this.

![Animation9](https://user-images.githubusercontent.com/83307074/116756215-44239480-a9fb-11eb-8489-b56a178c70f4.gif)

## Installation
Copy all files from the zip into YOUR_FOOBAR_PROFILE_PATH\scripts\SMP\xxx-scripts  
Any other path WILL NOT work without editing the scripts. (see images\_Installation_*jpg)  
For ex: mine is c:\Users\xxx\AppData\Roaming\foobar2000\scripts\SMP\xxx-scripts\...  
For portable installations >= 1.6: .\foobar2000\profile\scripts\SMP\xxx-scripts\...  
For portable installations <= 1.5: .\foobar2000\scripts\SMP\xxx-scripts\...  
Then load any button script into a SMP panel within foobar.  

Since the framework only requires 2 files, i.e. the main one and the helper... it's pretty easy to adjust the include paths to whatever it's preferred.

[changelog]: CHANGELOG.md
[version_badge]: https://img.shields.io/github/release/regorxxx/Menu-Framework-SMP.svg
[codacy_badge]: https://api.codacy.com/project/badge/Grade/e04be28637dd40d99fae7bd92f740677
[codefactor_badge]: https://www.codefactor.io/repository/github/regorxxx/Menu-Framework-SMP/badge/main

