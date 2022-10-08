# FreeSWITCH Builds

FreeSWITCH 是一个比较复杂的软件，如果自己编译也是需要花费不少的时间，原来官网有提供预编译的二进制文件。现在也有，但是相对繁琐。因此考虑编译出一些预编译的二进制包，并且可以直接解压运行的形式，方便一些新手可以快速上手。

## 编译系统说明

目前底座系统基于 Debian 11(x86_64)，会使用 bundle 的形式来实现基本系统无关化。后续有时间再新增其他的平台支持。

工具链使用 GCC 10.2.1，使用 [xmake](https://xmake.io/) 来构建。

编译的 FreeSWITCH 版本如下：

- 1.10.7
- 1.8.7
- 1.6.20

### 相关库依赖

| 依赖库                                                                            | 版本                               | FS 1.10 | FS 1.8 | FS 1.6 |
| --------------------------------------------------------------------------------- | ---------------------------------- | ------- | ------ | ------ |
| [lua](https://github.com/lua/lua.git)                                             | v5.4.4                             | ✓       | ✓      | ✓      |
| [sqlite3](https://sqlite.org/)                                                    | 3.39.0+200                         | ✓       | ✓      | ✓      |
| [sofia-sip](https://github.com/freeswitch/sofia-sip.git)                          | v1.13.9                            | ✓       | ✓      | ✓      |
| [speex](https://github.com/xiph/speex.git)                                        | 1.2.1                              | ✓       | ✓      | ✓      |
| [speexdsp](https://github.com/xiph/speexdsp.git)                                  | 1.2.1                              | ✓       | ✓      | ✓      |
| [libsndfile](https://github.com/libsndfile/libsndfile.git)                        | 1.0.31                             | ✓       | ✓      | ✓      |
| [libflac](https://github.com/xiph/flac.git)                                       | 1.3.3                              | ✓       | ✓      | ✓      |
| [libopus](https://gitlab.xiph.org/xiph/opus.git)                                  | 1.3.1                              | ✓       | ✓      | ✓      |
| [libvorbis](https://gitlab.xiph.org/xiph/vorbis.git)                              | 1.3.7                              | ✓       | ✓      | ✓      |
| [libogg](https://gitlab.xiph.org/xiph/ogg.git)                                    | v1.3.4                             | ✓       | ✓      | ✓      |
| [spandsp](https://github.com/freeswitch/spandsp.git)                              | e59ca8f                            | ✓       | ✓      | ✓      |
| [libjpeg-turbo](https://github.com/libjpeg-turbo/libjpeg-turbo.git)               | 2.1.4                              | ✓       | ✓      | ✓      |
| [libtiff](https://gitlab.com/libtiff/libtiff.git)                                 | v4.4.0                             | ✓       | ✓      | ✓      |
| [libedit](https://www.thrysoee.dk/editline/)                                      | 20210910-3.1                       | ✓       | ✓      | ✓      |
| [ncurses](https://ftp.gnu.org/pub/gnu/ncurses)                                    | 6.3                                | ✓       | ✓      | ✓      |
| [ffmpeg](https://git.ffmpeg.org/ffmpeg.git)                                       | 3.2.18                             | ✓       | ✓      | ✓      |
| [x265](https://github.com/videolan/x265.git)                                      | 3.4                                | ✓       | ✓      | ✓      |
| [x264](http://git.videolan.org/git/x264.git)                                      | v2021.09.29                        | ✓       | ✓      | ✓      |
| [libcurl](https://curl.haxx.se)                                                   | 7.84.0                             | ✓       | ✓      | ✓      |
| [freetype](https://www.freetype.org)                                              | 2.12.1                             | ✓       | ✓      | ✓      |
| [libpng](https://github.com/glennrp/libpng.git)                                   | v1.6.37                            | ✓       | ✓      | ✓      |
| [libpq](https://github.com/postgres/postgres)                                     | 13.8                               | ✓       | ×      | ×      |
| [krb5](https://kerberos.org/dist/krb5)                                            | 1.19.2                             | ✓       | ×      | ×      |
| [libverto](https://github.com/latchset/libverto)                                  | 0.3.2                              | ✓       | ×      | ×      |
| [libks](https://github.com/signalwire/libks)                                      | v1.8.0                             | ✓       | ×      | ×      |
| [libuuid](https://sourceforge.net/projects/libuuid)                               | 1.0.3                              | ✓       | ✓      | ✓      |
| [mariadb-connector-c](https://github.com/mariadb-corporation/mariadb-connector-c) | 3.1.13                             | ✓       | ×      | ×      |
| [ldns](https://nlnetlabs.nl/ldns)                                                 | 1.8.3(FS1.8~FS1.10)/1.6.17(FS1.6)  | ✓       | ✓      | ✓      |
| [openssl](https://www.openssl.org)                                                | 1.1.1q(FS1.8~FS1.10)/1.0.2u(FS1.6) | ✓       | ✓      | ✓      |
| [pcre](https://www.pcre.org)                                                      | 8.45(FS1.8~FS1.10)/8.32(FS1.6)     | ✓       | ✓      | ✓      |
| [zlib](http://www.zlib.net)                                                       | v1.2.12                            | ✓       | ✓      | ✓      |

## 快速使用

为了方便可以在不同的目录下运行，因此写了一些脚本，不能直接使用 freeswitch 这个可执行文件来执行运行：

```shell
./bootstrap.sh # start FS
./stop.sh # stop FS
./cli.sh # run fs_cli
```
