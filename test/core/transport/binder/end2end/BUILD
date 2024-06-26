# Copyright 2021 gRPC authors.
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

load("//bazel:grpc_build_system.bzl", "grpc_cc_library", "grpc_cc_test", "grpc_package", "grpc_proto_library")

licenses(["notice"])

grpc_package(
    name = "test/core/transport/binder/end2end",
    visibility = "tests",
)

grpc_cc_library(
    name = "fake_binder",
    testonly = 1,
    srcs = ["fake_binder.cc"],
    hdrs = ["fake_binder.h"],
    external_deps = [
        "absl/memory",
        "absl/random",
        "absl/strings",
        "absl/strings:str_format",
        "absl/time",
        "absl/types:variant",
    ],
    deps = [
        "//:gpr_base",
        "//src/core/ext/transport/binder/wire_format:binder",
        "//src/core/ext/transport/binder/wire_format:wire_reader",
    ],
)

grpc_cc_test(
    name = "fake_binder_test",
    srcs = ["fake_binder_test.cc"],
    external_deps = [
        "absl/strings",
        "absl/time",
        "gtest",
    ],
    language = "C++",
    uses_polling = False,
    deps = [
        ":fake_binder",
        "//test/core/util:grpc_test_util",
    ],
)

grpc_cc_library(
    name = "end2end_binder_channel",
    testonly = 1,
    srcs = ["testing_channel_create.cc"],
    hdrs = ["testing_channel_create.h"],
    external_deps = [],
    deps = [
        ":fake_binder",
        "//:grpc++_base",
        "//:grpc_base_c",
        "//src/core/ext/transport/binder/transport:binder_transport",
        "//src/core/ext/transport/binder/wire_format:wire_reader",
    ],
)

grpc_proto_library(
    name = "echo_grpc_proto",
    srcs = ["echo.proto"],
)

grpc_cc_library(
    name = "echo_service",
    testonly = 1,
    srcs = ["echo_service.cc"],
    hdrs = ["echo_service.h"],
    external_deps = [
        "absl/strings",
        "absl/strings:str_format",
        "absl/time",
    ],
    deps = [
        ":echo_grpc_proto",
    ],
)

grpc_cc_test(
    name = "end2end_binder_transport_test",
    srcs = ["end2end_binder_transport_test.cc"],
    external_deps = [
        "absl/memory",
        "absl/time",
        "gtest",
    ],
    language = "C++",
    deps = [
        ":echo_service",
        ":end2end_binder_channel",
        ":fake_binder",
        "//src/core/ext/transport/binder/transport:binder_transport",
        "//src/core/ext/transport/binder/wire_format:wire_reader",
        "//test/core/util:grpc_test_util",
    ],
)

grpc_cc_test(
    name = "binder_server_test",
    srcs = ["binder_server_test.cc"],
    external_deps = [
        "gtest",
    ],
    deps = [
        "//:grpc++",
        "//src/core/ext/transport/binder/client:grpc_transport_binder_client_impl",
        "//src/core/ext/transport/binder/server:grpc_transport_binder_server",
        "//test/core/transport/binder/end2end:echo_service",
        "//test/core/transport/binder/end2end:fake_binder",
        "//test/core/util:grpc_test_util",
        "//test/cpp/end2end:test_service_impl",
    ],
)
