
Build A0CC compiler for Spack Pkg. Mgmt System


#  required because aocc@0.23.0+license-agreed requested explicitly 

```markdown
      
 spack install aocc +license-agreed
[+] /usr (external glibc-2.39-2n42x2z3tkws4hno5t2a3olgv2sw47zg)
==> Installing gcc-runtime-13.3.0-o2i4t72frnbr7tyckcl2pdcpflvo5kff [2/20]
==> No binary for gcc-runtime-13.3.0-o2i4t72frnbr7tyckcl2pdcpflvo5kff found: installing from source
==> No patches needed for gcc-runtime
==> gcc-runtime: Executing phase: 'install'
==> gcc-runtime: Successfully installed gcc-runtime-13.3.0-o2i4t72frnbr7tyckcl2pdcpflvo5kff
  Stage: 0.00s.  Install: 2.75s.  Post-install: 0.06s.  Total: 2.89s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/gcc-runtime-13.3.0-o2i4t72frnbr7tyckcl2pdcpflvo5kff
==> Installing gmake-4.4.1-wbcsdfjkbkej32ctx65dp4bma7emlatt [3/20]
==> No binary for gmake-4.4.1-wbcsdfjkbkej32ctx65dp4bma7emlatt found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/dd/dd16fb1d67bfab79a72f5e8390735c49e3e8e70b4945a15ab1f81ddb78658fb3.tar.gz
==> No patches needed for gmake
==> gmake: Executing phase: 'install'
==> gmake: Successfully installed gmake-4.4.1-wbcsdfjkbkej32ctx65dp4bma7emlatt
  Stage: 0.51s.  Install: 38.23s.  Post-install: 0.03s.  Total: 38.86s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/gmake-4.4.1-wbcsdfjkbkej32ctx65dp4bma7emlatt
==> Installing libiconv-1.17-nnzgj3yo6jystvu5o6ec7fu6paxxad66 [4/20]
==> No binary for libiconv-1.17-nnzgj3yo6jystvu5o6ec7fu6paxxad66 found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/8f/8f74213b56238c85a50a5329f77e06198771e70dd9a739779f4c02f65d971313.tar.gz
==> No patches needed for libiconv
==> libiconv: Executing phase: 'autoreconf'
==> libiconv: Executing phase: 'configure'
==> libiconv: Executing phase: 'build'
==> libiconv: Executing phase: 'install'
==> libiconv: Successfully installed libiconv-1.17-nnzgj3yo6jystvu5o6ec7fu6paxxad66
  Stage: 0.74s.  Autoreconf: 0.00s.  Configure: 33.83s.  Build: 23.48s.  Install: 1.53s.  Post-install: 0.11s.  Total: 1m 0.01s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/libiconv-1.17-nnzgj3yo6jystvu5o6ec7fu6paxxad66
==> Installing zstd-1.5.6-nvwj5ycowigt5zafqp47yrn5pvqdb4z2 [5/20]
==> No binary for zstd-1.5.6-nvwj5ycowigt5zafqp47yrn5pvqdb4z2 found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/30/30f35f71c1203369dc979ecde0400ffea93c27391bfd2ac5a9715d2173d92ff7.tar.gz
==> No patches needed for zstd
==> zstd: Executing phase: 'edit'
==> zstd: Executing phase: 'build'
==> zstd: Executing phase: 'install'
==> zstd: Successfully installed zstd-1.5.6-nvwj5ycowigt5zafqp47yrn5pvqdb4z2
  Stage: 0.76s.  Edit: 0.00s.  Build: 0.00s.  Install: 45.57s.  Post-install: 0.04s.  Total: 46.58s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/zstd-1.5.6-nvwj5ycowigt5zafqp47yrn5pvqdb4z2
==> Installing libsigsegv-2.14-5cquzqkndsokzsgmymuqvlobxlwey6m2 [6/20]
==> No binary for libsigsegv-2.14-5cquzqkndsokzsgmymuqvlobxlwey6m2 found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/cd/cdac3941803364cf81a908499beb79c200ead60b6b5b40cad124fd1e06caa295.tar.gz
==> No patches needed for libsigsegv
==> libsigsegv: Executing phase: 'autoreconf'
==> libsigsegv: Executing phase: 'configure'
==> libsigsegv: Executing phase: 'build'
==> libsigsegv: Executing phase: 'install'
==> libsigsegv: Successfully installed libsigsegv-2.14-5cquzqkndsokzsgmymuqvlobxlwey6m2
  Stage: 0.40s.  Autoreconf: 0.00s.  Configure: 12.02s.  Build: 2.29s.  Install: 0.27s.  Post-install: 0.03s.  Total: 15.30s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/libsigsegv-2.14-5cquzqkndsokzsgmymuqvlobxlwey6m2
==> Installing pkgconf-2.3.0-zb5q7gdxhaxej7j47fx5pqrwycn4f574 [7/20]
==> No binary for pkgconf-2.3.0-zb5q7gdxhaxej7j47fx5pqrwycn4f574 found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/3a/3a9080ac51d03615e7c1910a0a2a8df08424892b5f13b0628a204d3fcce0ea8b.tar.xz
==> No patches needed for pkgconf
==> pkgconf: Executing phase: 'autoreconf'
==> pkgconf: Executing phase: 'configure'
==> pkgconf: Executing phase: 'build'
==> pkgconf: Executing phase: 'install'
==> pkgconf: Successfully installed pkgconf-2.3.0-zb5q7gdxhaxej7j47fx5pqrwycn4f574
  Stage: 0.96s.  Autoreconf: 0.01s.  Configure: 9.14s.  Build: 2.73s.  Install: 0.43s.  Post-install: 0.04s.  Total: 13.62s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/pkgconf-2.3.0-zb5q7gdxhaxej7j47fx5pqrwycn4f574
==> Installing xz-5.4.6-bkce4424a5mcpt7wawxraof6qhcmwl63 [8/20]
==> No binary for xz-5.4.6-bkce4424a5mcpt7wawxraof6qhcmwl63 found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/91/913851b274e8e1d31781ec949f1c23e8dbcf0ecf6e73a2436dc21769dd3e6f49.tar.bz2
==> No patches needed for xz
==> xz: Executing phase: 'autoreconf'
==> xz: Executing phase: 'configure'
==> xz: Executing phase: 'build'
==> xz: Executing phase: 'install'
==> xz: Successfully installed xz-5.4.6-bkce4424a5mcpt7wawxraof6qhcmwl63
  Stage: 2.00s.  Autoreconf: 0.00s.  Configure: 23.75s.  Build: 8.31s.  Install: 3.44s.  Post-install: 0.11s.  Total: 37.90s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/xz-5.4.6-bkce4424a5mcpt7wawxraof6qhcmwl63
==> Installing zlib-ng-2.2.3-cex7hbny26bnoaev7sfu6f2ab6m6g5kh [9/20]
==> No binary for zlib-ng-2.2.3-cex7hbny26bnoaev7sfu6f2ab6m6g5kh found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/f2/f2fb245c35082fe9ea7a22b332730f63cf1d42f04d84fe48294207d033cba4dd.tar.gz
==> No patches needed for zlib-ng
==> zlib-ng: Executing phase: 'autoreconf'
==> zlib-ng: Executing phase: 'configure'
==> zlib-ng: Executing phase: 'build'
==> zlib-ng: Executing phase: 'install'
==> zlib-ng: Successfully installed zlib-ng-2.2.3-cex7hbny26bnoaev7sfu6f2ab6m6g5kh
  Stage: 0.40s.  Autoreconf: 0.00s.  Configure: 12.32s.  Build: 2.92s.  Install: 14.44s.  Post-install: 0.02s.  Total: 30.40s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/zlib-ng-2.2.3-cex7hbny26bnoaev7sfu6f2ab6m6g5kh
==> Installing diffutils-3.10-oxz3t6fzbhfxww535brhvyfcvs5vwjsy [10/20]
==> No binary for diffutils-3.10-oxz3t6fzbhfxww535brhvyfcvs5vwjsy found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/90/90e5e93cc724e4ebe12ede80df1634063c7a855692685919bfe60b556c9bd09e.tar.xz
==> No patches needed for diffutils
==> diffutils: Executing phase: 'autoreconf'
==> diffutils: Executing phase: 'configure'
==> diffutils: Executing phase: 'build'
==> diffutils: Executing phase: 'install'
==> diffutils: Successfully installed diffutils-3.10-oxz3t6fzbhfxww535brhvyfcvs5vwjsy
  Stage: 0.59s.  Autoreconf: 0.00s.  Configure: 56.82s.  Build: 3.39s.  Install: 1.37s.  Post-install: 0.09s.  Total: 1m 2.55s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/diffutils-3.10-oxz3t6fzbhfxww535brhvyfcvs5vwjsy
==> Installing ncurses-6.5-7tikjbf5ohs2uoa7wsw32ewbrw5xpphq [11/20]
==> No binary for ncurses-6.5-7tikjbf5ohs2uoa7wsw32ewbrw5xpphq found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/13/136d91bc269a9a5785e5f9e980bc76ab57428f604ce3e5a5a90cebc767971cc6.tar.gz
==> Applied patch /home/admins/spack/var/spack/repos/builtin/packages/ncurses/rxvt_unicode_6_4.patch
==> ncurses: Executing phase: 'autoreconf'
==> ncurses: Executing phase: 'configure'
==> ncurses: Executing phase: 'build'
==> ncurses: Executing phase: 'install'
==> ncurses: Successfully installed ncurses-6.5-7tikjbf5ohs2uoa7wsw32ewbrw5xpphq
  Stage: 1.07s.  Autoreconf: 0.00s.  Configure: 57.81s.  Build: 37.14s.  Install: 10.74s.  Post-install: 1.50s.  Total: 1m 48.60s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/ncurses-6.5-7tikjbf5ohs2uoa7wsw32ewbrw5xpphq
==> Installing pigz-2.8-ub6z3ew6nt6vatycresfm4kwoeg6eatw [12/20]
==> No binary for pigz-2.8-ub6z3ew6nt6vatycresfm4kwoeg6eatw found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/2f/2f7f6a6986996d21cb8658535fff95f1c7107ddce22b5324f4b41890e2904706.tar.gz
==> No patches needed for pigz
==> pigz: Executing phase: 'edit'
==> pigz: Executing phase: 'build'
==> pigz: Executing phase: 'install'
==> pigz: Successfully installed pigz-2.8-ub6z3ew6nt6vatycresfm4kwoeg6eatw
  Stage: 0.33s.  Edit: 0.00s.  Build: 4.62s.  Install: 0.01s.  Post-install: 0.02s.  Total: 5.26s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/pigz-2.8-ub6z3ew6nt6vatycresfm4kwoeg6eatw
==> Installing libxml2-2.13.5-neuejs6jzgsr43d624exgqpmr4jibcbf [13/20]
==> No binary for libxml2-2.13.5-neuejs6jzgsr43d624exgqpmr4jibcbf found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/74/74fc163217a3964257d3be39af943e08861263c4231f9ef5b496b6f6d4c7b2b6.tar.xz
==> Fetching https://mirror.spack.io/_source-cache/archive/96/96151685cec997e1f9f3387e3626d61e6284d4d6e66e0e440c209286c03e9cc7.tar.gz
==> Moving resource stage
        source: /tmp/admins/spack-stage/resource-xmlts-neuejs6jzgsr43d624exgqpmr4jibcbf/spack-src/
        destination: /tmp/admins/spack-stage/spack-stage-libxml2-2.13.5-neuejs6jzgsr43d624exgqpmr4jibcbf/spack-src/xmlconf
==> Ran patch() for libxml2
==> libxml2: Executing phase: 'autoreconf'
==> libxml2: Executing phase: 'configure'
==> libxml2: Executing phase: 'build'
==> libxml2: Executing phase: 'install'
==> libxml2: Successfully installed libxml2-2.13.5-neuejs6jzgsr43d624exgqpmr4jibcbf
  Stage: 2.97s.  Autoreconf: 0.00s.  Configure: 11.52s.  Build: 14.85s.  Install: 0.78s.  Post-install: 0.12s.  Total: 30.56s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/libxml2-2.13.5-neuejs6jzgsr43d624exgqpmr4jibcbf
==> Installing m4-1.4.19-ewhwo32ya4jhht3okad5p2zzy2fv6eyf [14/20]
==> No binary for m4-1.4.19-ewhwo32ya4jhht3okad5p2zzy2fv6eyf found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/3b/3be4a26d825ffdfda52a56fc43246456989a3630093cced3fbddf4771ee58a70.tar.gz
==> Applied patch /home/admins/spack/var/spack/repos/builtin/packages/m4/checks-198.sysval.1.patch
==> Applied patch /home/admins/spack/var/spack/repos/builtin/packages/m4/checks-198.sysval.2.patch
==> Ran patch() for m4
==> m4: Executing phase: 'autoreconf'
==> m4: Executing phase: 'configure'
==> m4: Executing phase: 'build'
==> m4: Executing phase: 'install'
==> m4: Successfully installed m4-1.4.19-ewhwo32ya4jhht3okad5p2zzy2fv6eyf
  Stage: 0.67s.  Autoreconf: 0.00s.  Configure: 1m 15.02s.  Build: 10.29s.  Install: 2.00s.  Post-install: 0.05s.  Total: 1m 28.44s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/m4-1.4.19-ewhwo32ya4jhht3okad5p2zzy2fv6eyf
==> Installing bzip2-1.0.8-xcpnsyzgb7efuokjzqot7wbwvrn2ew4l [15/20]
==> No binary for bzip2-1.0.8-xcpnsyzgb7efuokjzqot7wbwvrn2ew4l found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/ab/ab5a03176ee106d3f0fa90e381da478ddae405918153cca248e682cd0c4a2269.tar.gz
==> Ran patch() for bzip2
==> bzip2: Executing phase: 'install'
==> bzip2: Successfully installed bzip2-1.0.8-xcpnsyzgb7efuokjzqot7wbwvrn2ew4l
  Stage: 0.69s.  Install: 6.15s.  Post-install: 0.04s.  Total: 6.98s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/bzip2-1.0.8-xcpnsyzgb7efuokjzqot7wbwvrn2ew4l
==> Installing tar-1.35-nby5x2et2amlet2o2gl6hxjbvalg24jq [16/20]
==> No binary for tar-1.35-nby5x2et2amlet2o2gl6hxjbvalg24jq found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/14/14d55e32063ea9526e057fbf35fcabd53378e769787eff7919c3755b02d2b57e.tar.gz
==> No patches needed for tar
==> tar: Executing phase: 'autoreconf'
==> tar: Executing phase: 'configure'
==> tar: Executing phase: 'build'
==> tar: Executing phase: 'install'
==> tar: Successfully installed tar-1.35-nby5x2et2amlet2o2gl6hxjbvalg24jq
  Stage: 0.66s.  Autoreconf: 0.00s.  Configure: 1m 15.23s.  Build: 6.93s.  Install: 1.05s.  Post-install: 0.06s.  Total: 1m 24.28s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/tar-1.35-nby5x2et2amlet2o2gl6hxjbvalg24jq
==> Installing gettext-0.23.1-r7kjcvzrwgy43m6inex6ilz2tgyrclsy [17/20]
==> No binary for gettext-0.23.1-r7kjcvzrwgy43m6inex6ilz2tgyrclsy found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/c1/c1f97a72a7385b7e71dd07b5fea6cdaf12c9b88b564976b23bd8c11857af2970.tar.xz
==> Ran patch() for gettext
==> gettext: Executing phase: 'autoreconf'
==> gettext: Executing phase: 'configure'
==> gettext: Executing phase: 'build'
==> gettext: Executing phase: 'install'
==> gettext: Successfully installed gettext-0.23.1-r7kjcvzrwgy43m6inex6ilz2tgyrclsy
  Stage: 2.98s.  Autoreconf: 0.00s.  Configure: 4m 58.88s.  Build: 4m 35.03s.  Install: 38.57s.  Post-install: 1.18s.  Total: 10m 17.05s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/gettext-0.23.1-r7kjcvzrwgy43m6inex6ilz2tgyrclsy
==> Installing findutils-4.10.0-yoteieolbcxvg45red7jttsgyxx3bhki [18/20]
==> No binary for findutils-4.10.0-yoteieolbcxvg45red7jttsgyxx3bhki found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/13/1387e0b67ff247d2abde998f90dfbf70c1491391a59ddfecb8ae698789f0a4f5.tar.xz
==> Applied patch /home/admins/spack/var/spack/repos/builtin/packages/findutils/nonnull.patch
==> findutils: Executing phase: 'autoreconf'
==> findutils: Executing phase: 'configure'
==> findutils: Executing phase: 'build'
==> findutils: Executing phase: 'install'
==> findutils: Successfully installed findutils-4.10.0-yoteieolbcxvg45red7jttsgyxx3bhki
  Stage: 0.96s.  Autoreconf: 0.00s.  Configure: 1m 35.37s.  Build: 8.41s.  Install: 3.11s.  Post-install: 0.13s.  Total: 1m 48.40s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/findutils-4.10.0-yoteieolbcxvg45red7jttsgyxx3bhki
==> Installing libtool-2.4.7-gmroq6p7kyndi77e2r4aiz3r4bonfd3f [19/20]
==> No binary for libtool-2.4.7-gmroq6p7kyndi77e2r4aiz3r4bonfd3f found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/04/04e96c2404ea70c590c546eba4202a4e12722c640016c12b9b2f1ce3d481e9a8.tar.gz
==> Ran patch() for libtool
==> libtool: Executing phase: 'autoreconf'
==> libtool: Executing phase: 'configure'
==> libtool: Executing phase: 'build'
==> libtool: Executing phase: 'install'
==> libtool: Successfully installed libtool-2.4.7-gmroq6p7kyndi77e2r4aiz3r4bonfd3f
  Stage: 0.74s.  Autoreconf: 0.01s.  Configure: 17.30s.  Build: 4.20s.  Install: 1.18s.  Post-install: 0.10s.  Total: 24.01s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/libtool-2.4.7-gmroq6p7kyndi77e2r4aiz3r4bonfd3f
==> Installing aocc-5.0.0-apukhybcqimtpjdaoof2cd6odhjgklwx [20/20]
==> No binary for aocc-5.0.0-apukhybcqimtpjdaoof2cd6odhjgklwx found: installing from source
==> Fetching https://mirror.spack.io/_source-cache/archive/96/966fac2d2c759e9de6e969c10ada7a7b306c113f7f1e07ea376829ec86380daa.tar
==> No patches needed for aocc
==> aocc: Executing phase: 'install'
==> aocc: Successfully installed aocc-5.0.0-apukhybcqimtpjdaoof2cd6odhjgklwx
  Stage: 27.92s.  Install: 4.14s.  Post-install: 4.12s.  Total: 36.37s
[+] /home/admins/spack/opt/spack/linux-ubuntu24.04-zen2/gcc-13.3.0/aocc-5.0.0-apukhybcqimtpjdaoof2cd6odhjgklwx
╭─ ~/spack/bin  on develop ───────────────────────────────────────────── ✔  took 24m 48s  at 18:06:23 ─╮
╰─      

export BLIS_PATH=/opt/AMD/aocl/aocl-linux-aocc-5.0.0/aocc/lib 
export LIBFLAME_PATH=/opt/AMD/aocl/aocl-linux-aocc-5.0.0/aocc/lib
export LD_LIBRARY_PATH=$BLIS_PATH:$LIBFLAME_PATH:$LD_LIBRARY_PATH
./configure --with-blas="-L$BLIS_PATH -lblis-mt -L$LIBFLAME_PATH -lflame" --with-lapack
make -j          
                                                                                 ─╯


```
