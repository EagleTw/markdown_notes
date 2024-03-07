# [Tips] Profiling: Callgrind/Collect

## Valgrind / Callgrind

Gprof, valgrind, and gpertools
http://gernotklingler.com/blog/gprof-valgrind-gperftools-evaluation-tools-application-level-cpu-profiling-linux/

```shell

source ~blazar/envscript/workfl$w/gcc-9.2.0.csh
source ~blazar/envscript/tool/kcachegrind/22.0.3.csh
qcachegrind callgrind.out.<pid>

```

## Collect (Solaris)

- `collect <exe>`
  - in vcs `vcs -collect ...`
- `analyzer <test.1.er>`
- Command line version of analyzer
  - `er_print -function test.1.er > report.log`
