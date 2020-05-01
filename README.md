# nginx-ssllabs-tlsv1.3
Get A+ and score 100/100/100/100 on sslabs tlsv1.3


For this i'm use SSL from Letsencrypt

1) Generate ssl certificate 4096 bit

2) Generate Key exchange 4096 bit (for get 100% score of Key exchange) : 
      ```
       openssl dhparam -out dhparams.pem 4096 
      ```

3) Download nginx from source http://nginx.org/en/download.html

5) Download OpenSSL from source https://www.openssl.org/source/

5) Edit ssl.h (openssl_src/include/openssl/ssl.h) on openssl folder source which already downloaded

6) Go to line 178 & 181 and remove TLS_AES_128_GCM_SHA256 (Based on https://github.com/ssllabs/research/wiki/SSL-Server-Rating-Guide#cipher-strength , 128 bit keys will scored 90%, so you need removed it if you want get 100% Cipher strength.). code like this :
      ```C
      #define TLS_DEFAULT_CIPHERSUITES "TLS_AES_256_GCM_SHA384:" \
                                       "TLS_CHACHA20_POLY1305_SHA256:" \
                                       "TLS_AES_128_GCM_SHA256"
      #else
      #define TLS_DEFAULT_CIPHERSUITES "TLS_AES_256_GCM_SHA384:" \
                                       "TLS_AES_128_GCM_SHA256"
      #endif
      ```
      
      edit to like this :
 
      ```C
      #define TLS_DEFAULT_CIPHERSUITES "TLS_AES_256_GCM_SHA384:" \
                                       "TLS_CHACHA20_POLY1305_SHA256"
      #else
      #define TLS_DEFAULT_CIPHERSUITES "TLS_AES_256_GCM_SHA384"
      #endif
      ```
      


7) Compile nginx with openssl which you're downloaded :
      ```
      ./Configure .... 
                  ....
                  --with-openssl=openssl_src
                  
      make && make install
      ````

8) You're done , you get A+ score with 100/100/100/100 :)


## Based on https://github.com/ssllabs/research/wiki/SSL-Server-Rating-Guide
* Protocol : min TLSv1.2 for get 100%
* Key exchange : min 4096 bit for get 100%
* Cipher strenght : >= 256 bit for get 100%

## My Results : [ssllabs](https://www.ssllabs.com/ssltest/analyze.html?d=www.infectingthe.world)

![www.infecthingthe.world](https://github.com/0xfffb4dc0d3/nginx-ssllabs-tlsv1.3/blob/master/ssllabs.png)

## A+ with score 100/100/100/100 TLSv1.3 :tada:

<a href='https://ko-fi.com/L3L41N1PZ' target='_blank'><img height='50' style='border:0px;height:50px;' src='https://cdn.ko-fi.com/cdn/kofi5.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
