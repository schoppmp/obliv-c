genrule(
  name = "compile_oblivc",
  outs = [
    "bin/oblivcc",
    "bin/cilly",
  ],
  local = 1,
  # Build Obliv-C locally. We have to make a deep-copy of the sources, because
  # relative paths do not work across symlinks.
  cmd = "\n".join([
        "DIR=$$(mktemp -d $${TMPDIR-/tmp}/tmp.XXXXXXX)",
        "echo $${DIR}",
        "cp -Lfr . \"$${DIR}\"",
        "(cd \"$${DIR}\" && ./configure && make)",
        "cp $${DIR}/bin/oblivcc $(@D)/bin/oblivcc",
        "cp $${DIR}/bin/cilly $(@D)/bin/cilly",
        "cp -r $${DIR}/lib $(@D)",
        ]),
)

sh_binary(
  name = "oblivcc",
  srcs = ["bin/oblivcc"],
  data = [":compile_oblivc"],
  visibility = ["//visibility:public"],
)

cc_library(
  name = "runtime",
  srcs = glob(["src/ext/oblivc/*.c"]),
  hdrs = glob(["src/ext/oblivc/*.h"]),
  copts = ["-Isrc/ext/oblivc -Wno-unused-variable"],
  visibility = ["//visibility:public"],
)
