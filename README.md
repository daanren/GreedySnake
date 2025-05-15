
# 贪吃蛇游戏文档

这是一个简单的基于 HTML, CSS, 和 JavaScript 的浏览器端贪吃蛇游戏项目。游戏包含用户登录、分数记录系统，以及一个基础的管理员面板用于数据管理。所有数据当前都存储在浏览器的本地存储 (localStorage) 中。
Do you need an English version? Slide down
## 项目文件

项目包含以下三个主要文件：

-   `main.html`: 游戏的 HTML 结构，定义了用户界面（登录区域、游戏区域、管理员区域）和各个元素的布局。
-   `style.css`: 游戏的样式表，控制游戏的外观和元素的布局、颜色、字体等。
-   `script.js`: 游戏的核心逻辑，包括初始化游戏、处理用户输入、游戏循环、得分计算、碰撞检测、食物生成、用户登录/管理，以及管理员面板的功能实现。

## 如何运行游戏

1.  确保 `main.html`, `style.css`, 和 `script.js` 这三个文件位于 **同一个文件夹** 中。
2.  使用任何现代网页浏览器（如 Chrome, Firefox, Edge 等）打开 `main.html` 文件。
3.  游戏将在浏览器中启动。

**重要提示：** 由于游戏数据存储在浏览器的 `localStorage` 中，这意味着分数记录仅在该 **当前浏览器** 中有效。如果清除浏览器数据或更换浏览器/设备，分数将丢失。要实现跨浏览器/设备的同步，需要一个后端服务器来集中存储数据。

## 玩家游戏功能

当你打开 `main.html` 并输入一个非 `admin` 的名字登录后，将进入玩家游戏界面。

### 玩家登录

1.  打开 `main.html`。
2.  在登录界面输入你的用户名。
3.  点击“进入游戏”。
    *   如果是新用户，你的分数将被初始化为 0。
    *   如果是已有用户（在当前浏览器保存过分数），你的最高分将被加载。

### 游戏玩法

-   **目标：** 控制贪吃蛇移动，吃到红色的食物方块。每吃到一个食物，蛇会变长并增加分数。
-   **失败：** 蛇头撞到墙壁或撞到自己的身体时，游戏结束。

### 游戏控制

-   **键盘：**
    -   使用方向键 (↑, ↓, ←, →) 控制蛇的移动方向。
    -   或者使用 WASD 键 (W:上, S:下, A:左, D:右) 控制蛇的移动方向。
-   **虚拟摇杆：**
    -   在游戏 Canvas 下方有四个带有方向箭头的方块按钮。
    -   点击对应的按钮来控制蛇移动方向。这对于触摸屏设备非常方便。

### 游戏界面元素

-   **当前用户 / 最高分：** 显示当前登录的用户名和你的历史最高分。
-   **分数：** 显示当前局游戏的得分。
-   **Canvas：** 游戏的主要区域，蛇和食物在这里绘制。
-   **虚拟摇杆：** 控制蛇的按钮。
-   **游戏消息：** 显示游戏提示，如“按任意方向键开始”、“游戏结束”等。
-   **重新开始按钮：** 游戏结束后出现，点击开始新一局游戏。
-   **所有最高分：** 显示除管理员外所有玩家的最高分排行榜（基于当前浏览器的 localStorage 数据）。

### 保存分数按钮

在“当前用户 / 最高分”旁边有一个“保存分数”按钮。

-   **功能：** 点击此按钮会将当前用户的最高分记录强制保存到**当前浏览器的 localStorage**。
-   **注意：**
    -   游戏结束后获得新高分时，系统会自动保存到 localStorage。所以这个按钮在核心功能上并非必需，但提供了手动保存的选项。
    -   **它无法实现跨浏览器或跨设备的同步！** 同步功能需要后端支持。

## 管理员面板功能

### 如何进入管理员面板

在游戏的登录界面，输入用户名 `admin`，然后点击“进入游戏”。

### 管理员面板界面元素

-   **管理员面板标题：** 显示“管理员面板”。
-   **当前用户：** 显示当前登录的管理员用户名 (`admin`)。
-   **退出管理员按钮：** 点击返回登录界面。
-   **所有玩家分数记录表格：** 显示一个表格，列出所有玩家（包括admin自身，但admin不显示分数）的用户名和他们的最高分。
-   **危险操作区域：** 包含清空所有数据的按钮。

### 管理员操作

在“所有玩家分数记录”表格中，管理员可以对除 `admin` 之外的玩家数据进行操作：

-   **修改分数：**
    1.  在要修改分数的玩家行中，找到“最高分”列旁的数字输入框。
    2.  在输入框中输入新的最高分数（只能输入非负整数）。
    3.  点击输入框旁边的“修改”按钮。
    4.  修改将保存到 localStorage，表格显示会立即更新。
-   **删除用户：**
    1.  在要删除用户的行中，找到“删除用户”按钮。
    2.  点击按钮。
    3.  会弹出一个确认框，asks you to confirm the deletion.
    4.  如果点击“确定”，该用户的分数数据将被从 localStorage 中删除，该行也会从表格中移除。此操作不可恢复。
-   **清空所有数据：**
    1.  在管理员面板底部，找到红色的“清空所有数据”按钮。
    2.  点击按钮。
    3.  会弹出一个警告确认框，明确说明此操作将删除所有玩家（包括admin自己的记录，意味着下次登录admin需要再次输入用户名）的数据且不可恢复。
    4.  如果点击“确定”，localStorage 中存储的所有玩家数据将被删除，并立即返回登录界面。

## 数据存储说明 (localStorage)

如前所述，游戏数据（用户名和最高分）存储在浏览器的 `localStorage` 中。

-   `localStorage` 是一种客户端 (浏览器) 存储机制。
-   数据没有过期时间，除非用户清除浏览器数据或通过管理员面板手动删除。
-   数据特定于当前浏览器和域名（协议+主机+端口）。**不同浏览器、不同设备或同一域名下的不同子域/端口之间不共享数据。**
-   存储的数据量有限（通常为 5-10MB）。

## 潜在的未来改进

-   实现后端服务器和数据库，实现跨浏览器/设备的用户数据同步。
-   添加游戏音效和背景音乐。
-   增加游戏难度选项（控制蛇的速度、食物生成速度等）。
-   实现游戏暂停/继续功能。
-   设计不同的游戏地图或障碍物。
-   提升游戏视觉效果和动画。

这份文档应该能帮助你或其他任何人理解这个贪吃蛇游戏项目的运行、玩法以及包含的玩家和管理员功能。
文件已放在Releases中


For English,This document is a direct translation by translation software, and the meaning may not be accurate

#Snake game documentation

This is a simple browser side Snake game project based on HTML, CSS, and JavaScript. The game includes user login, score recording system, and a basic administrator panel for data management. All data is currently stored in the browser's local storage.

##Project documents

The project includes the following three main files:

-` main. html `: The HTML structure of the game, which defines the user interface (login area, game area, administrator area) and the layout of various elements.
-Style. css: A style sheet for the game that controls the appearance and layout of elements, colors, fonts, etc.
-Script. js: The core logic of the game, including initializing the game, processing user input, game loops, score calculation, collision detection, food generation, user login/management, and implementing the functions of the administrator panel.

##How to run the game

1. Ensure that the files' main. html ',' style. css', and 'script. js' are located in the same folder.
2. Use any modern web browser (such as Chrome, Firefox, Edge, etc.) to open the 'main. html' file.
3. The game will start in the browser.

**Important note: Due to game data being stored in the browser's' localStorage ', this means that score records are only valid in the current browser. If the browser data is cleared or the browser/device is replaced, the score will be lost. To achieve cross browser/device synchronization, a backend server is needed to centrally store data.

##Player game functions

When you open 'main. html' and enter a non admin name to log in, you will enter the player game interface.

###Player login

1. Open 'main. html'.
2. Enter your username in the login interface.
3. Click on "Enter Game".
*If you are a new user, your score will be initialized to 0.
*If it is an existing user (who has saved scores in the current browser), your highest score will be loaded.

###Gameplay

-* * Objective: * * Control the movement of the greedy snake and eat the red food cube. Every time a snake eats a food, it grows longer and increases its score.
-* * Failure: * * The game ends when the snake head hits a wall or hits its own body.

###Game Control

-* * Keyboard:**
-Use the directional keys (↑, ↓, ←, →) to control the direction of the snake's movement.
-Alternatively, use the WASD keys (W: up, S: down, A: left, D: right) to control the direction of the snake's movement.
-Virtual joystick:**
-There are four square buttons with directional arrows below the game Canvas.
-Click the corresponding button to control the direction of snake movement. This is very convenient for touch screen devices.

###Game interface elements

-* * Current User/Highest Score: * * Display the currently logged in username and your highest score in history.
-Score: * * Display the score of the current game.
-Canvas: The main area of the game, where snakes and food are drawn.
-Virtual joystick: The button that controls the snake.
-Game message: Display game prompts such as "Press any directional key to start", "Game ends", etc.
-* * Restart button: * * Appears after the game ends, click to start a new game.
-* * All highest scores: * * Display the highest score ranking list of all players except for the administrator (based on the current browser's local storage data).

###Save Score Button

There is a 'Save Score' button next to 'Current User/Highest Score'.

-* * Function: * * Clicking this button will force the highest score record of the current user to be saved to the local Storage * * of the current browser.
-* * Attention:**
-When a new high score is obtained after the game ends, the system will automatically save it to local storage. So this button is not necessary in terms of core functionality, but it provides an option for manual saving.
-It cannot achieve cross browser or cross device synchronization! **The synchronization function requires backend support.

##Administrator panel function

###How to enter the administrator panel

In the login interface of the game, enter the username 'admin', and then click 'Enter Game'.

###Administrator panel interface elements

-Administrator Panel Title: * * Display "Administrator Panel".
-* * Current user: * * Display the current logged in administrator username (` admin `).
-* * Exit Administrator Button: * * Click to return to the login interface.
-* * All player score record table: * * Display a table that lists the usernames and highest scores of all players (including admin themselves, but admin does not display scores).
-Dangerous operation area: * * Includes a button to clear all data.

###Administrator operation

In the 'All Player Score Records' table, administrators can manipulate player data except for' admin ':

-* * Modify score:**
1. In the player row where you want to modify the score, find the number input box next to the "highest score" column.
2. Enter the new highest score in the input box (only non negative integers can be entered).
3. Click the "Modify" button next to the input box.
4. The modifications will be saved to local storage, and the table display will be updated immediately.
-* * Delete user:**
1. In the row where you want to delete a user, find the "Delete User" button.
2. Click the button.
3. A confirmation box will pop up, asks you to confirm the deletion.
If you click "OK", the user's score data will be deleted from the local storage and the row will also be removed from the table. This operation is irreversible.
-* * Clear all data:**
At the bottom of the administrator panel, find the red "Clear All Data" button.
2. Click the button.
3. A warning confirmation box will pop up, clearly stating that this operation will delete the data of all players (including admin's own records, which means that the next login to admin will require entering the username again) and cannot be restored.
If you click "OK", all player data stored in localStorage will be deleted and you will immediately return to the login interface.

##Data Storage Instructions (LocalStorage)

As mentioned earlier, game data (username and highest score) is stored in the browser's' localStorage '.

-LocalStorage is a client (browser) storage mechanism.
-The data has no expiration date unless the user clears the browser data or manually deletes it through the administrator panel.
-The data is specific to the current browser and domain name (protocol+host+port). **Data is not shared between different browsers, devices, or subdomains/ports under the same domain name. **
-The amount of stored data is limited (usually 5-10MB).

##Potential future improvements

-Implement backend servers and databases to achieve cross browser/device synchronization of user data.
-Add game sound effects and background music.
-Increase game difficulty options (control snake speed, food generation speed, etc.).
-Implement game pause/resume function.
-Design different game maps or obstacles.
-Enhance the visual effects and animations of the game.

This document should help you or anyone else understand the operation, gameplay, and player and administrator features included in this Snake game project.
The file has been placed in the releases
