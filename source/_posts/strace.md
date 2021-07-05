---
title: strace
date: 2021-06-21 23:36:21
tags:
    - linux
    - strace
---
## strace参数列表
* strace常用参数
-c 统计每一系统调用的所执行的时间,次数和出错的次数等.
-d 输出strace关于标准错误的调试信息.
<font color=#FF0000 >-f 跟踪由fork调用所产生的子进程.</font>
-ff 如果提供-o filename,则所有进程的跟踪结果输出到相应的filename.pid中,pid是各进程的进程号.
-F 尝试跟踪vfork调用.在-f时,vfork不被跟踪.
-h 输出简要的帮助信息.
-i 输出系统调用的入口指针.
-q 禁止输出关于脱离的消息.
-r 打印出相对时间关于,每一个系统调用.
<font color=#FF0000 >-t 在输出中的每一行前加上时间信息.
-tt 在输出中的每一行前加上时间信息,微秒级.
-ttt 微秒级输出,以秒了表示时间.
-T 显示每一调用所耗的时间.</font>
-v 输出所有的系统调用.一些调用关于环境变量,状态,输入输出等调用由于使用频繁,默认不输出.
-V 输出strace的版本信息.
-x 以十六进制形式输出非标准字符串
-xx 所有字符串以十六进制形式输出.
-a column 设置返回值的输出位置.默认 为40.
<!-- more -->
<font color=#FF0000 >-e expr 指定一个表达式,用来控制如何跟踪.格式如下:
[qualifier=][!]value1[,value2]…
qualifier只能是 trace,abbrev,verbose,raw,signal,read,write其中之一.value是用来限定的符号或数字.默认的 qualifier是 trace.感叹号是否定符号.例如:
-eopen等价于 -e trace=open,表示只跟踪open调用.而-etrace!=open表示跟踪除了open以外的其他调用.有两个特殊的符号 all 和 none.</font>
<font color=#FF00FF >注意有些shell使用!来执行历史记录里的命令,所以要使用\.</font>
-e trace=set 只跟踪指定的系统 调用.例如:-e trace=open,close,rean,write表示只跟踪这四个系统调用.默认的为set=all.
-e trace=file 只跟踪有关文件操作的系统调用.
-e trace=process 只跟踪有关进程控制的系统调用.
-e trace=network 跟踪与网络有关的所有系统调用.
-e strace=signal 跟踪所有与系统信号有关的 系统调用
-e trace=ipc 跟踪所有与进程通讯有关的系统调用
-e abbrev=set 设定 strace输出的系统调用的结果集.-v 等与 abbrev=none.默认为abbrev=all.
-e raw=set 将指 定的系统调用的参数以十六进制显示.
-e signal=set 指定跟踪的系统信号.默认为all.如 signal=!SIGIO(或者signal=!io),表示不跟踪SIGIO信号.
-e read=set 输出从指定文件中读出 的数据.例如:
-e read=3,5
-e write=set 输出写入到指定文件中的数据.
-o filename 将strace的输出写入文件filename
<font color=#FF0000>-p pid 跟踪指定的进程pid.
-s strsize 指定输出的字符串的最大长度.默认为32.文件名一直全部输出.</font>
-u username 以username 的UID和GID执行被跟踪的命令


## 命令参数演示
<details>
    <summary>strace ls</summary>
<pre><code> 
execve("/usr/bin/ls", ["ls"], 0x7ffefa0f2260 /* 67 vars */) = 0
brk(NULL)                               = 0x561cd864d000
arch_prctl(0x3001 /* ARCH_??? */, 0x7fff64449820) = -1 EINVAL (无效的参数)
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (没有那个文件或目录)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=80267, ...}) = 0
mmap(NULL, 80267, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7fd6cc2ca000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0@p\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=163200, ...}) = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7fd6cc2c8000
mmap(NULL, 174600, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7fd6cc29d000
mprotect(0x7fd6cc2a3000, 135168, PROT_NONE) = 0
mmap(0x7fd6cc2a3000, 102400, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x7fd6cc2a3000
mmap(0x7fd6cc2bc000, 28672, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1f000) = 0x7fd6cc2bc000
mmap(0x7fd6cc2c4000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x26000) = 0x7fd6cc2c4000
mmap(0x7fd6cc2c6000, 6664, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7fd6cc2c6000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\360q\2\0\0\0\0\0"..., 832) = 832
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
pread64(3, "\4\0\0\0\20\0\0\0\5\0\0\0GNU\0\2\0\0\300\4\0\0\0\3\0\0\0\0\0\0\0", 32, 848) = 32
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\t\233\222%\274\260\320\31\331\326\10\204\276X>\263"..., 68, 880) = 68
fstat(3, {st_mode=S_IFREG|0755, st_size=2029224, ...}) = 0
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
pread64(3, "\4\0\0\0\20\0\0\0\5\0\0\0GNU\0\2\0\0\300\4\0\0\0\3\0\0\0\0\0\0\0", 32, 848) = 32
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\t\233\222%\274\260\320\31\331\326\10\204\276X>\263"..., 68, 880) = 68
mmap(NULL, 2036952, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7fd6cc0ab000
mprotect(0x7fd6cc0d0000, 1847296, PROT_NONE) = 0
mmap(0x7fd6cc0d0000, 1540096, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x25000) = 0x7fd6cc0d0000
mmap(0x7fd6cc248000, 303104, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x19d000) = 0x7fd6cc248000
mmap(0x7fd6cc293000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1e7000) = 0x7fd6cc293000
mmap(0x7fd6cc299000, 13528, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7fd6cc299000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\340\"\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=584392, ...}) = 0
mmap(NULL, 586536, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7fd6cc01b000
mmap(0x7fd6cc01d000, 409600, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x2000) = 0x7fd6cc01d000
mmap(0x7fd6cc081000, 163840, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x66000) = 0x7fd6cc081000
mmap(0x7fd6cc0a9000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x8d000) = 0x7fd6cc0a9000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libdl.so.2", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0 \22\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=18816, ...}) = 0
mmap(NULL, 20752, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7fd6cc015000
mmap(0x7fd6cc016000, 8192, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1000) = 0x7fd6cc016000
mmap(0x7fd6cc018000, 4096, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7fd6cc018000
mmap(0x7fd6cc019000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7fd6cc019000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpthread.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220\201\0\0\0\0\0\0"..., 832) = 832
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\345Ga\367\265T\320\374\301V)Yf]\223\337"..., 68, 824) = 68
fstat(3, {st_mode=S_IFREG|0755, st_size=157224, ...}) = 0
pread64(3, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0\345Ga\367\265T\320\374\301V)Yf]\223\337"..., 68, 824) = 68
mmap(NULL, 140408, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7fd6cbff2000
mmap(0x7fd6cbff9000, 69632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x7000) = 0x7fd6cbff9000
mmap(0x7fd6cc00a000, 20480, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x18000) = 0x7fd6cc00a000
mmap(0x7fd6cc00f000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1c000) = 0x7fd6cc00f000
mmap(0x7fd6cc011000, 13432, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7fd6cc011000
close(3)                                = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7fd6cbff0000
arch_prctl(ARCH_SET_FS, 0x7fd6cbff1400) = 0
mprotect(0x7fd6cc293000, 12288, PROT_READ) = 0
mprotect(0x7fd6cc00f000, 4096, PROT_READ) = 0
mprotect(0x7fd6cc019000, 4096, PROT_READ) = 0
mprotect(0x7fd6cc0a9000, 4096, PROT_READ) = 0
mprotect(0x7fd6cc2c4000, 4096, PROT_READ) = 0
mprotect(0x561cd7376000, 4096, PROT_READ) = 0
mprotect(0x7fd6cc30b000, 4096, PROT_READ) = 0
munmap(0x7fd6cc2ca000, 80267)           = 0
set_tid_address(0x7fd6cbff16d0)         = 35150
set_robust_list(0x7fd6cbff16e0, 24)     = 0
rt_sigaction(SIGRTMIN, {sa_handler=0x7fd6cbff9bf0, sa_mask=[], sa_flags=SA_RESTORER|SA_SIGINFO, sa_restorer=0x7fd6cc0073c0}, NULL, 8) = 0
rt_sigaction(SIGRT_1, {sa_handler=0x7fd6cbff9c90, sa_mask=[], sa_flags=SA_RESTORER|SA_RESTART|SA_SIGINFO, sa_restorer=0x7fd6cc0073c0}, NULL, 8) = 0
rt_sigprocmask(SIG_UNBLOCK, [RTMIN RT_1], NULL, 8) = 0
prlimit64(0, RLIMIT_STACK, NULL, {rlim_cur=8192*1024, rlim_max=RLIM64_INFINITY}) = 0
statfs("/sys/fs/selinux", 0x7fff64449770) = -1 ENOENT (没有那个文件或目录)
statfs("/selinux", 0x7fff64449770)      = -1 ENOENT (没有那个文件或目录)
brk(NULL)                               = 0x561cd864d000
brk(0x561cd866e000)                     = 0x561cd866e000
openat(AT_FDCWD, "/proc/filesystems", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0444, st_size=0, ...}) = 0
read(3, "nodev\tsysfs\nnodev\ttmpfs\nnodev\tbd"..., 1024) = 400
read(3, "", 1024)                       = 0
close(3)                                = 0
access("/etc/selinux/config", F_OK)     = -1 ENOENT (没有那个文件或目录)
openat(AT_FDCWD, "/usr/lib/locale/locale-archive", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=14537584, ...}) = 0
mmap(NULL, 14537584, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7fd6cb212000
close(3)                                = 0
ioctl(1, TCGETS, {B38400 opost isig icanon echo ...}) = 0
ioctl(1, TIOCGWINSZ, {ws_row=13, ws_col=229, ws_xpixel=0, ws_ypixel=0}) = 0
openat(AT_FDCWD, ".", O_RDONLY|O_NONBLOCK|O_CLOEXEC|O_DIRECTORY) = 3
fstat(3, {st_mode=S_IFDIR|0775, st_size=4096, ...}) = 0
getdents64(3, /* 17 entries */, 32768)  = 544
getdents64(3, /* 0 entries */, 32768)   = 0
close(3)                                = 0
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(0x88, 0x1), ...}) = 0
write(1, "_config.landscape.yml  _config.y"..., 136_config.landscape.yml  _config.yml  db.json  node_modules  package.json  package-lock.json  pub_all.sh       public  scaffolds  source  themes
) = 136
close(1)                                = 0
close(2)                                = 0
exit_group(0)                           = ?
+++ exited with 0 +++
</code></pre>
</details>

<details>
<summary>strace -tt ls</summary>
<pre><code>
00:01:46.196960 execve("/usr/bin/ls", ["ls"], 0x7ffc1cb16ee8 /* 67 vars */) = 0
00:01:46.197277 brk(NULL)               = 0x5596897ad000
00:01:46.197318 arch_prctl(0x3001 /* ARCH_??? */, 0x7fff0cb92770) = -1 EINVAL (无效的参数)
00:01:46.197473 access("/etc/ld.so.preload", R_OK) = -1 ENOENT (没有那个文件或目录)
00:01:46.197537 openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
00:01:46.197587 fstat(3, {st_mode=S_IFREG|0644, st_size=80267, ...}) = 0
00:01:46.197635 mmap(NULL, 80267, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f4b887c9000
00:01:46.197671 close(3)                = 0
</code></pre>
</details>

<details>
<summary>strace -tt -T ls</summary>
<pre><code>
00:03:09.784585 execve("/usr/bin/ls", ["ls"], 0x7ffd07ef4a80 /* 67 vars */) = 0 <0.000157>
00:03:09.784872 brk(NULL)               = 0x55d3aed13000 <0.000010>
00:03:09.784916 arch_prctl(0x3001 /* ARCH_??? */, 0x7ffc6de437f0) = -1 EINVAL (无效的参数) <0.000009>
00:03:09.785117 access("/etc/ld.so.preload", R_OK) = -1 ENOENT (没有那个文件或目录) <0.000016>
00:03:09.785195 openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3 <0.000016>
00:03:09.785254 fstat(3, {st_mode=S_IFREG|0644, st_size=80267, ...}) = 0 <0.000011>
00:03:09.785307 mmap(NULL, 80267, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f2ffca08000 <0.000014>
00:03:09.785354 close(3)                = 0 <0.000011>
</code></pre>
</details>


<details>
<summary>strace -tt -T -v ls</summary>
<pre><code>
00:12:35.936338 execve("/usr/bin/ls", ["ls"], ["SHELL=/bin/bash", "SESSION_MANAGER=local/gao-X550VX"..., "WINDOWID=73400327", "QT_ACCESSIBILITY=1", "COLORTERM=truecolor", "XDG_CONFIG_DIRS=/etc/xdg/xdg-ubu"..., "XDG_MENU_PREFIX=gnome-", "TERM_PROGRAM_VERSION=1.57.0", "GNOME_DESKTOP_SESSION_ID=this-is"..., "APPLICATION_INSIGHTS_NO_DIAGNOST"..., "LANGUAGE=zh_CN:zh", "GNOME_SHELL_SESSION_MODE=ubuntu", "SSH_AUTH_SOCK=/run/user/1000/key"..., "BREAKPAD_DUMP_LOCATION=/home/gao"..., "SHELL_SESSION_ID=eb7ceb33561f492"..., "XMODIFIERS=@im=ibus", "DESKTOP_SESSION=ubuntu", "SSH_AGENT_PID=2200", "GTK_MODULES=gail:atk-bridge", "PWD=/home/gao/wkspace/Andersonhe"..., "XDG_SESSION_DESKTOP=ubuntu", "LOGNAME=gao", "XDG_SESSION_TYPE=x11", "GPG_AGENT_INFO=/run/user/1000/gn"..., "XAUTHORITY=/run/user/1000/gdm/Xa"..., "VSCODE_GIT_ASKPASS_NODE=/usr/sha"..., "GJS_DEBUG_TOPICS=JS ERROR;JS LOG", "WINDOWPATH=2", "HOME=/home/gao", "USERNAME=gao", "IM_CONFIG_PHASE=1", "LANG=zh_CN.UTF-8", "LS_COLORS=rs=0:di=01;34:ln=01;36"..., "XDG_CURRENT_DESKTOP=Unity", "KONSOLE_DBUS_SERVICE=:1.94", "KONSOLE_DBUS_SESSION=/Sessions/1", "GIT_ASKPASS=/usr/share/code/reso"..., "INVOCATION_ID=4498fa43c37e41e080"..., "KONSOLE_VERSION=191203", "MANAGERPID=2017", "CHROME_DESKTOP=code-url-handler."..., "GJS_DEBUG_OUTPUT=stderr", "LESSCLOSE=/usr/bin/lesspipe %s %"..., "XDG_SESSION_CLASS=user", "TERM=xterm-256color", "LESSOPEN=| /usr/bin/lesspipe %s", "USER=gao", "VSCODE_GIT_IPC_HANDLE=/run/user/"..., "COLORFGBG=0;15", "DISPLAY=:0", "SHLVL=2", "QT_IM_MODULE=ibus", "XDG_RUNTIME_DIR=/run/user/1000", "VSCODE_GIT_ASKPASS_MAIN=/usr/sha"..., "JOURNAL_STREAM=8:46455", "XDG_DATA_DIRS=/usr/share/ubuntu:"..., "GDK_BACKEND=x11", "PATH=/usr/local/sbin:/usr/local/"..., "GDMSESSION=ubuntu", "ORIGINAL_XDG_CURRENT_DESKTOP=ubu"..., "DBUS_SESSION_BUS_ADDRESS=unix:pa"..., "GIO_LAUNCHED_DESKTOP_FILE_PID=33"..., "GIO_LAUNCHED_DESKTOP_FILE=/usr/s"..., "OLDPWD=/home/gao/wkspace", "TERM_PROGRAM=vscode", "KONSOLE_DBUS_WINDOW=/Windows/1", "_=/usr/bin/strace"]) = 0 <0.000200>
00:12:35.936746 brk(NULL)               = 0x55f1bb015000 <0.000018>
00:12:35.936803 arch_prctl(0x3001 /* ARCH_??? */, 0x7ffe38df9fa0) = -1 EINVAL (无效的参数) <0.000011>
00:12:35.936966 access("/etc/ld.so.preload", R_OK) = -1 ENOENT (没有那个文件或目录) <0.000015>
00:12:35.937023 openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3 <0.000016>
00:12:35.937070 fstat(3, {st_dev=makedev(0x8, 0x2), st_ino=14418090, st_mode=S_IFREG|0644, st_nlink=1, st_uid=0, st_gid=0, st_blksize=4096, st_blocks=160, st_size=80267, st_atime=1624289410 /* 2021-06-21T23:30:10.860018116+0800 */, st_atime_nsec=860018116, st_mtime=1624119090 /* 2021-06-20T00:11:30.461763078+0800 */, st_mtime_nsec=461763078, st_ctime=1624119090 /* 2021-06-20T00:11:30.465763100+0800 */, st_ctime_nsec=465763100}) = 0 <0.000011>
00:12:35.937127 mmap(NULL, 80267, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f6be6917000 <0.000013>
00:12:35.937165 close(3)                = 0 <0.000010>
</code></pre>
</details>




<details>
<summary>strace -p 1</summary>
<pre><code>
strace: Process 1 attached
gettid()                                = 1
epoll_wait(4, [{EPOLLIN, {u32=2342796768, u64=94805155921376}}], 189, -1) = 1
recvmsg(16, {msg_name=NULL, msg_namelen=0, msg_iov=[{iov_base="WATCHDOG=1", iov_len=4096}], msg_iovlen=1, msg_control=[{cmsg_len=28, cmsg_level=SOL_SOCKET, cmsg_type=SCM_CREDENTIALS, cmsg_data={pid=657, uid=101, gid=103}}], msg_controllen=32, msg_flags=MSG_CMSG_CLOEXEC}, MSG_TRUNC|MSG_DONTWAIT|MSG_CMSG_CLOEXEC) = 10
openat(AT_FDCWD, "/proc/657/cgroup", O_RDONLY|O_CLOEXEC) = 21
fstat(21, {st_mode=S_IFREG|0444, st_size=0, ...}) = 0
read(21, "12:cpuset:/\n11:rdma:/\n10:devices"..., 1024) = 422
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
ioctl(21, TCGETS, 0x7fff27adf6a0)       = -1 ENOTTY (对设备不适当的 ioctl 操作)
</code></pre>
</details>


