load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

http_archive(
    name = "io_bazel_rules_go",
    urls = ["https://github.com/bazelbuild/rules_go/releases/download/0.18.5/rules_go-0.18.5.tar.gz"],
    sha256 = "a82a352bffae6bee4e95f68a8d80a70e87f42c4741e6a448bec11998fcc82329",
)

http_archive(
    name = "bazel_gazelle",
    urls = ["https://github.com/bazelbuild/bazel-gazelle/releases/download/0.17.0/bazel-gazelle-0.17.0.tar.gz"],
    sha256 = "3c681998538231a2d24d0c07ed5a7658cb72bfb5fd4bf9911157c0e9ac6a2687",
)

BAZEL_BUILD_TOOLS_SHA = "f8fc3cbc809e100a8ced163e35bde46f8e6453f5"

http_archive(
    name = "com_github_bazelbuild_buildtools",
    strip_prefix = "buildtools-"+BAZEL_BUILD_TOOLS_SHA,
    url = "https://github.com/bazelbuild/buildtools/archive/"+BAZEL_BUILD_TOOLS_SHA+".zip",
)

ATLASSIAN_BAZEL_TOOLS_SHA = "c7e0fd9070f04f88bf671e57f101aa0877a9b5c8"

http_archive(
    name = "com_github_atlassian_bazel_tools",
    strip_prefix = "bazel-tools-"+ATLASSIAN_BAZEL_TOOLS_SHA,
    urls = ["https://github.com/atlassian/bazel-tools/archive/"+ATLASSIAN_BAZEL_TOOLS_SHA+".zip"],
)

git_repository(
    name = "io_bazel_rules_docker",
    commit = "f40c92d1b30ff758a66aba7578039cbf959aea62",
    remote = "https://github.com/bazelbuild/rules_docker.git",
)

git_repository(
    name = "io_bazel_rules_k8s",
    commit = "87de67e50c1135a6b6bd0f1401f004bf7c711c42",
    remote = "https://github.com/bazelbuild/rules_k8s.git",
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains()

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

gazelle_dependencies()

load("@com_github_bazelbuild_buildtools//buildifier:deps.bzl", "buildifier_dependencies")

buildifier_dependencies()

load("@com_github_atlassian_bazel_tools//goimports:deps.bzl", "goimports_dependencies")

goimports_dependencies()

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)
load(
    "@io_bazel_rules_docker//go:image.bzl",
    _go_image_repos = "repositories",
)

_go_image_repos()

load("@io_bazel_rules_k8s//k8s:k8s.bzl", "k8s_repositories")

k8s_repositories()
