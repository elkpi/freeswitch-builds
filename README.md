# FreeSWITCH Builds

FreeSWITCH 是一个比较复杂的软件，如果自己编译也是需要花费不少的时间，原来官网有提供预编译的二进制文件。现在也有，但是相对繁琐。因此考虑编译出一些预编译的二进制包，并且可以直接解压运行的形式，方便一些新手可以快速上手。

## 编译系统说明

目前底座系统基于 Debian 12(x86_64)，会使用 bundle 的形式来实现基本系统无关化。后续有时间再新增其他的平台支持。

工具链使用 GCC 12.2.0，使用 [xmake](https://xmake.io/) 来构建。

编译的 FreeSWITCH 版本如下：

- 1.10.10
- 1.10.7
- 1.8.7
- 1.6.20

### 相关库依赖

| 依赖库                                                                            | 版本                                 | FS 1.10 | FS 1.8  | FS 1.6  |
| --------------------------------------------------------------------------------- | ------------------------------------ | ------- | ------- | ------- |
| [ffmpeg](https://git.ffmpeg.org/ffmpeg.git)                                       | 3.2.18                               | ✓       | ✓       | ✓       |
| [freetype](https://www.freetype.org)                                              | 2.13.1                               | ✓       | ✓       | ✓       |
| [krb5](https://kerberos.org/dist/krb5)                                            | 1.19.2                               | ✓       | ×       | ×       |
| [lame](https://lame.sourceforge.io/)                                              | 3.100                                | ✓       | ✓       | ✓       |
| [ldns](https://nlnetlabs.nl/ldns)                                                 | 1.8.3(FS1.8~FS1.10)/1.6.17(FS1.6)    | ✓       | ✓       | ✓       |
| [libcurl](https://curl.haxx.se)                                                   | 8.0.1                                | ✓       | ✓       | ✓       |
| [libedit](https://www.thrysoee.dk/editline/)                                      | 20210910-3.1                         | ✓       | ✓       | ✓       |
| [libflac](https://github.com/xiph/flac.git)                                       | 1.4.3                                | ✓       | ✓       | ✓       |
| [libjpeg-turbo](https://github.com/libjpeg-turbo/libjpeg-turbo.git)               | 2.1.4                                | ✓       | ✓       | ✓       |
| [libks](https://github.com/signalwire/libks)                                      | v1.8.3                               | ✓       | ×       | ×       |
| [libogg](https://gitlab.xiph.org/xiph/ogg.git)                                    | v1.3.4                               | ✓       | ✓       | ✓       |
| [libopus](https://gitlab.xiph.org/xiph/opus.git)                                  | 1.4                                  | ✓       | ✓       | ✓       |
| [libpng](https://github.com/glennrp/libpng.git)                                   | v1.6.40                              | ✓       | ✓       | ✓       |
| [libpq](https://github.com/postgres/postgres)                                     | 13.8                                 | ✓       | ×       | ×       |
| [libshout](https://icecast.org/download/)                                         | 2.4.6                                | ✓       | ✓       | ✓       |
| [libsndfile](https://github.com/libsndfile/libsndfile.git)                        | 1.0.31                               | ✓       | ✓       | ✓       |
| [libtiff](https://gitlab.com/libtiff/libtiff.git)                                 | v4.4.0                               | ✓       | ✓       | ✓       |
| [libuuid](https://sourceforge.net/projects/libuuid)                               | 1.0.3                                | ✓       | ✓       | ✓       |
| [libverto](https://github.com/latchset/libverto)                                  | 0.3.2                                | ✓       | ×       | ×       |
| [libvorbis](https://gitlab.xiph.org/xiph/vorbis.git)                              | 1.3.7                                | ✓       | ✓       | ✓       |
| [lua](https://github.com/lua/lua.git)                                             | v5.4.6                               | ✓       | ✓       | ✓       |
| [mariadb-connector-c](https://github.com/mariadb-corporation/mariadb-connector-c) | 3.3.4                                | ✓       | ×       | ×       |
| [mpg123](https://www.mpg123.de/)                                                  | 1.30.2                               | ✓       | ✓       | ✓       |
| [ncurses](https://ftp.gnu.org/pub/gnu/ncurses)                                    | 6.4                                  | ✓       | ✓       | ✓       |
| [opencore-amr](https://sourceforge.net/projects/opencore-amr/)                    | 0.1.6                                | ✓       | ✓       | ✓       |
| [openh264](https://github.com/cisco/openh264)                                     | v2.1.1                               | ✓       | ✓       | ✓       |
| [openssl](https://www.openssl.org)                                                | 1.1.1-t(FS1.8~FS1.10)/1.0.2-u(FS1.6) | ✓       | ✓       | ✓       |
| [pcre](https://www.pcre.org)                                                      | 8.45(FS1.8~FS1.10)/8.32(FS1.6)       | ✓       | ✓       | ✓       |
| [sofia-sip](https://github.com/freeswitch/sofia-sip.git)                          | v1.13.16                             | ✓       | builtin | builtin |
| [spandsp](https://github.com/freeswitch/spandsp.git)                              | 56795ba                              | ✓       | ✓       | ✓       |
| [speex](https://github.com/xiph/speex.git)                                        | 1.2.1                                | ✓       | ✓       | ✓       |
| [speexdsp](https://github.com/xiph/speexdsp.git)                                  | 1.2.1                                | ✓       | ✓       | ✓       |
| [sqlite3](https://sqlite.org/)                                                    | 3.39.0+200                           | ✓       | ✓       | ✓       |
| [vo-amrwbenc](https://sourceforge.net/projects/opencore-amr/)                     | 0.1.3                                | ✓       | ✓       | ✓       |
| [x264](http://git.videolan.org/git/x264.git)                                      | 3fd9e89                              | ✓       | ✓       | ✓       |
| [x265](https://github.com/videolan/x265.git)                                      | 3.4                                  | ✓       | ✓       | ✓       |
| [zlib](http://www.zlib.net)                                                       | v1.3                                 | ✓       | ✓       | ✓       |

## 快速使用

为了方便可以在不同的目录下运行，因此写了一些脚本，不能直接使用 freeswitch 这个可执行文件来执行运行：

```shell
./bootstrap.sh # start FS
./stop.sh # stop FS
./cli.sh # run fs_cli
```

### 模块说明

| 模块              | 备注 |
| ----------------- | ---- |
| amr               |      |
| amrwb             |      |
| av                |      |
| b64               |      |
| cdr_csv           |      |
| cdr_sqlite        |      |
| commands          |      |
| conference        |      |
| console           |      |
| curl              |      |
| db                |      |
| dialplan_asterisk |      |
| dialplan_xml      |      |
| dptools           |      |
| enum              |      |
| esf               |      |
| event_socket      |      |
| expr              |      |
| fifo              |      |
| fsv               |      |
| g723_1            |      |
| g729              |      |
| h26x              |      |
| openh264          |      |
| hash              |      |
| httapi            |      |
| local_stream      |      |
| logfile           |      |
| loopback          |      |
| lua               |      |
| native_file       |      |
| opus              |      |
| png               |      |
| rtc               |      |
| say_en            |      |
| skinny            |      |
| sms               |      |
| sndfile           |      |
| shout             |      |
| sofia             |      |
| spandsp           |      |
| syslog            |      |
| tone_stream       |      |
| valet_parking     |      |
| verto             |      |
| voicemail         |      |
| xml_cdr           |      |
| xml_rpc           |      |
| xml_scgi          |      |
