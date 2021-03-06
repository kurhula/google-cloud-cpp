# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

load(":google_cloud_cpp_generator.bzl", "google_cloud_cpp_generator_hdrs", "google_cloud_cpp_generator_srcs")

cc_library(
    name = "google_cloud_cpp_generator",
    srcs = google_cloud_cpp_generator_srcs,
    hdrs = google_cloud_cpp_generator_hdrs,
    deps = [
        "//google/cloud:google_cloud_cpp_common",
        "//google/cloud:google_cloud_cpp_grpc_utils",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/strings",
        "@com_google_googleapis//google/longrunning:longrunning_cc_grpc",
        "@com_google_protobuf//:protoc_lib",
    ],
)

load(":google_cloud_cpp_generator_unit_tests.bzl", "google_cloud_cpp_generator_unit_tests")

[cc_test(
    name = test.replace("/", "_").replace(".cc", ""),
    srcs = [test],
    deps = [
        ":google_cloud_cpp_generator",
        "@com_google_googletest//:gtest_main",
    ],
) for test in google_cloud_cpp_generator_unit_tests]

cc_binary(
    name = "protoc-gen-cpp_codegen",
    srcs = ["main.cc"],
    includes = ["."],
    visibility = ["//visibility:public"],
    deps = [":google_cloud_cpp_generator"],
)
