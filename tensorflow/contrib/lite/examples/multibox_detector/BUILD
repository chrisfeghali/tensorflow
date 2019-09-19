# Description:
# TensorFlow Lite Multibox Detector using example label_image as a template.

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

load("//tensorflow/contrib/lite:build_def.bzl", "tflite_linkopts")

exports_files(glob([
    "testdata/*.bmp",
]))

cc_binary(
    name = "multibox_detector",
    srcs = [
        "get_top_n.h",
        "get_top_n_impl.h",
        "multibox_detector.cc",
    ],
    linkopts = tflite_linkopts() + select({
        "//tensorflow:android": [
            "-pie",  # Android 5.0 and later supports only PIE
            "-lm",  # some builtin ops, e.g., tanh, need -lm
        ],
        "//conditions:default": [],
    }),
    deps = [
        ":bitmap_helpers",
        "//tensorflow/contrib/lite:framework",
        "//tensorflow/contrib/lite:string_util",
        "//tensorflow/contrib/lite/kernels:builtin_ops",
        "//tensorflow/contrib/lite/profiling:profiler",
    ],
)

cc_library(
    name = "bitmap_helpers",
    srcs = ["bitmap_helpers.cc"],
    hdrs = [
        "bitmap_helpers.h",
        "bitmap_helpers_impl.h",
        "multibox_detector.h",
    ],
    deps = [
        "//tensorflow/contrib/lite:builtin_op_data",
        "//tensorflow/contrib/lite:framework",
        "//tensorflow/contrib/lite:string",
        "//tensorflow/contrib/lite:string_util",
        "//tensorflow/contrib/lite/kernels:builtin_ops",
        "//tensorflow/contrib/lite/schema:schema_fbs",
    ],
)

cc_test(
    name = "multibox_detector_test",
    srcs = [
        "get_top_n.h",
        "get_top_n_impl.h",
        "multibox_detector_test.cc",
    ],
    data = [
        "testdata/contrib/grace_hopper.bmp",
    ],
    deps = [
        ":bitmap_helpers",
        "@com_google_googletest//:gtest",
    ],
)
