# Bazel workspace created by @bazel/create 2.0.0

# Declares that this directory is the root of a Bazel workspace.
# See https://docs.bazel.build/versions/master/build-ref.html#workspace
workspace(
    # How this workspace would be referenced with absolute labels from another workspace
    name = "bazel_repro",
    # Map the @npm bazel workspace to the node_modules directory.
    # This lets Bazel use the same node_modules as other local tooling.
    managed_directories = {
        "@npm": ["node_modules"],
        "@app_npm": ["app/node_modules"],
        "@lib_npm": ["lib/node_modules"],
    },
)

# Install the nodejs "bootstrap" package
# This provides the basic tools for running and packaging nodejs programs in Bazel
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "5bf77cc2d13ddf9124f4c1453dd96063774d755d4fc75d922471540d1c9a8ea8",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/2.0.0-rc.0/rules_nodejs-2.0.0-rc.0.tar.gz"],
)

# The npm_install rule runs yarn anytime the package.json or package-lock.json file changes.
# It also extracts any Bazel rules distributed in an npm package.
load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

yarn_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "app_npm",
    package_json = "//app:package.json",
    yarn_lock = "//app:yarn.lock",
)

yarn_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "lib_npm",
    package_json = "//lib:package.json",
    yarn_lock = "//lib:yarn.lock",
)
