# Ansible Day-1

## Initial run
```bash
ansible all --key-file ~/key_pair.pem --user debian -i inventory -m ping
```
<hr>

$${\color{green}Output:}$$

```bash
192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## Running with local ansible.cfg
```bash
ansible all -m ping
```
<hr>

$${\color{green}Output:}$$

```bash
192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## Running **apt update** in worker instance
```bash
ansible all -m apt -a update_cache=true --become --ask-become-pass
```

**-m** : module

**-a** : argument

**--become** : run via sudo

**--ask-become-pass** : input sudo password


$${\color{green}Output:}$$

```bash
192.168.2.243 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1711643758,
    "cache_updated": true,
    "changed": true
}
```

## Running **apt install vim-nox** in worker instance
```bash
ansible all -m apt -a "name=vim-nox state=latest" --become
```

**name=** : install <package>

**state** : package version

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
192.168.2.243 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1711643758,
    "cache_updated": false,
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following additional packages will be installed:\n  fonts-lato javascript-common libgdbm-compat4 libjs-jquery liblua5.2-0\n  libncurses6 libperl5.36 libpython3.11 libruby libruby3.1 libtcl8.6 perl\n  perl-modules-5.36 rake ruby ruby-net-telnet ruby-rubygems ruby-sdbm\n  ruby-webrick ruby-xmlrpc ruby3.1 rubygems-integration unzip zip\nSuggested packages:\n  apache2 | lighttpd | httpd tcl8.6 perl-doc libterm-readline-gnu-perl\n  | libterm-readline-perl-perl make libtap-harness-archive-perl ri ruby-dev\n  bundler cscope vim-doc\nThe following NEW packages will be installed:\n  fonts-lato javascript-common libgdbm-compat4 libjs-jquery liblua5.2-0\n  libncurses6 libperl5.36 libpython3.11 libruby libruby3.1 libtcl8.6 perl\n  perl-modules-5.36 rake ruby ruby-net-telnet ruby-rubygems ruby-sdbm\n  ruby-webrick ruby-xmlrpc ruby3.1 rubygems-integration unzip vim-nox zip\n0 upgraded, 25 newly installed, 0 to remove and 0 not upgraded.\nNeed to get 22.3 MB of archives.\nAfter this operation, 108 MB of additional disk space will be used.\nGet:1 file:/etc/apt/mirrors/debian.list Mirrorlist [30 B]\nGet:2 https://deb.debian.org/debian bookworm/main amd64 perl-modules-5.36 all 5.36.0-7+deb12u1 [2815 kB]\nGet:3 https://deb.debian.org/debian bookworm/main amd64 libgdbm-compat4 amd64 1.23-3 [48.2 kB]\nGet:4 https://deb.debian.org/debian bookworm/main amd64 libperl5.36 amd64 5.36.0-7+deb12u1 [4218 kB]\nGet:5 https://deb.debian.org/debian bookworm/main amd64 perl amd64 5.36.0-7+deb12u1 [239 kB]\nGet:6 https://deb.debian.org/debian bookworm/main amd64 fonts-lato all 2.0-2.1 [2696 kB]\nGet:7 https://deb.debian.org/debian bookworm/main amd64 javascript-common all 11+nmu1 [6260 B]\nGet:8 https://deb.debian.org/debian bookworm/main amd64 libjs-jquery all 3.6.1+dfsg+~3.5.14-1 [326 kB]\nGet:9 https://deb.debian.org/debian bookworm/main amd64 liblua5.2-0 amd64 5.2.4-3 [111 kB]\nGet:10 https://deb.debian.org/debian bookworm/main amd64 libncurses6 amd64 6.4-4 [103 kB]\nGet:11 https://deb.debian.org/debian bookworm/main amd64 libpython3.11 amd64 3.11.2-6 [1988 kB]\nGet:12 https://deb.debian.org/debian bookworm/main amd64 rubygems-integration all 1.18 [6704 B]\nGet:13 https://deb.debian.org/debian bookworm/main amd64 ruby3.1 amd64 3.1.2-7 [663 kB]\nGet:14 https://deb.debian.org/debian bookworm/main amd64 ruby-rubygems all 3.3.15-2 [293 kB]\nGet:15 https://deb.debian.org/debian bookworm/main amd64 ruby amd64 1:3.1 [5868 B]\nGet:16 https://deb.debian.org/debian bookworm/main amd64 rake all 13.0.6-3 [83.9 kB]\nGet:17 https://deb.debian.org/debian bookworm/main amd64 ruby-net-telnet all 0.2.0-1 [13.1 kB]\nGet:18 https://deb.debian.org/debian bookworm/main amd64 ruby-webrick all 1.8.1-1 [51.4 kB]\nGet:19 https://deb.debian.org/debian bookworm/main amd64 ruby-xmlrpc all 0.3.2-2 [24.4 kB]\nGet:20 https://deb.debian.org/debian bookworm/main amd64 ruby-sdbm amd64 1.0.0-5+b1 [15.4 kB]\nGet:21 https://deb.debian.org/debian bookworm/main amd64 libruby3.1 amd64 3.1.2-7 [5401 kB]\nGet:22 https://deb.debian.org/debian bookworm/main amd64 libruby amd64 1:3.1 [4972 B]\nGet:23 https://deb.debian.org/debian bookworm/main amd64 libtcl8.6 amd64 8.6.13+dfsg-2 [1035 kB]\nGet:24 https://deb.debian.org/debian bookworm/main amd64 unzip amd64 6.0-28 [166 kB]\nGet:25 https://deb.debian.org/debian bookworm/main amd64 vim-nox amd64 2:9.0.1378-2 [1747 kB]\nGet:26 https://deb.debian.org/debian bookworm/main amd64 zip amd64 3.0-13 [230 kB]\nFetched 22.3 MB in 3s (8362 kB/s)\nSelecting previously unselected package perl-modules-5.36.\r\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 24327 files and directories currently installed.)\r\nPreparing to unpack .../00-perl-modules-5.36_5.36.0-7+deb12u1_all.deb ...\r\nUnpacking perl-modules-5.36 (5.36.0-7+deb12u1) ...\r\nSelecting previously unselected package libgdbm-compat4:amd64.\r\nPreparing to unpack .../01-libgdbm-compat4_1.23-3_amd64.deb ...\r\nUnpacking libgdbm-compat4:amd64 (1.23-3) ...\r\nSelecting previously unselected package libperl5.36:amd64.\r\nPreparing to unpack .../02-libperl5.36_5.36.0-7+deb12u1_amd64.deb ...\r\nUnpacking libperl5.36:amd64 (5.36.0-7+deb12u1) ...\r\nSelecting previously unselected package perl.\r\nPreparing to unpack .../03-perl_5.36.0-7+deb12u1_amd64.deb ...\r\nUnpacking perl (5.36.0-7+deb12u1) ...\r\nSelecting previously unselected package fonts-lato.\r\nPreparing to unpack .../04-fonts-lato_2.0-2.1_all.deb ...\r\nUnpacking fonts-lato (2.0-2.1) ...\r\nSelecting previously unselected package javascript-common.\r\nPreparing to unpack .../05-javascript-common_11+nmu1_all.deb ...\r\nUnpacking javascript-common (11+nmu1) ...\r\nSelecting previously unselected package libjs-jquery.\r\nPreparing to unpack .../06-libjs-jquery_3.6.1+dfsg+~3.5.14-1_all.deb ...\r\nUnpacking libjs-jquery (3.6.1+dfsg+~3.5.14-1) ...\r\nSelecting previously unselected package liblua5.2-0:amd64.\r\nPreparing to unpack .../07-liblua5.2-0_5.2.4-3_amd64.deb ...\r\nUnpacking liblua5.2-0:amd64 (5.2.4-3) ...\r\nSelecting previously unselected package libncurses6:amd64.\r\nPreparing to unpack .../08-libncurses6_6.4-4_amd64.deb ...\r\nUnpacking libncurses6:amd64 (6.4-4) ...\r\nSelecting previously unselected package libpython3.11:amd64.\r\nPreparing to unpack .../09-libpython3.11_3.11.2-6_amd64.deb ...\r\nUnpacking libpython3.11:amd64 (3.11.2-6) ...\r\nSelecting previously unselected package rubygems-integration.\r\nPreparing to unpack .../10-rubygems-integration_1.18_all.deb ...\r\nUnpacking rubygems-integration (1.18) ...\r\nSelecting previously unselected package ruby3.1.\r\nPreparing to unpack .../11-ruby3.1_3.1.2-7_amd64.deb ...\r\nUnpacking ruby3.1 (3.1.2-7) ...\r\nSelecting previously unselected package ruby-rubygems.\r\nPreparing to unpack .../12-ruby-rubygems_3.3.15-2_all.deb ...\r\nUnpacking ruby-rubygems (3.3.15-2) ...\r\nSelecting previously unselected package ruby.\r\nPreparing to unpack .../13-ruby_1%3a3.1_amd64.deb ...\r\nUnpacking ruby (1:3.1) ...\r\nSelecting previously unselected package rake.\r\nPreparing to unpack .../14-rake_13.0.6-3_all.deb ...\r\nUnpacking rake (13.0.6-3) ...\r\nSelecting previously unselected package ruby-net-telnet.\r\nPreparing to unpack .../15-ruby-net-telnet_0.2.0-1_all.deb ...\r\nUnpacking ruby-net-telnet (0.2.0-1) ...\r\nSelecting previously unselected package ruby-webrick.\r\nPreparing to unpack .../16-ruby-webrick_1.8.1-1_all.deb ...\r\nUnpacking ruby-webrick (1.8.1-1) ...\r\nSelecting previously unselected package ruby-xmlrpc.\r\nPreparing to unpack .../17-ruby-xmlrpc_0.3.2-2_all.deb ...\r\nUnpacking ruby-xmlrpc (0.3.2-2) ...\r\nSelecting previously unselected package ruby-sdbm:amd64.\r\nPreparing to unpack .../18-ruby-sdbm_1.0.0-5+b1_amd64.deb ...\r\nUnpacking ruby-sdbm:amd64 (1.0.0-5+b1) ...\r\nSelecting previously unselected package libruby3.1:amd64.\r\nPreparing to unpack .../19-libruby3.1_3.1.2-7_amd64.deb ...\r\nUnpacking libruby3.1:amd64 (3.1.2-7) ...\r\nSelecting previously unselected package libruby:amd64.\r\nPreparing to unpack .../20-libruby_1%3a3.1_amd64.deb ...\r\nUnpacking libruby:amd64 (1:3.1) ...\r\nSelecting previously unselected package libtcl8.6:amd64.\r\nPreparing to unpack .../21-libtcl8.6_8.6.13+dfsg-2_amd64.deb ...\r\nUnpacking libtcl8.6:amd64 (8.6.13+dfsg-2) ...\r\nSelecting previously unselected package unzip.\r\nPreparing to unpack .../22-unzip_6.0-28_amd64.deb ...\r\nUnpacking unzip (6.0-28) ...\r\nSelecting previously unselected package vim-nox.\r\nPreparing to unpack .../23-vim-nox_2%3a9.0.1378-2_amd64.deb ...\r\nUnpacking vim-nox (2:9.0.1378-2) ...\r\nSelecting previously unselected package zip.\r\nPreparing to unpack .../24-zip_3.0-13_amd64.deb ...\r\nUnpacking zip (3.0-13) ...\r\nSetting up javascript-common (11+nmu1) ...\r\nSetting up fonts-lato (2.0-2.1) ...\r\nSetting up libpython3.11:amd64 (3.11.2-6) ...\r\nSetting up unzip (6.0-28) ...\r\nSetting up rubygems-integration (1.18) ...\r\nSetting up zip (3.0-13) ...\r\nSetting up perl-modules-5.36 (5.36.0-7+deb12u1) ...\r\nSetting up libncurses6:amd64 (6.4-4) ...\r\nSetting up ruby-net-telnet (0.2.0-1) ...\r\nSetting up libtcl8.6:amd64 (8.6.13+dfsg-2) ...\r\nSetting up libgdbm-compat4:amd64 (1.23-3) ...\r\nSetting up ruby-webrick (1.8.1-1) ...\r\nSetting up liblua5.2-0:amd64 (5.2.4-3) ...\r\nSetting up libjs-jquery (3.6.1+dfsg+~3.5.14-1) ...\r\nSetting up ruby-xmlrpc (0.3.2-2) ...\r\nSetting up libperl5.36:amd64 (5.36.0-7+deb12u1) ...\r\nSetting up perl (5.36.0-7+deb12u1) ...\r\nSetting up libruby:amd64 (1:3.1) ...\r\nSetting up ruby-rubygems (3.3.15-2) ...\r\nSetting up ruby (1:3.1) ...\r\nSetting up rake (13.0.6-3) ...\r\nSetting up ruby-sdbm:amd64 (1.0.0-5+b1) ...\r\nSetting up libruby3.1:amd64 (3.1.2-7) ...\r\nSetting up ruby3.1 (3.1.2-7) ...\r\nSetting up vim-nox (2:9.0.1378-2) ...\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/ex (ex) in auto mode\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/rview (rview) in auto mode\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/rvim (rvim) in auto mode\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vi (vi) in auto mode\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/view (view) in auto mode\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vim (vim) in auto mode\r\nupdate-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vimdiff (vimdiff) in auto mode\r\nProcessing triggers for libc-bin (2.36-9+deb12u4) ...\r\nProcessing triggers for man-db (2.11.2-2) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following additional packages will be installed:",
        "  fonts-lato javascript-common libgdbm-compat4 libjs-jquery liblua5.2-0",
        "  libncurses6 libperl5.36 libpython3.11 libruby libruby3.1 libtcl8.6 perl",
        "  perl-modules-5.36 rake ruby ruby-net-telnet ruby-rubygems ruby-sdbm",
        "  ruby-webrick ruby-xmlrpc ruby3.1 rubygems-integration unzip zip",
        "Suggested packages:",
        "  apache2 | lighttpd | httpd tcl8.6 perl-doc libterm-readline-gnu-perl",
        "  | libterm-readline-perl-perl make libtap-harness-archive-perl ri ruby-dev",
        "  bundler cscope vim-doc",
        "The following NEW packages will be installed:",
        "  fonts-lato javascript-common libgdbm-compat4 libjs-jquery liblua5.2-0",
        "  libncurses6 libperl5.36 libpython3.11 libruby libruby3.1 libtcl8.6 perl",
        "  perl-modules-5.36 rake ruby ruby-net-telnet ruby-rubygems ruby-sdbm",
        "  ruby-webrick ruby-xmlrpc ruby3.1 rubygems-integration unzip vim-nox zip",
        "0 upgraded, 25 newly installed, 0 to remove and 0 not upgraded.",
        "Need to get 22.3 MB of archives.",
        "After this operation, 108 MB of additional disk space will be used.",
        "Get:1 file:/etc/apt/mirrors/debian.list Mirrorlist [30 B]",
        "Get:2 https://deb.debian.org/debian bookworm/main amd64 perl-modules-5.36 all 5.36.0-7+deb12u1 [2815 kB]",
        "Get:3 https://deb.debian.org/debian bookworm/main amd64 libgdbm-compat4 amd64 1.23-3 [48.2 kB]",
        "Get:4 https://deb.debian.org/debian bookworm/main amd64 libperl5.36 amd64 5.36.0-7+deb12u1 [4218 kB]",
        "Get:5 https://deb.debian.org/debian bookworm/main amd64 perl amd64 5.36.0-7+deb12u1 [239 kB]",
        "Get:6 https://deb.debian.org/debian bookworm/main amd64 fonts-lato all 2.0-2.1 [2696 kB]",
        "Get:7 https://deb.debian.org/debian bookworm/main amd64 javascript-common all 11+nmu1 [6260 B]",
        "Get:8 https://deb.debian.org/debian bookworm/main amd64 libjs-jquery all 3.6.1+dfsg+~3.5.14-1 [326 kB]",
        "Get:9 https://deb.debian.org/debian bookworm/main amd64 liblua5.2-0 amd64 5.2.4-3 [111 kB]",
        "Get:10 https://deb.debian.org/debian bookworm/main amd64 libncurses6 amd64 6.4-4 [103 kB]",
        "Get:11 https://deb.debian.org/debian bookworm/main amd64 libpython3.11 amd64 3.11.2-6 [1988 kB]",
        "Get:12 https://deb.debian.org/debian bookworm/main amd64 rubygems-integration all 1.18 [6704 B]",
        "Get:13 https://deb.debian.org/debian bookworm/main amd64 ruby3.1 amd64 3.1.2-7 [663 kB]",
        "Get:14 https://deb.debian.org/debian bookworm/main amd64 ruby-rubygems all 3.3.15-2 [293 kB]",
        "Get:15 https://deb.debian.org/debian bookworm/main amd64 ruby amd64 1:3.1 [5868 B]",
        "Get:16 https://deb.debian.org/debian bookworm/main amd64 rake all 13.0.6-3 [83.9 kB]",
        "Get:17 https://deb.debian.org/debian bookworm/main amd64 ruby-net-telnet all 0.2.0-1 [13.1 kB]",
        "Get:18 https://deb.debian.org/debian bookworm/main amd64 ruby-webrick all 1.8.1-1 [51.4 kB]",
        "Get:19 https://deb.debian.org/debian bookworm/main amd64 ruby-xmlrpc all 0.3.2-2 [24.4 kB]",
        "Get:20 https://deb.debian.org/debian bookworm/main amd64 ruby-sdbm amd64 1.0.0-5+b1 [15.4 kB]",
        "Get:21 https://deb.debian.org/debian bookworm/main amd64 libruby3.1 amd64 3.1.2-7 [5401 kB]",
        "Get:22 https://deb.debian.org/debian bookworm/main amd64 libruby amd64 1:3.1 [4972 B]",
        "Get:23 https://deb.debian.org/debian bookworm/main amd64 libtcl8.6 amd64 8.6.13+dfsg-2 [1035 kB]",
        "Get:24 https://deb.debian.org/debian bookworm/main amd64 unzip amd64 6.0-28 [166 kB]",
        "Get:25 https://deb.debian.org/debian bookworm/main amd64 vim-nox amd64 2:9.0.1378-2 [1747 kB]",
        "Get:26 https://deb.debian.org/debian bookworm/main amd64 zip amd64 3.0-13 [230 kB]",
        "Fetched 22.3 MB in 3s (8362 kB/s)",
        "Selecting previously unselected package perl-modules-5.36.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 24327 files and directories currently installed.)",
        "Preparing to unpack .../00-perl-modules-5.36_5.36.0-7+deb12u1_all.deb ...",
        "Unpacking perl-modules-5.36 (5.36.0-7+deb12u1) ...",
        "Selecting previously unselected package libgdbm-compat4:amd64.",
        "Preparing to unpack .../01-libgdbm-compat4_1.23-3_amd64.deb ...",
        "Unpacking libgdbm-compat4:amd64 (1.23-3) ...",
        "Selecting previously unselected package libperl5.36:amd64.",
        "Preparing to unpack .../02-libperl5.36_5.36.0-7+deb12u1_amd64.deb ...",
        "Unpacking libperl5.36:amd64 (5.36.0-7+deb12u1) ...",
        "Selecting previously unselected package perl.",
        "Preparing to unpack .../03-perl_5.36.0-7+deb12u1_amd64.deb ...",
        "Unpacking perl (5.36.0-7+deb12u1) ...",
        "Selecting previously unselected package fonts-lato.",
        "Preparing to unpack .../04-fonts-lato_2.0-2.1_all.deb ...",
        "Unpacking fonts-lato (2.0-2.1) ...",
        "Selecting previously unselected package javascript-common.",
        "Preparing to unpack .../05-javascript-common_11+nmu1_all.deb ...",
        "Unpacking javascript-common (11+nmu1) ...",
        "Selecting previously unselected package libjs-jquery.",
        "Preparing to unpack .../06-libjs-jquery_3.6.1+dfsg+~3.5.14-1_all.deb ...",
        "Unpacking libjs-jquery (3.6.1+dfsg+~3.5.14-1) ...",
        "Selecting previously unselected package liblua5.2-0:amd64.",
        "Preparing to unpack .../07-liblua5.2-0_5.2.4-3_amd64.deb ...",
        "Unpacking liblua5.2-0:amd64 (5.2.4-3) ...",
        "Selecting previously unselected package libncurses6:amd64.",
        "Preparing to unpack .../08-libncurses6_6.4-4_amd64.deb ...",
        "Unpacking libncurses6:amd64 (6.4-4) ...",
        "Selecting previously unselected package libpython3.11:amd64.",
        "Preparing to unpack .../09-libpython3.11_3.11.2-6_amd64.deb ...",
        "Unpacking libpython3.11:amd64 (3.11.2-6) ...",
        "Selecting previously unselected package rubygems-integration.",
        "Preparing to unpack .../10-rubygems-integration_1.18_all.deb ...",
        "Unpacking rubygems-integration (1.18) ...",
        "Selecting previously unselected package ruby3.1.",
        "Preparing to unpack .../11-ruby3.1_3.1.2-7_amd64.deb ...",
        "Unpacking ruby3.1 (3.1.2-7) ...",
        "Selecting previously unselected package ruby-rubygems.",
        "Preparing to unpack .../12-ruby-rubygems_3.3.15-2_all.deb ...",
        "Unpacking ruby-rubygems (3.3.15-2) ...",
        "Selecting previously unselected package ruby.",
        "Preparing to unpack .../13-ruby_1%3a3.1_amd64.deb ...",
        "Unpacking ruby (1:3.1) ...",
        "Selecting previously unselected package rake.",
        "Preparing to unpack .../14-rake_13.0.6-3_all.deb ...",
        "Unpacking rake (13.0.6-3) ...",
        "Selecting previously unselected package ruby-net-telnet.",
        "Preparing to unpack .../15-ruby-net-telnet_0.2.0-1_all.deb ...",
        "Unpacking ruby-net-telnet (0.2.0-1) ...",
        "Selecting previously unselected package ruby-webrick.",
        "Preparing to unpack .../16-ruby-webrick_1.8.1-1_all.deb ...",
        "Unpacking ruby-webrick (1.8.1-1) ...",
        "Selecting previously unselected package ruby-xmlrpc.",
        "Preparing to unpack .../17-ruby-xmlrpc_0.3.2-2_all.deb ...",
        "Unpacking ruby-xmlrpc (0.3.2-2) ...",
        "Selecting previously unselected package ruby-sdbm:amd64.",
        "Preparing to unpack .../18-ruby-sdbm_1.0.0-5+b1_amd64.deb ...",
        "Unpacking ruby-sdbm:amd64 (1.0.0-5+b1) ...",
        "Selecting previously unselected package libruby3.1:amd64.",
        "Preparing to unpack .../19-libruby3.1_3.1.2-7_amd64.deb ...",
        "Unpacking libruby3.1:amd64 (3.1.2-7) ...",
        "Selecting previously unselected package libruby:amd64.",
        "Preparing to unpack .../20-libruby_1%3a3.1_amd64.deb ...",
        "Unpacking libruby:amd64 (1:3.1) ...",
        "Selecting previously unselected package libtcl8.6:amd64.",
        "Preparing to unpack .../21-libtcl8.6_8.6.13+dfsg-2_amd64.deb ...",
        "Unpacking libtcl8.6:amd64 (8.6.13+dfsg-2) ...",
        "Selecting previously unselected package unzip.",
        "Preparing to unpack .../22-unzip_6.0-28_amd64.deb ...",
        "Unpacking unzip (6.0-28) ...",
        "Selecting previously unselected package vim-nox.",
        "Preparing to unpack .../23-vim-nox_2%3a9.0.1378-2_amd64.deb ...",
        "Unpacking vim-nox (2:9.0.1378-2) ...",
        "Selecting previously unselected package zip.",
        "Preparing to unpack .../24-zip_3.0-13_amd64.deb ...",
        "Unpacking zip (3.0-13) ...",
        "Setting up javascript-common (11+nmu1) ...",
        "Setting up fonts-lato (2.0-2.1) ...",
        "Setting up libpython3.11:amd64 (3.11.2-6) ...",
        "Setting up unzip (6.0-28) ...",
        "Setting up rubygems-integration (1.18) ...",
        "Setting up zip (3.0-13) ...",
        "Setting up perl-modules-5.36 (5.36.0-7+deb12u1) ...",
        "Setting up libncurses6:amd64 (6.4-4) ...",
        "Setting up ruby-net-telnet (0.2.0-1) ...",
        "Setting up libtcl8.6:amd64 (8.6.13+dfsg-2) ...",
        "Setting up libgdbm-compat4:amd64 (1.23-3) ...",
        "Setting up ruby-webrick (1.8.1-1) ...",
        "Setting up liblua5.2-0:amd64 (5.2.4-3) ...",
        "Setting up libjs-jquery (3.6.1+dfsg+~3.5.14-1) ...",
        "Setting up ruby-xmlrpc (0.3.2-2) ...",
        "Setting up libperl5.36:amd64 (5.36.0-7+deb12u1) ...",
        "Setting up perl (5.36.0-7+deb12u1) ...",
        "Setting up libruby:amd64 (1:3.1) ...",
        "Setting up ruby-rubygems (3.3.15-2) ...",
        "Setting up ruby (1:3.1) ...",
        "Setting up rake (13.0.6-3) ...",
        "Setting up ruby-sdbm:amd64 (1.0.0-5+b1) ...",
        "Setting up libruby3.1:amd64 (3.1.2-7) ...",
        "Setting up ruby3.1 (3.1.2-7) ...",
        "Setting up vim-nox (2:9.0.1378-2) ...",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/ex (ex) in auto mode",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/rview (rview) in auto mode",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/rvim (rvim) in auto mode",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vi (vi) in auto mode",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/view (view) in auto mode",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vim (vim) in auto mode",
        "update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vimdiff (vimdiff) in auto mode",
        "Processing triggers for libc-bin (2.36-9+deb12u4) ...",
        "Processing triggers for man-db (2.11.2-2) ..."
    ]
}
```
</details>

## Running **apt upgrade** in worker instance
```bash
ansible all -m apt -a "upgrade=dist" --become
```

**upgrade** : will upgrade

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "msg": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nCalculating upgrade...\n0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.\n",
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nCalculating upgrade...\n0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "Calculating upgrade...",
        "0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded."
    ]
}
```
</details>


