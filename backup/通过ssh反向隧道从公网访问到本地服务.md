## 通过ssh反向隧道从公网访问到本地服务

核心操作

```
!mkdir  ~/.ssh/
!touch  ~/.ssh/known_hosts
!ssh-keyscan -t rsa remote.moe >> ~/.ssh/known_hosts
!rm /root/.ssh/id_rsa
!ssh-keygen -t rsa -b 4096 -f /root/.ssh/id_rsa -q -N ""
!python /kaggle/working/ComfyUI/main.py & ssh -R 80:127.0.0.1:8188 -o StrictHostKeyChecking=no -i /root/.ssh/id_rsa remote.moe
```

这里用到了 [remote.moe](https://github.com/fasmide/remotemoe)这个项目