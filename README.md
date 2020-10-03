# lwt-ssl

Fatal error: exception (Failure "No SSL or TLS support compiled into Conduit") を調べる

https://github.com/mirage/ocaml-cohttp

## dev

```sh
dune exec ./get.exe
```

## memo

```sh
dune init exe get --libs cohttp,lwt,cohttp-lwt-unix
```
