# grok2api 自动补丁构建

这个分支只放构建工作流,不含源码。

- 补丁:分支 `patch/include-optin`(Console 不再强制 `include: reasoning.encrypted_content`,
  避免 multi-agent + 搜索时回复超过 128 MiB 被截断)。
- 工作流 `Build patched image`:每天检查上游 `chenyme/grok2api` 最新 release,
  打补丁 → `go test ./...` → 构建 arm64 镜像 → `ghcr.io/yjl-debug/grok2api:<tag>-include-optin`
  与 `latest-include-optin`。
- 补丁冲突或测试失败时工作流失败,GitHub 会发邮件。
- 手动触发:Actions → Build patched image → Run workflow(可填 tag、可强制重建)。
