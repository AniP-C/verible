# This package contains functions and classes related to analysis of
# structural representations of Verilog/SystemVerilog source code.

licenses(["notice"])

default_visibility = [
    "//verilog:__subpackages__",
]

package(
    default_visibility = default_visibility,
)

cc_library(
    name = "default_rules",
    hdrs = ["default_rules.h"],
    deps = [
        "//verilog/analysis/checkers:verilog_lint_rules",
    ],
)

cc_test(
    name = "default_rules_test",
    srcs = ["default_rules_test.cc"],
    deps = [
        ":default_rules",
        ":lint_rule_registry",
        "//verilog/analysis/checkers:verilog_lint_rules",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "descriptions",
    srcs = ["descriptions.cc"],
    hdrs = ["descriptions.h"],
    deps = ["@com_google_absl//absl/strings"],
    alwayslink = 1,
)

cc_library(
    name = "lint_rule_registry",
    srcs = ["lint_rule_registry.cc"],
    hdrs = ["lint_rule_registry.h"],
    deps = [
        ":descriptions",
        "//common/analysis:line_lint_rule",
        "//common/analysis:syntax_tree_lint_rule",
        "//common/analysis:text_structure_lint_rule",
        "//common/analysis:token_stream_lint_rule",
        "//common/strings:compare",
        "//common/util:container_util",
        "//common/util:logging",
        "@com_google_absl//absl/container:node_hash_map",
        "@com_google_absl//absl/strings",
    ],
)

cc_test(
    name = "descriptions_test",
    srcs = ["descriptions_test.cc"],
    deps = [
        ":descriptions",
        "@com_google_absl//absl/strings",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_test(
    name = "lint_rule_registry_test",
    srcs = ["lint_rule_registry_test.cc"],
    deps = [
        ":descriptions",
        ":lint_rule_registry",
        "//common/analysis:line_lint_rule",
        "//common/analysis:lint_rule_status",
        "//common/analysis:syntax_tree_lint_rule",
        "//common/analysis:text_structure_lint_rule",
        "//common/analysis:token_stream_lint_rule",
        "//common/text:concrete_syntax_leaf",
        "//common/text:concrete_syntax_tree",
        "//common/text:syntax_tree_context",
        "//common/text:text_structure",
        "//common/text:token_info",
        "@com_google_absl//absl/strings",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "verilog_analyzer",
    srcs = [
        "verilog_analyzer.cc",
        "verilog_excerpt_parse.cc",
        # paired together because of mutual recursion
    ],
    hdrs = [
        "verilog_analyzer.h",
        "verilog_excerpt_parse.h",
    ],
    deps = [
        "//common/analysis:file_analyzer",
        "//common/lexer:token_stream_adapter",
        "//common/strings:comment_utils",
        "//common/text:concrete_syntax_leaf",
        "//common/text:concrete_syntax_tree",
        "//common/text:symbol",
        "//common/text:text_structure",
        "//common/text:token_info",
        "//common/text:token_stream_view",
        "//common/text:visitors",
        "//common/util:container_util",
        "//common/util:logging",
        "//common/util:status_macros",
        "//verilog/parser:verilog_lexer",
        "//verilog/parser:verilog_lexical_context",
        "//verilog/parser:verilog_parser",
        "//verilog/parser:verilog_token_classifications",
        "//verilog/parser:verilog_token_enum",
        "//verilog/preprocessor:verilog_preprocess",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "verilog_equivalence",
    srcs = ["verilog_equivalence.cc"],
    hdrs = ["verilog_equivalence.h"],
    deps = [
        "//common/lexer:token_stream_adapter",
        "//common/text:token_info",
        "//common/text:token_stream_view",
        "//common/util:enum_flags",
        "//common/util:logging",
        "//verilog/parser:verilog_lexer",
        "//verilog/parser:verilog_parser",
        "//verilog/parser:verilog_token_classifications",
        "//verilog/parser:verilog_token_enum",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "verilog_linter_configuration",
    srcs = ["verilog_linter_configuration.cc"],
    hdrs = ["verilog_linter_configuration.h"],
    deps = [
        ":default_rules",
        ":lint_rule_registry",
        "//common/analysis:line_lint_rule",
        "//common/analysis:syntax_tree_lint_rule",
        "//common/analysis:text_structure_lint_rule",
        "//common/analysis:token_stream_lint_rule",
        "//common/util:container_util",
        "//common/util:enum_flags",
        "//common/util:file_util",
        "//common/util:logging",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "verilog_linter_constants",
    hdrs = ["verilog_linter_constants.h"],
)

cc_library(
    name = "verilog_linter",
    srcs = ["verilog_linter.cc"],
    hdrs = ["verilog_linter.h"],
    deps = [
        ":default_rules",
        ":lint_rule_registry",
        ":verilog_analyzer",
        ":verilog_linter_configuration",
        ":verilog_linter_constants",
        "//common/analysis:line_lint_rule",
        "//common/analysis:line_linter",
        "//common/analysis:lint_rule_status",
        "//common/analysis:lint_waiver",
        "//common/analysis:syntax_tree_lint_rule",
        "//common/analysis:syntax_tree_linter",
        "//common/analysis:text_structure_lint_rule",
        "//common/analysis:text_structure_linter",
        "//common/analysis:token_stream_lint_rule",
        "//common/analysis:token_stream_linter",
        "//common/strings:line_column_map",
        "//common/text:concrete_syntax_tree",
        "//common/text:text_structure",
        "//common/text:token_info",
        "//common/util:file_util",
        "//common/util:logging",
        "//verilog/parser:verilog_token_classifications",
        "//verilog/parser:verilog_token_enum",
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
    ],
)

cc_test(
    name = "verilog_analyzer_test",
    srcs = ["verilog_analyzer_test.cc"],
    deps = [
        ":verilog_analyzer",
        "//common/analysis:file_analyzer",
        "//common/text:concrete_syntax_leaf",
        "//common/text:concrete_syntax_tree",
        "//common/text:constants",
        "//common/text:symbol",
        "//common/text:text_structure",
        "//common/text:token_info",
        "//common/text:token_info_test_util",
        "//common/text:token_stream_view",
        "//common/text:tree_utils",
        "//common/util:casts",
        "//common/util:logging",
        "//verilog/parser:verilog_parser",
        "//verilog/parser:verilog_token_enum",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_test(
    name = "verilog_linter_configuration_test",
    srcs = ["verilog_linter_configuration_test.cc"],
    deps = [
        ":default_rules",
        ":descriptions",
        ":lint_rule_registry",
        ":verilog_linter",
        ":verilog_linter_configuration",
        "//common/analysis:line_lint_rule",
        "//common/analysis:lint_rule_status",
        "//common/analysis:syntax_tree_lint_rule",
        "//common/analysis:text_structure_lint_rule",
        "//common/analysis:token_stream_lint_rule",
        "//common/strings:line_column_map",
        "//common/text:concrete_syntax_leaf",
        "//common/text:concrete_syntax_tree",
        "//common/text:syntax_tree_context",
        "//common/text:text_structure",
        "//common/text:token_info",
        "//common/text:tree_builder_test_util",
        "@com_google_absl//absl/strings",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_test(
    name = "verilog_linter_test",
    srcs = ["verilog_linter_test.cc"],
    deps = [
        ":default_rules",
        ":verilog_analyzer",
        ":verilog_linter",
        ":verilog_linter_configuration",
        "//common/util:file_util",
        "//common/util:logging",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_test(
    name = "verilog_equivalence_test",
    srcs = ["verilog_equivalence_test.cc"],
    deps = [
        ":verilog_equivalence",
        "//common/text:token_info",
        "//common/util:logging",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
    ],
)
