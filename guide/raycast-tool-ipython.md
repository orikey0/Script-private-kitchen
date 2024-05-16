## ipython快速启动
### 创建方式
1. 创建一个script
2. 选择bash
3. 输入下面的脚本代码
### 脚本
```shell
#!/bin/bash

# Required parameters:
# @raycast.schemaVersion 1
# @raycast.title ipython
# @raycast.mode silent

# Optional parameters:
# @raycast.icon 

# Documentation:
# @raycast.description Open IPython in iTerm.

osascript <<EOF
tell application "iTerm"
    activate
    try
        set newWindow to (create window with default profile)
    on error
        set newWindow to current window
    end try
    tell newWindow
        tell current session
            write text "ipython"
        end tell
    end tell
end tell
EOF
```
