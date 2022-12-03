# [Tips] Profiling: Callgrind/Collect

## Valgrind / Callgrind

Gprof, valgrind, and gpertools
http://gernotklingler.com/blog/gprof-valgrind-gperftools-evaluation-tools-application-level-cpu-profiling-linux/

```shell
# run the program with callgrind; generates a file callgrind.out.12345 that can be viewed with kcachegrind
valgrind --tool=callgrind ./cpuload

# open profile.callgrind with kcachegrind
kcachegrind profile.callgrind
```

## Collect (Solaris)

* `collect <exe>`
  * in vcs `vcs -collect ...`
* `analyzer <test.1.er>`
* Command line version of analyzer
  * `er_print -function test.1.er > report.log`
