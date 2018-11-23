genrule(
  name = "obliv-c",
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
