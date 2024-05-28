load("@tsl//tsl/platform:rules_cc.bzl", "cc_library")
load("//xla:xla.bzl", "xla_cc_test")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    default_visibility = [":friends"],
    licenses = ["notice"],
)

package_group(
    name = "friends",
    includes = [
        "//xla:friends",
    ],
)

cc_library(
    name = "buffer_allocations",
    srcs = ["buffer_allocations.cc"],
    hdrs = ["buffer_allocations.h"],
    deps = [
        "//xla/service:buffer_assignment",
        "//xla/service:maybe_owning_device_memory",
        "//xla/stream_executor",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/status:statusor",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@tsl//tsl/platform:statusor",
    ],
)

cc_library(
    name = "thunk",
    srcs = ["thunk.cc"],
    hdrs = ["thunk.h"],
    deps = [
        ":buffer_allocations",
        "@com_google_absl//absl/status",
        "@tsl//tsl/platform:errors",
        "@tsl//tsl/platform:logging",
    ],
)

cc_library(
    name = "copy_thunk",
    srcs = ["copy_thunk.cc"],
    hdrs = ["copy_thunk.h"],
    deps = [
        ":thunk",
        "//xla/service:buffer_assignment",
        "//xla/stream_executor",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings:str_format",
        "@tsl//tsl/platform:logging",
        "@tsl//tsl/platform:numbers",
        "@tsl//tsl/platform:statusor",
    ],
)

xla_cc_test(
    name = "copy_thunk_test",
    srcs = ["copy_thunk_test.cc"],
    deps = [
        ":buffer_allocations",
        ":copy_thunk",
        ":thunk",
        "//xla/service:buffer_assignment",
        "//xla/service:maybe_owning_device_memory",
        "//xla/stream_executor",
        "@tsl//tsl/lib/core:status_test_util",
        "@tsl//tsl/platform:test",
        "@tsl//tsl/platform:test_main",
    ],
)