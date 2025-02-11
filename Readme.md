### 编译 Nginx-QUIC

进入到nginx-quic目录

```shell
auto/configure `nginx -V 2>&1 | sed "s/ \-\-/ \\\ \n\t--/g" | grep "\-\-" | grep -ve opt= -e param= -e build=` \
                   --build=nginx-quic --with-debug --with-http_v2_module \
                   --with-http_v3_module --with-stream_quic_module \
                   --with-cc-opt="-I../boringssl/include" --with-ld-opt="-L../boringssl/build/ssl -L../boringssl/build/crypto"
```

### 证书

```shell
https://www.cnblogs.com/dreasky/p/13497210.html

验证HTTPS
 /usr/local/bin/curl -k  --alt-svc altsvc.cache https://test.com:4433
```



### 编译支持QUIC 的CURL

进入到curl目录

```shell
# 可以参考 https://github.com/curl/curl/blob/master/docs/HTTP3.md
```

```shell
Build Linux (with quictls fork of OpenSSL)
Build msh3:

 % git clone --depth 1 --recursive https://github.com/nibanks/msh3
 % cd msh3 && mkdir build && cd build
 % cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
 % cmake --build .
 % cmake --install .
Build curl:

 % git clone https://github.com/curl/curl
 % cd curl
 % autoreconf -fi
 % ./configure LDFLAGS="-Wl,-rpath,/usr/local/lib" --with-msh3=/usr/local --with-openssl
 % make
 % make install
Run from /usr/local/bin/curl.
```



### 测试脚本

```shell
/usr/local/bin/curl --http3 -k --alt-svc altsvc.cache https://test.com
```



### 参考资料

```
https://mytechshares.com/2022/02/14/nginx-blog-quic/
https://nestealin.com/ce9634bf/
```

