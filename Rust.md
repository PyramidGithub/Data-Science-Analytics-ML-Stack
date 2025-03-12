


## Install Rust 

```markdown 
 sudo curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -
info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /home/admins/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory is located at:

  /home/admins/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /home/admins/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /home/admins/.profile
  /home/admins/.bashrc
  /home/admins/.zshenv

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-unknown-linux-gnu
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with standard installation (default - just press enter)
2) Customize installation
3) Cancel installation
>

info: profile set to 'default'
info: default host triple is x86_64-unknown-linux-gnu

  stable-x86_64-unknown-linux-gnu installed - rustc 1.85.0 (4d91de4e4 2025-02-17)


Rust is installed now. Great!

To get started you may need to restart your current shell.
This would reload your PATH environment variable to include
Cargo's bin directory ($HOME/.cargo/bin).

To configure your current shell, you need to source
the corresponding env file under $HOME/.cargo.

This is usually done by running one of the following (note the leading DOT):
. "$HOME/.cargo/env"            # For sh/bash/zsh/ash/dash/pdksh
source "$HOME/.cargo/env.fish"  # For fish
source "$HOME/.cargo/env.nu"    # For nushell
❯ . "$HOME/.cargo/env"
```


## Setup Rust

```markdown
 install.packages("polars", repos = "https://rpolars.r-universe.dev")
Installing package into ‘/home/admins/R/x86_64-pc-linux-gnu-library/4.4’
(as ‘lib’ is unspecified)
trying URL 'https://rpolars.r-universe.dev/src/contrib/polars_0.22.1.tar.gz'
Content type 'application/gzip' length 2073109 bytes (2.0 MB)
==================================================
downloaded 2.0 MB

* installing *source* package ‘polars’ ...
** using staged installation

--------------------------- [RUST FOUND] ---------------------------
cargo 1.85.0 (d73d2caf9 2024-12-31)

rustc 1.85.0 (4d91de4e4 2025-02-17)
binary: rustc
commit-hash: 4d91de4e48198da2e33413efdcd9cd2cc0c46688
commit-date: 2025-02-17
host: x86_64-unknown-linux-gnu
release: 1.85.0
LLVM version: 19.1.7
--------------------------------------------------------------------

** libs
using C compiler: ‘gcc (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0’
rm -Rf "polars.so" "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/target/x86_64-unknown-linux-gnu/release/libr_polars.a" "entrypoint.o"
gcc -I"/usr/share/R/include" -DNDEBUG       -fpic  -g -O2 -fno-omit-frame-pointer -mno-omit-leaf-frame-pointer -ffile-prefix-map=/build/r-base-fxpJxi/r-base-4.4.3=. -fstack-protector-strong -fstack-clash-protection -Wformat -Werror=format-security -fcf-protection -fdebug-prefix-map=/build/r-base-fxpJxi/r-base-4.4.3=/usr/src/r-base-4.4.3-1.2404.0 -Wdate-time -D_FORTIFY_SOURCE=3  -c entrypoint.c -o entrypoint.o
if [ -f "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/../tools/libr_polars.a" ]; then \
	mkdir -p "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/target/x86_64-unknown-linux-gnu/release" ; \
	mv "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/../tools/libr_polars.a" "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/target/x86_64-unknown-linux-gnu/release/libr_polars.a" ; \
	exit 0; \
fi && \
if [ "true" != "true" ]; then \
	export CARGO_HOME="/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/.cargo"; \
	export CARGO_BUILD_JOBS=2; \
fi && \
	export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/snap/bin:/usr/lib/rstudio-server/bin/quarto/bin:/usr/lib/rstudio-server/bin/postback:/home/admins/.cargo/bin" && \
	cargo build --lib --manifest-path="/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/Cargo.toml" --target-dir "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/target" --target="x86_64-unknown-linux-gnu" \
		--profile="release" --features=""
   Compiling proc-macro2 v1.0.92
   Compiling unicode-ident v1.0.14
   Compiling libc v0.2.168
   Compiling autocfg v1.4.0
   Compiling shlex v1.3.0
   Compiling version_check v0.9.5
   Compiling serde v1.0.217
   Compiling cfg-if v1.0.0
   Compiling crossbeam-utils v0.8.20
   Compiling memchr v2.7.4
   Compiling once_cell v1.20.2
   Compiling rayon-core v1.12.1
   Compiling futures-core v0.3.31
   Compiling libm v0.2.11
   Compiling itoa v1.0.14
   Compiling pin-project-lite v0.2.15
   Compiling allocator-api2 v0.2.21
   Compiling stable_deref_trait v1.2.0
   Compiling futures-sink v0.3.31
   Compiling smallvec v1.13.2
   Compiling log v0.4.22
   Compiling scopeguard v1.2.0
   Compiling equivalent v1.0.1
   Compiling foldhash v0.1.3
   Compiling bytes v1.9.0
   Compiling byteorder v1.5.0
   Compiling writeable v0.5.5
   Compiling litemap v0.7.4
   Compiling futures-task v0.3.31
   Compiling futures-io v0.3.31
   Compiling pin-utils v0.1.0
   Compiling fnv v1.0.7
   Compiling ryu v1.0.18
   Compiling icu_locid_transform_data v1.5.0
   Compiling rustls-pki-types v1.10.0
   Compiling typenum v1.17.0
   Compiling untrusted v0.9.0
   Compiling icu_properties_data v1.5.0
   Compiling serde_json v1.0.135
   Compiling httparse v1.9.5
   Compiling utf16_iter v1.0.5
   Compiling parking_lot_core v0.9.10
   Compiling write16 v1.0.0
   Compiling atomic-waker v1.1.2
   Compiling utf8_iter v1.0.4
   Compiling try-lock v0.2.5
   Compiling icu_normalizer_data v1.5.0
   Compiling rustls v0.23.19
   Compiling subtle v2.6.1
   Compiling want v0.3.1
   Compiling zeroize v1.8.1
   Compiling heck v0.5.0
   Compiling percent-encoding v2.3.1
   Compiling rustversion v1.0.18
   Compiling openssl-probe v0.1.5
   Compiling iana-time-zone v0.1.61
   Compiling futures-channel v0.3.31
   Compiling tracing-core v0.1.33
   Compiling tower-service v0.3.3
   Compiling rand_core v0.6.4
   Compiling regex-syntax v0.8.5
   Compiling siphasher v0.3.11
   Compiling crc32fast v1.4.2
   Compiling rle-decode-fast v1.0.3
   Compiling target-features v0.1.6
   Compiling snap v1.1.1
   Compiling pkg-config v0.3.31
   Compiling sync_wrapper v1.0.2
   Compiling array-init-cursor v0.2.0
   Compiling ipnet v2.10.1
   Compiling crc-catalog v1.1.1
   Compiling base64 v0.22.1
   Compiling fallible-streaming-iterator v0.1.9
   Compiling libflate_lz77 v1.2.0
   Compiling mime v0.3.17
   Compiling generic-array v0.14.7
   Compiling ahash v0.8.11
   Compiling thiserror v2.0.11
   Compiling form_urlencoded v1.2.1
   Compiling adler32 v1.2.0
   Compiling rand v0.8.5
   Compiling same-file v1.0.6
   Compiling planus v0.3.1
   Compiling crc v2.1.0
   Compiling static_assertions v1.1.0
   Compiling simdutf8 v0.1.5
   Compiling syn v1.0.109
   Compiling humantime v2.1.0
   Compiling polars-utils v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling zstd-safe v7.2.1
   Compiling phf_shared v0.11.2
   Compiling rustls-native-certs v0.8.1
   Compiling rustls-pemfile v2.2.0
   Compiling polars-schema v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling rustix v0.38.42
   Compiling walkdir v2.5.0
   Compiling num-traits v0.2.19
   Compiling lock_api v0.4.12
   Compiling slab v0.4.9
   Compiling libflate v1.4.0
   Compiling polars-arrow v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling linux-raw-sys v0.4.14
   Compiling polars-compute v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling ethnum v1.5.0
   Compiling itoap v1.0.1
   Compiling dyn-clone v1.0.17
   Compiling streaming-iterator v0.1.9
   Compiling http v1.2.0
   Compiling aho-corasick v1.1.3
   Compiling strength_reduce v0.2.4
   Compiling atoi_simd v0.16.0
   Compiling fast-float2 v0.2.3
   Compiling matrixmultiply v0.3.9
   Compiling ref-cast v1.0.23
   Compiling rawpointer v0.2.1
   Compiling polars-core v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling unicode-width v0.2.0
   Compiling phf v0.11.2
   Compiling alloc-no-stdlib v2.0.4
   Compiling strum v0.26.3
   Compiling polars-ops v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling unicode-segmentation v1.12.0
   Compiling xxhash-rust v0.8.12
   Compiling alloc-stdlib v0.2.2
   Compiling adler2 v2.0.0
   Compiling hex v0.4.3
   Compiling streaming-decompression v0.1.2
   Compiling arrayvec v0.7.6
   Compiling constant_time_eq v0.3.1
   Compiling arrayref v0.3.9
   Compiling polars-plan v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling miniz_oxide v0.8.0
   Compiling home v0.5.9
   Compiling glob v0.3.1
   Compiling brotli-decompressor v4.0.1
   Compiling quote v1.0.37
   Compiling polars-pipe v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-lazy v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling libR-sys v0.6.0
   Compiling crossbeam-epoch v0.9.18
   Compiling spin v0.9.8
   Compiling phf_generator v0.11.2
   Compiling crossbeam-channel v0.5.13
   Compiling crossbeam-queue v0.3.11
   Compiling paste v1.0.15
   Compiling smartstring v1.0.1
   Compiling polars v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling phf_codegen v0.11.2
   Compiling sqlparser v0.52.0
   Compiling fastrand v2.3.0
   Compiling extendr-api v0.6.0 (https://github.com/extendr/extendr?rev=1895bfc8ee22347665900caa0e48da4f0b13232f#1895bfc8)
   Compiling r-polars v0.45.0 (/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust)
   Compiling lazy_static v1.5.0
   Compiling indenter v0.3.3
   Compiling state v0.6.0
   Compiling syn v2.0.90
   Compiling jobserver v0.1.32
   Compiling castaway v0.2.3
   Compiling crossbeam-deque v0.8.5
   Compiling unicode-reverse v1.0.9
   Compiling getrandom v0.2.15
   Compiling mio v1.0.3
   Compiling socket2 v0.5.8
   Compiling memmap2 v0.9.5
   Compiling sysinfo v0.32.1
   Compiling cc v1.2.3
   Compiling uuid v1.11.0
   Compiling nanorand v0.7.0
   Compiling parking_lot v0.12.3
   Compiling regex-automata v0.4.9
   Compiling flume v0.11.1
   Compiling http-body v1.0.1
   Compiling atoi v2.0.0
   Compiling float-cmp v0.10.0
   Compiling num-integer v0.1.46
   Compiling num-complex v0.4.6
   Compiling argminmax v0.6.2
   Compiling brotli v7.0.0
   Compiling crypto-common v0.1.6
   Compiling block-buffer v0.10.4
   Compiling digest v0.10.7
   Compiling md-5 v0.10.6
   Compiling cmake v0.1.52
   Compiling ndarray v0.16.1
   Compiling ring v0.17.8
   Compiling psm v0.1.24
   Compiling zstd-sys v2.0.13+zstd.1.5.6
   Compiling stacker v0.1.17
   Compiling lz4-sys v1.11.1+lz4-1.10.0
   Compiling blake3 v1.5.5
   Compiling jemalloc-sys v0.5.4+5.3.0-patched
   Compiling libz-ng-sys v1.1.20
   Compiling regex v1.11.1
   Compiling parse-zoneinfo v0.3.1
   Compiling chrono-tz-build v0.4.0
   Compiling chrono-tz v0.10.0
   Compiling synstructure v0.13.1
   Compiling multiversion-macros v0.7.4
   Compiling serde_derive v1.0.217
   Compiling zerofrom-derive v0.1.5
   Compiling yoke-derive v0.7.5
   Compiling zerovec-derive v0.10.3
   Compiling zerocopy-derive v0.7.35
   Compiling displaydoc v0.2.5
   Compiling futures-macro v0.3.31
   Compiling tokio-macros v2.4.0
   Compiling icu_provider_macros v1.5.0
   Compiling tracing-attributes v0.1.28
   Compiling async-trait v0.1.83
   Compiling snafu-derive v0.8.5
   Compiling thiserror-impl v2.0.11
   Compiling bytemuck_derive v1.8.0
   Compiling strum_macros v0.26.4
   Compiling ref-cast-impl v1.0.23
   Compiling async-stream-impl v0.3.6
   Compiling recursive-proc-macro-impl v0.1.1
   Compiling enum_dispatch v0.3.13
   Compiling extendr-macros v0.6.0 (https://github.com/extendr/extendr?rev=1895bfc8ee22347665900caa0e48da4f0b13232f#1895bfc8)
   Compiling recursive v0.1.1
   Compiling async-stream v0.3.6
   Compiling tokio v1.42.0
   Compiling multiversion v0.7.4
   Compiling zerocopy v0.7.35
   Compiling futures-util v0.3.31
   Compiling zerofrom v0.1.5
   Compiling yoke v0.7.5
   Compiling bytemuck v1.20.0
   Compiling tracing v0.1.41
   Compiling zerovec v0.10.4
   Compiling snafu v0.8.5
   Compiling ppv-lite86 v0.2.20
   Compiling rand_chacha v0.3.1
   Compiling rand_distr v0.4.3
   Compiling tinystr v0.7.6
   Compiling icu_collections v1.5.0
   Compiling icu_locid v1.5.0
   Compiling lz4 v1.28.0
   Compiling futures-executor v0.3.31
   Compiling http-body-util v0.1.2
   Compiling futures v0.3.31
   Compiling polars-parquet-format v0.1.0
   Compiling icu_provider v1.5.0
   Compiling icu_locid_transform v1.5.0
   Compiling rustls-webpki v0.102.8
   Compiling icu_properties v1.5.1
   Compiling either v1.13.0
   Compiling bitflags v2.6.0
   Compiling chrono v0.4.39
   Compiling serde_urlencoded v0.7.1
   Compiling quick-xml v0.36.2
   Compiling polars-arrow-format v0.1.0
   Compiling compact_str v0.8.0
   Compiling bincode v1.3.3
   Compiling raw-cpuid v11.2.0
   Compiling rayon v1.10.0
   Compiling itertools v0.13.0
   Compiling flate2 v1.0.35
   Compiling tokio-util v0.7.13
   Compiling icu_normalizer v1.5.0
   Compiling now v0.1.3
   Compiling idna_adapter v1.2.0
   Compiling idna v1.0.3
   Compiling url v2.5.4
   Compiling zstd v0.13.2
   Compiling crossterm v0.28.1
   Compiling fs4 v0.12.0
   Compiling tempfile v3.14.0
   Compiling ipc-channel v0.18.3
   Compiling comfy-table v7.1.3
   Compiling hashbrown v0.15.2
   Compiling hashbrown v0.14.5
   Compiling tokio-rustls v0.26.1
   Compiling indexmap v2.7.0
   Compiling halfbrown v0.2.5
   Compiling value-trait v0.10.1
   Compiling h2 v0.4.7
   Compiling avro-schema v0.3.0
   Compiling simd-json v0.14.3
   Compiling jsonpath_lib_polars_vendor v0.0.1
   Compiling hyper v1.5.1
   Compiling hyper-util v0.1.10
   Compiling hyper-rustls v0.27.3
   Compiling reqwest v0.12.9
   Compiling object_store v0.11.1
   Compiling jemallocator v0.5.4
   Compiling polars-error v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-row v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-json v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-parquet v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-time v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-io v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-expr v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-mem-engine v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
   Compiling polars-sql v0.45.1 (https://github.com/pola-rs/polars.git?rev=e83e7d47cda3475b84a7add7838d349779143cc7#e83e7d47)
    Finished `release` profile [optimized] target(s) in 7m 50s
if [ "true" != "true" ]; then \
	rm -Rf "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/.cargo" "/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/target/x86_64-unknown-linux-gnu/release/build"; \
fi
gcc -shared -L/usr/lib/R/lib -Wl,-Bsymbolic-functions -flto=auto -ffat-lto-objects -Wl,-z,relro -o polars.so entrypoint.o -L/tmp/RtmpDuF0pR/R.INSTALL3611ca29de69dd/polars/src/rust/target/x86_64-unknown-linux-gnu/release -lr_polars -lrt -L/usr/lib/R/lib -lR
/usr/bin/ld: warning: 4f9a91766097c4c5-x86_64.o: missing .note.GNU-stack section implies executable stack
/usr/bin/ld: NOTE: This behaviour is deprecated and will be removed in a future version of the linker
installing to /home/admins/R/x86_64-pc-linux-gnu-library/4.4/00LOCK-polars/00new/polars/libs
** R
** inst
** byte-compile and prepare package for lazy loading
** help
*** installing help indices
** building package indices
** installing vignettes
** testing if installed package can be loaded from temporary location
** checking absolute paths in shared objects and dynamic libraries
** testing if installed package can be loaded from final location
** testing if installed package keeps a record of temporary installation path
* DONE (polars)

The downloaded source packages are in
	‘/tmp/RtmpsAoB5U/downloaded_packages’

```
