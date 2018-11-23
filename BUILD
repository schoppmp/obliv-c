genrule(
  name = "oblivcc",
  outs = [
    "libobliv.a",
  ],
  local = 1,
  cmd = "\n".join([
        "DIR=$$(mktemp -d $${TMPDIR-/tmp}/tmp.XXXXXXX)",
        "cp -Lfr . \"$${DIR}\"",
        "(cd \"$${DIR}\" && ./configure && make)",
        "cp $${DIR}/_build/libobliv.a $(@D)",
        ]),
)

cc_library(
  name = "runtime",
  srcs = glob(["src/ext/oblivc/*.c"]),
  hdrs = glob(["src/ext/oblivc/*.h"]),
  copts = ["-Isrc/ext/oblivc -Wno-unused-variable"],
  visibility = ["//visibility:public"],
)
