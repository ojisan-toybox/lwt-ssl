# lwt-ssl

Fatal error: exception (Failure "No SSL or TLS support compiled into Conduit") を調べる

https://github.com/mirage/ocaml-cohttp

## dev

```sh
# これがないとopam install tls に失敗する（エラーログは下記）
brew install gmp pkg-config

# https へアクセスするときに手元で必要になるライブラリ
opam install tls

dune exec ./get.exe
```

## memo

```sh
dune init exe get --libs cohttp,lwt,cohttp-lwt-unix
```

## errorlog

```
~/Documents/project/toybox/lwt-ssl main* 6s
❯ opam install tls
The following actions will be performed:
  ∗ install   conf-gmp          2      [required by conf-gmp-powm-sec, zarith]
  ∗ install   conf-pkg-config   1.3    [required by mirage-crypto]
  ∗ install   zarith            1.10   [required by mirage-crypto-pk]
  ∗ install   conf-gmp-powm-sec 2      [required by mirage-crypto-pk]
  ∗ install   mirage-crypto     0.8.5  [required by tls]
  ∗ install   asn1-combinators  0.2.3  [required by x509]
  ∗ install   mirage-crypto-rng 0.8.5  [required by tls]
  ∗ install   hkdf              1.0.4  [required by tls]
  ∗ install   mirage-crypto-pk  0.8.5  [required by tls]
  ∗ install   x509              0.11.2 [required by tls]
  ∗ install   tls               0.12.5
  ↻ recompile conduit-lwt-unix  2.2.2  [uses tls]
  ↻ recompile cohttp-lwt-unix   2.5.4  [uses conduit-lwt-unix]
===== ∗ 11   ↻ 2 =====
Do you want to continue? [Y/n] Y

<><> Gathering sources ><><><><><><><><><><><><><><><><><><><><><><><><><><>  🐫
[asn1-combinators.0.2.3] found in cache
[cohttp-lwt-unix.2.5.4] found in cache
[conduit-lwt-unix.2.2.2] found in cache
[hkdf.1.0.4] found in cache
[mirage-crypto.0.8.5] found in cache
[mirage-crypto-pk.0.8.5] found in cache
[mirage-crypto-rng.0.8.5] found in cache
[tls.0.12.5] found in cache
[x509.0.11.2] found in cache
[zarith.1.10] found in cache

<><> Processing actions <><><><><><><><><><><><><><><><><><><><><><><><><><>  🐫
[ERROR] The compilation of conf-pkg-config failed at "/Users/ojisan/.opam/opam-init/hooks/sandbox.sh build pkg-config --help".
[ERROR] The compilation of conf-gmp failed at "/Users/ojisan/.opam/opam-init/hooks/sandbox.sh build sh -exc cc -c $CFLAGS
        -I/opt/local/include -I/usr/local/include test.c".

#=== ERROR while compiling conf-pkg-config.1.3 ================================#
# context     2.0.7 | macos/x86_64 | ocaml-base-compiler.4.11.1 | https://opam.ocaml.org#e8fe3ce4
# path        ~/.opam/default/.opam-switch/build/conf-pkg-config.1.3
# command     ~/.opam/opam-init/hooks/sandbox.sh build pkg-config --help
# exit-code   71
# env-file    ~/.opam/log/conf-pkg-config-10737-e0259d.env
# output-file ~/.opam/log/conf-pkg-config-10737-e0259d.out
### output ###
# sandbox-exec: execvp() of 'pkg-config' failed: No such file or directory


#=== ERROR while compiling conf-gmp.2 =========================================#
# context     2.0.7 | macos/x86_64 | ocaml-base-compiler.4.11.1 | https://opam.ocaml.org#e8fe3ce4
# path        ~/.opam/default/.opam-switch/build/conf-gmp.2
# command     ~/.opam/opam-init/hooks/sandbox.sh build sh -exc cc -c $CFLAGS -I/opt/local/include -I/usr/local/include test.c
# exit-code   1
# env-file    ~/.opam/log/conf-gmp-10737-a7c577.env
# output-file ~/.opam/log/conf-gmp-10737-a7c577.out
### output ###
# + cc -c -I/opt/local/include -I/usr/local/include test.c
# test.c:1:10: fatal error: 'gmp.h' file not found
# #include <gmp.h>
#          ^~~~~~~
# 1 error generated.



<><> Error report <><><><><><><><><><><><><><><><><><><><><><><><><><><><><>  🐫
┌─ The following actions failed
│ λ build conf-gmp        2
│ λ build conf-pkg-config 1.3
└─
╶─ No changes have been performed

The packages you requested declare the following system dependencies. Please make sure they are installed before retrying:
    gmp pkg-config

```

## refs

- https://dev.to/idkjs/the-postman-rides-ocaml-part-2-58p7
