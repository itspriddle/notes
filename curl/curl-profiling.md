---
title: Profiling curl requests
date: Mon Jun 03 21:52:06 -0400 2024
tags:
  - curl
---

To see how long different parts of a `curl` request take, you can use `curl -w`.

Create a file, `curl-timing.txt` with the following:

```
     time_namelookup:  %{time_namelookup}s\n
        time_connect:  %{time_connect}s\n
     time_appconnect:  %{time_appconnect}s\n
    time_pretransfer:  %{time_pretransfer}s\n
       time_redirect:  %{time_redirect}s\n
  time_starttransfer:  %{time_starttransfer}s\n
                       ---------\n
          time_total:  %{time_total}s\n
```

Then, run your `curl` request as normal, but insert `-w '@curl-format.txt'`, i.e.:

```
curl -w '@curl-format.txt' -o /dev/null -s -L 'https://example.com'
```

The output looks like:

```
     time_namelookup:  0.008203s
        time_connect:  0.036324s
     time_appconnect:  0.108840s
    time_pretransfer:  0.108922s
       time_redirect:  0.000000s
  time_starttransfer:  0.173767s
                       ---------
          time_total:  0.175557s
```
