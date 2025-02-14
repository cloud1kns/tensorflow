# Fuzzing TensorFlow.
# Since we use OSSFuzz, gather all fuzzers into a single place.
# This way, we can use tooling to determine the status of the fuzzing efforts.

load(
    "//tensorflow/security/fuzzing:tf_fuzzing.bzl",
    "tf_fuzz_target",
    "tf_py_fuzz_target",
)
load(
    "//tensorflow/core/platform:build_config.bzl",
    "tf_proto_library",
)

package(
    licenses = ["notice"],
)

tf_fuzz_target(
    name = "status_fuzz",
    srcs = ["status_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:status",
    ],
)

tf_fuzz_target(
    name = "status_group_fuzz",
    srcs = ["status_group_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:status",
    ],
)

tf_fuzz_target(
    name = "bfloat16_fuzz",
    srcs = ["bfloat16_fuzz.cc"],
    tags = ["no_oss"],  # b/175698644
    deps = [
        "//tensorflow/core:test",
        "//tensorflow/core/framework:bfloat16",
        "@com_google_absl//absl/strings",
    ],
)

tf_fuzz_target(
    name = "AreAttrValuesEqual_fuzz",
    srcs = ["AreAttrValuesEqual_fuzz.cc"],
    tags = ["no_oss"],  # b/175698644
    deps = [
        "//tensorflow/core/framework:attr_value_proto_cc",
        "//tensorflow/core/framework:attr_value_util",
        "@com_google_absl//absl/strings",
    ],
)

tf_fuzz_target(
    name = "ParseAttrValue_fuzz",
    srcs = ["ParseAttrValue_fuzz.cc"],
    tags = ["no_oss"],  # b/175698644
    deps = [
        "//tensorflow/core/framework:attr_value_proto_cc",
        "//tensorflow/core/framework:attr_value_util",
    ],
)

tf_fuzz_target(
    name = "joinpath_fuzz",
    srcs = ["joinpath_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:path",
        "@com_google_absl//absl/strings",
    ],
)

tf_fuzz_target(
    name = "parseURI_fuzz",
    srcs = ["parseURI_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:path",
        "//tensorflow/core/platform:stringpiece",
        "@com_google_absl//absl/strings",
    ],
)

tf_fuzz_target(
    name = "cleanpath_fuzz",
    srcs = ["cleanpath_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:path",
        "@com_google_absl//absl/strings",
    ],
)

tf_fuzz_target(
    name = "consume_leading_digits_fuzz",
    srcs = ["consume_leading_digits_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:str_util",
        "//tensorflow/core/platform:stringpiece",
    ],
)

tf_fuzz_target(
    name = "arg_def_case_fuzz",
    srcs = ["arg_def_case_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:str_util",
        "//tensorflow/core/platform:stringpiece",
    ],
)

tf_fuzz_target(
    name = "string_replace_fuzz",
    srcs = ["string_replace_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:str_util",
        "//tensorflow/core/platform:stringpiece",
    ],
)

tf_fuzz_target(
    name = "stringprintf_fuzz",
    srcs = ["stringprintf_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:stringprintf",
    ],
)

tf_fuzz_target(
    name = "tstring_fuzz",
    srcs = ["tstring_fuzz.cc"],
    tags = ["notap"],  # TODO(188445161): Flaky, re-enable.
    deps = [
        "//tensorflow/core/platform:tstring",
    ],
)

tf_fuzz_target(
    name = "base64_fuzz",
    srcs = ["base64_fuzz.cc"],
    deps = [
        "//tensorflow/core/platform:base64",
        "//tensorflow/core/platform:status",
        "//tensorflow/core/platform:stringpiece",
    ],
)

tf_fuzz_target(
    name = "checkpoint_reader_fuzz",
    srcs = ["checkpoint_reader_fuzz.cc"],
    corpus = glob(["checkpoint_reader_testdata/*"]),
    deps = [
        ":checkpoint_reader_fuzz_input_proto_cc",
        "//tensorflow/c:checkpoint_reader",
        "//tensorflow/c:tf_status_headers",
        "//tensorflow/c:tf_status_helper",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
        "//tensorflow/core/framework:types_proto_cc",
        "//tensorflow/core/platform:status",
        "@com_google_libprotobuf_mutator//:libprotobuf_mutator",
    ],
)

tf_proto_library(
    name = "checkpoint_reader_fuzz_input_proto",
    srcs = ["checkpoint_reader_fuzz_input.proto"],
    cc_api_version = 2,
    make_default_target_header_only = True,
    protodeps = [
        "//tensorflow/core/util:saved_tensor_slice_proto",
    ],
)

py_library(
    name = "python_fuzzing",
    srcs = ["python_fuzzing.py"],
    srcs_version = "PY3",
)

tf_py_fuzz_target(
    name = "abs_fuzz",
    srcs = ["abs_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "acos_fuzz",
    srcs = ["acos_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "acosh_fuzz",
    srcs = ["acosh_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "add_fuzz",
    srcs = ["add_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "constant_fuzz",
    srcs = ["constant_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
)

tf_py_fuzz_target(
    name = "raggedCountSparseOutput_fuzz",
    srcs = ["raggedCountSparseOutput_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "dataFormatVecPermute_fuzz",
    srcs = ["dataFormatVecPermute_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "sparseCountSparseOutput_fuzz",
    srcs = ["sparseCountSparseOutput_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)

tf_py_fuzz_target(
    name = "tf2migration_fuzz",
    srcs = ["tf2migration_fuzz.py"],
    tags = ["notap"],  # Run in OSS only.
    deps = [":python_fuzzing"],
)
