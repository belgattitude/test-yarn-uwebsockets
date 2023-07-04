## YARN reproductions

A repo to reproduce some issues with YARN.

Clone this repo

```bash
git clone https://github.com/belgattitude/test-yarn-uwebsockets.git
```

```bash
rm -rf .yarn/cache ~/.yarn/berry/cache && \
YARN_ENABLE_GLOBAL_CACHE=false corepack yarn@4.0.0-rc.48 install && \
ls -la .yarn/cache && ls -la  ~/.yarn/berry/cache
```

`YARN_ENABLE_GLOBAL_CACHE=false` is read (either from env, either from .yarnrc.yml).

- ✅ will persist the cache in `.yarn/cache/*.zip` (useful for CI as it's purged)
- ❌ will save also in global cache `~/.yarn/berry/cache/*.zip`)

Why doubling ? 

```
➤ YN0000: · Yarn 4.0.0-rc.48
➤ YN0000: ┌ Resolution step
➤ YN0000: └ Completed
➤ YN0000: ┌ Fetch step
➤ YN0013: │ A package was added to the cache (+ 95.8 KiB).
➤ YN0000: └ Completed in 1s 133ms
➤ YN0000: ┌ Link step
➤ YN0000: └ Completed
➤ YN0000: · Done in 1s 176ms
total 108
drwxrwxr-x 2 sebastien sebastien  4096 juil.  4 21:55 .
drwxrwxr-x 3 sebastien sebastien  4096 juil.  4 21:55 ..
-rw-rw-r-- 1 sebastien sebastien    26 juil.  4 21:55 .gitignore
-rw-r--r-- 1 sebastien sebastien 98104 juil.  4 21:55 @httpx-exception-npm-1.8.1-593ae98fd6-20d564e4e6.zip
total 104
drwxrwxr-x 2 sebastien sebastien  4096 juil.  4 21:55 .
drwxrwxr-x 6 sebastien sebastien  4096 juil.  4 21:55 ..
-rw-r--r-- 1 sebastien sebastien 98104 juil.  4 21:55 @httpx-exception-npm-1.8.1-593ae98fd6-10.zip

```