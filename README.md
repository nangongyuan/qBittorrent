qBittorrent - A BitTorrent client in Qt
------------------------------------------

[![GitHub Actions CI Status](https://github.com/qbittorrent/qBittorrent/actions/workflows/ci_ubuntu.yaml/badge.svg)](https://github.com/qbittorrent/qBittorrent/actions)
[![Coverity Status](https://scan.coverity.com/projects/5494/badge.svg)](https://scan.coverity.com/projects/5494)
********************************
### Description:
qBittorrent is a bittorrent client programmed in C++ / Qt that uses
libtorrent (sometimes called libtorrent-rasterbar) by Arvid Norberg.

It aims to be a good alternative to all other bittorrent clients
out there. qBittorrent is fast, stable and provides unicode
support as well as many features.

The free [IP to Country Lite database](https://db-ip.com/db/download/ip-to-country-lite) by [DB-IP](https://db-ip.com/) is used for resolving the countries of peers. The database is licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

### Installation:

Refer to the [INSTALL](INSTALL) file.

### Public key:
Starting from v3.3.4 all source tarballs and binaries are signed.<br />
The key currently used is 4096R/[5B7CC9A2](https://pgp.mit.edu/pks/lookup?op=get&search=0x6E4A2D025B7CC9A2) with fingerprint `D8F3DA77AAC6741053599C136E4A2D025B7CC9A2`.<br />
You can also download it from [here](https://github.com/qbittorrent/qBittorrent/raw/master/5B7CC9A2.asc).<br />
**PREVIOUSLY** the following key was used to sign the v3.3.4 source tarballs and v3.3.4 Windows installer **only**: 4096R/[520EC6F6](https://pgp.mit.edu/pks/lookup?op=get&search=0xA1ACCAE4520EC6F6) with fingerprint `F4A5FD201B117B1C2AB590E2A1ACCAE4520EC6F6`.<br />

### Misc:
For more information please visit:
https://www.qbittorrent.org

or our wiki here:
https://wiki.qbittorrent.org

Use the forum for troubleshooting before reporting bugs:
https://forum.qbittorrent.org

Please report any bug (or feature request) to:
https://bugs.qbittorrent.org

Official IRC channel:
[#qbittorrent on irc.libera.chat](ircs://irc.libera.chat:6697/qbittorrent)

------------------------------------------
sledgehammer999 \<sledgehammer999@qbittorrent.org\>







# 环境配置

安装VS2022
安装vcpkg


cmake -B build -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE="E:\vcpkg\scripts\buildsystems\vcpkg.cmake" -DVCPKG_TARGET_TRIPLET="x64-windows-static-release" -DMSVC_RUNTIME_DYNAMIC=OFF

vcpkg.cmake根据目录自己修改
-DVCPKG_TARGET_TRIPLET="x64-windows-static-release" vcpkg安装的版本，库会被安装在build/vcpkg_installed目录
-DCMAKE_BUILD_TYPE=Release 编译release版本

cmake生成vs的解决方案之后，用vs打开编译


5>H:\qBittorrent\src\app\stacktrace.cpp(31,10): error C1083: 无法打开包括文件: “boost/stacktrace.hpp”: No such file or directory
需要安装boost-stacktrace，在vcpkg.json中添加boost-stacktrace
或者直接注释

~~~
#include "stacktrace.h"

//#include <boost/stacktrace.hpp>

std::string getStacktrace()
{
    //return boost::stacktrace::to_string(boost::stacktrace::stacktrace());
    return "";
}
~~~



qwindows.lib(qwindowsintegration.cpp.obj) : error LNK2038: 检测到“_COROUTINE_ABI”的不匹配项: 值“1”不匹配值“2”(qbt_base.lib(sessionimpl.obj) 中)
Qt 与 STL 协程似乎存在冲突
_ALLOW_COROUTINE_ABI_MISMATCH 预处理器变量之后，现在它可以编译了

