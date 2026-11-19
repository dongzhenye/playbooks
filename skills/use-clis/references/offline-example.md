# Try it with a document outline

This fictional example runs locally in a POSIX shell with Git, awk and jq. Use a temporary directory. The catalog format is illustrative; the skill works with other registries.

```sh
set -eu
demo=$(mktemp -d)
mkdir -p "$demo/guide/bin" "$demo/other"
git -C "$demo/guide" init -q
git -C "$demo/other" init -q
cat > "$demo/guide/README.md" <<'DOC'
# Field Guide
## Setup
## Daily use
DOC
cat > "$demo/guide/bin/doc-outline" <<'SH'
#!/bin/sh
set -eu
if [ "${1:-}" = "--help" ]; then
  echo "Usage: doc-outline FILE — list Markdown headings"
  exit 0
fi
[ "$#" -eq 1 ] || exit 2
awk '/^#+ / { sub(/^#+ /, ""); print }' "$1"
SH
chmod +x "$demo/guide/bin/doc-outline"
cat > "$demo/catalog.json" <<'JSON'
[{
  "id": "doc-outline",
  "purpose": "Show the outline of a guide",
  "command": "./bin/doc-outline",
  "source": "guide/bin/doc-outline",
  "run_from": "guide",
  "scope": "project",
  "projects": ["guide"]
}]
JSON
(cd "$demo/other" && jq -r '.[] | select(.purpose | test("outline"; "i")) | .id' ../catalog.json)
(cd "$demo/guide" && ./bin/doc-outline --help && ./bin/doc-outline README.md)
printf 'Fixture: %s\n' "$demo"
```

The search from `other` should return `doc-outline`. Running the command from `guide` should print **Field Guide**, **Setup** and **Daily use**, one per line. These are shell checks. To test an agent:

1. In two disposable project instruction files that your chosen host loads, place the same pointer: “To look up a local CLI by task, search the catalog at [absolute path to catalog.json].” Substitute the fixture's actual path. In a new session in `other`, ask “Which registered tool can show the outline of a guide?” Check the search and the returned execution location.
2. Add one line **only to guide's instructions**: “To show the outline of a guide, run ./bin/doc-outline from the project root.” In a new session there, ask “Show me the outline of the README.” Inspect the trace for the command and compare its output with the three headings.
3. Open a fresh session in `other`. Inspect the host's loaded instructions or skill inventory: the pointer should still be there and the guide-specific hint should be absent. Active lookup should still work.

Use the host's native scope and discovery facilities when available. The two temporary instruction files simulate a user-wide pointer without changing a real user's configuration.
