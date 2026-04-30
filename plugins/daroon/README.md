# Daroon Codex Plugin

Daroon provides local-first personal context skills for Codex and similar agents.

The skills are intentionally file-first: agents should use `~/.daroon/current` as the stable workspace pointer, read durable context before acting, capture future-useful continuity as lightweight logs, and curate stable facts into maintained project, person, and topic pages.

If the workspace pointer is missing or broken, the `daroon-setup` skill is responsible for inspecting and repairing setup before normal Daroon work continues.
