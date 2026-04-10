Environment notes:
- Running in NemoClaw/OpenClaw sandbox on ASUS GX10.
- Sandbox name: chief.
- Host access may be mediated through NemoClaw/OpenShell.
- Use caution with commands that assume direct host persistence.
- Network policies currently enabled include brave, discord, npm, pypi, huggingface.

Operational notes:
- Ask before destructive actions.
- Prefer diagnostics before mutation.
- Prefer minimal changes with clear rollback path.

Git / GitHub workflow notes:
- The workspace git repository is inside /sandbox/.openclaw/workspace.
- Commits should be created from inside the chief sandbox.
- Direct git push from inside the sandbox may fail because HTTPS certificate verification is blocked by the sandbox proxy/TLS environment.
- Host-side GitHub SSH works, but the sandbox itself does not have a working ssh client for git push.
- Reliable workflow:
  1. Edit and commit inside the sandbox.
  2. Push from the host using the approved docker/kubectl push wrapper.
- Do not disable SSL verification.
- Do not assume host paths like /sandbox/... exist outside the sandbox.
- Before git operations, confirm whether the current shell is host or sandbox.

Approved host push command:
sudo docker exec -it openshell-cluster-nemoclaw sh -lc 'kubectl exec -it -n openshell chief -- sh -lc "git config --global --add safe.directory /sandbox/.openclaw-data/workspace >/dev/null 2>&1; cd /sandbox/.openclaw/workspace && git push"'
