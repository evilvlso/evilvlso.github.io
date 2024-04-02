有两个配置文件 :
settings.json - 用来运行的配置
launch.json  -  用来调试的配置
> 划取代码运行使用的是 settings.json 配置  
> vscode 下面的解释器选择可以直接更改两个文件的 python 解释器路径

配置展示:  
settings.json  

```JSON
{
    "launch": {

        "configurations": [
            {"name":"Launch",
            "type":"python",
            "request":"launch",
            "console": "integratedTerminal",
            "cwd":"${fileDirname}", ## 解决执行路径问题
             //工作路径用打开的顶层目录，影响文件读写相对路径
            //"cwd": "${workspaceFolder}", 
            //工作路径用当前文件所在目录，影响文件读写相对路径
            //"cwd": "${fileDirname}",
            //sys.path 会加入顶层目录，影响模块导入查询路径
            //"env": { "PYTHONPATH": "${workspaceFolder}" }
            }
        ],
        "compounds": []
    },
    "python.pythonPath": "/usr/local/anaconda3/envs/mrcnn/bin/python"
}
```
launch.json  
```JSON
{
    "version": "0.2.0",
    "configurations": [

        {
            "name": "Python: base",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "pythonPath": "/usr/local/anaconda3/bin/python"
        },
        {
            "name": "Python: env",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "pythonPath": "~/env/bin/python"
        },
        {
            "name": "Python: mrcnn",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "pythonPath": "/usr/local/anaconda3/envs/mrcnn/bin/python"
        },
    ]

}
```