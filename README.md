# eof_alfred

### Alfred集成iTerm

步骤1：打开Alfred -> Preperence -> Features -> Terminal / Shell

步骤2：Application选择“Custom”，下方的脚本替换为

```
on alfred_script(q)  
    if application "iTerm2" is running or application "iTerm" is running then  
        run script "  
            on run {q}  
                tell application \":Applications:iTerm.app\"  
                    activate  
                    try  
                        select first window  
                        set onlywindow to false  
                    on error  
                        create window with default profile  
                        select first window  
                        set onlywindow to true  
                    end try  
                    tell current session of the first window  
                        if onlywindow is false then  
                            tell split vertically with default profile  
                                write text q  
                            end tell  
                        end if  
                    end tell  
                end tell  
            end run  
        " with parameters {q}  
    else  
        run script "  
            on run {q}  
                tell application \":Applications:iTerm.app\"  
                    activate  
                    try  
                        select first window  
                    on error  
                        create window with default profile  
                        select first window  
                    end try  
                    tell the first window  
                        tell current session to write text q  
                    end tell  
                end tell  
            end run  
        " with parameters {q}  
    end if  
end alfred_script  
```

[Alfred集成Iterm2](https://blog.csdn.net/endlu/article/details/52955554)

[iTerm documentation-scripting](http://www.iterm2.com/documentation-scripting.html)

[custom-iterm-applescripts-for-alfred](https://github.com/stuartcryan/custom-iterm-applescripts-for-alfred)

