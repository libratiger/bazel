load("@rules_java//java:defs.bzl", "java_library", "java_test")

# Description:
#   Skyframe tests.
package(
    default_testonly = 1,
    default_visibility = ["//src:__subpackages__"],
)

filegroup(
    name = "srcs",
    testonly = 0,
    srcs = glob(["**"]),
    visibility = ["//src:__subpackages__"],
)

TESTUTIL_FILES = [
    "TrackingAwaiter.java",
    "GraphTester.java",
    "GenericFunctionException.java",
    "SomeErrorException.java",
    "TrackingProgressReceiver.java",
    "WalkableGraphUtils.java",
    # Truth Subject, SubjectFactory, and Graph files.
] + glob(["*Subject.java"]) + glob(["*SubjectFactory.java"]) + glob(["*Graph.java"]) + glob(["*Helper.java"])

java_library(
    name = "testutil",
    srcs = TESTUTIL_FILES,
    deps = [
        "//src/main/java/com/google/devtools/build/lib/concurrent",
        "//src/main/java/com/google/devtools/build/lib/events",
        "//src/main/java/com/google/devtools/build/lib/skyframe/serialization/autocodec",
        "//src/main/java/com/google/devtools/build/lib/util",
        "//src/main/java/com/google/devtools/build/skyframe",
        "//src/main/java/com/google/devtools/build/skyframe:skyframe-objects",
        "//src/test/java/com/google/devtools/build/lib/testutil:TestUtils",
        "//third_party:auto_value",
        "//third_party:guava",
        "//third_party:jsr305",
        "//third_party:truth",
    ],
)

java_library(
    name = "skyframe_tests",
    srcs = glob(
        ["*.java"],
        exclude = TESTUTIL_FILES,
    ),
    deps = [
        ":testutil",
        "//src/main/java/com/google/devtools/build/lib/collect/nestedset",
        "//src/main/java/com/google/devtools/build/lib/concurrent",
        "//src/main/java/com/google/devtools/build/lib/events",
        "//src/main/java/com/google/devtools/build/lib/skyframe/serialization/autocodec",
        "//src/main/java/com/google/devtools/build/lib/skyframe/serialization/testutils",
        "//src/main/java/com/google/devtools/build/lib/util",
        "//src/main/java/com/google/devtools/build/skyframe",
        "//src/main/java/com/google/devtools/build/skyframe:cpu_heavy_skykey",
        "//src/main/java/com/google/devtools/build/skyframe:graph_inconsistency_java_proto",
        "//src/main/java/com/google/devtools/build/skyframe:skyframe-objects",
        "//src/test/java/com/google/devtools/build/lib/testutil:EventUtils",
        "//src/test/java/com/google/devtools/build/lib/testutil:TestRunnableWrapper",
        "//src/test/java/com/google/devtools/build/lib/testutil:TestSuite",
        "//src/test/java/com/google/devtools/build/lib/testutil:TestThread",
        "//src/test/java/com/google/devtools/build/lib/testutil:TestUtils",
        "//third_party:auto_value",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
        "@com_google_testparameterinjector//:testparameterinjector",
    ],
)

java_test(
    name = "SkyframeTests",
    size = "medium",
    shard_count = 2,
    test_class = "com.google.devtools.build.skyframe.AllTests",
    runtime_deps = [":skyframe_tests"],
)
