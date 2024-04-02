1. 还是先Release编译程序

2. 将可执行程序复制到一个新目录 src

3. 新建一个脚本**copylib.sh**，主要用来 copy 相关库的,**第一个参数是可执行文件**

   ```
   #!/bin/bash
   
   LibDir=$PWD"/lib"
   Target=$1
   
   lib_array=($(ldd $Target | grep -o "/.*" | grep -o "/.*/[^[:space:]]*"))
   
   $(mkdir $LibDir)
   
   for Variable in ${lib_array[@]}
   do
       cp "$Variable" $LibDir
   done
   ```

4. 先 copy 程序依赖库，`copylib.sh ISTSC`，将 lib 下的库复制出来

5. 再 copy qt 运行依赖库;

   进入qt平台目录下 `/opt/Qt/5.15.2/gcc_64/plugins/platforms`

   运行`copylib.sh libqxcb.so`

   copy lib下的库到src中
   copy platforms目录下其他库到src
   
6. COPY mysql的库 `sqldrivers/libqsql.so`和 `/usr/lib/x86_64-linux-gnu/libmysqlclient.so 到src`
   
7. copy qml下的所有到sr c

8. copy gcc_x86下的lib库的内容到src下

9. 可以在目录下在创建一个运行脚本,用来设置程序运行库的路径的
  ```
  #!/bin/sh
  appname=`basename $0 | sed s,\.sh$,,`
  dirname=`dirname $0`
  tmp="${dirname#?}"
  if [ "${dirname%$tmp}" != "/" ]; then
  dirname=$PWD/$dirname
  fi
  LD_LIBRARY_PATH=$dirname
  export LD_LIBRARY_PATH
  $dirname/$appname "$@"
  ```



>>    [参考链接](https://www.huaweicloud.com/articles/ca0f1e1d3ed52d1fd572b4229026aa59.html)