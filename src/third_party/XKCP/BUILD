config_setting(
    name = "no_avx",
    values = {
        "copt": "-DNO_AVX",
    },
)

config_setting(
    name = "darwin_x86_64",
    constraint_values = [
        "@platforms//os:darwin",
        "@platforms//cpu:x86_64",
    ],
)

cc_library(
    name = "Keccak1600F",
    srcs = select({
        ":no_avx": [
            "CompactFIPS202/Keccak-readable-and-compact.c",
        ],
        "@platforms//cpu:x86_64": [
            "KeccakP-1600-OptimizedAVX2/KeccakP-1600-AVX2.s",
        ],
        "//conditions:default": [
            "CompactFIPS202/Keccak-readable-and-compact.c",
        ],
    }),
    visibility = ['//visibility:public'],
    tags = ["external_prover"],
    copts = select({
        ":darwin_x86_64": ["-Dold_gas_syntax"],
        "//conditions:default": [],
    }),
)
