# webapp.rs on Rust + WebAssembly

2018-10-04

Source:

* https://medium.com/@saschagrunert/lessons-learned-on-writing-web-applications-completely-in-rust-2080d0990287
* https://medium.com/@saschagrunert/a-web-application-completely-in-rust-6f6bdb6c4471

## Project layout

* cargo workspaces: https://doc.rust-lang.org/book/second-edition/ch14-03-cargo-workspaces.html

## Core protocol

* Cap'n Proto https://capnproto.org/ (x)
* Rust structures

* CBOR http://cbor.io/

## Front end

* yew https://github.com/DenisKolodin/yew
* yew-router https://github.com/saschagrunert/yew-router

* UIKit https://getuikit.com/
* fetch API https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

## Back end

* active-web https://github.com/actix/actix-web
* PostgreSQL https://www.postgresql.org/
* Diesel http://diesel.rs/
* r2d2 https://github.com/sfackler/r2d2
* tungstenite https://github.com/snapview/tungstenite-rs

## Deployment

* rust-musl-builder https://hub.docker.com/r/ekidd/rust-musl-builder/
