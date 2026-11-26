# claude-cheby

Cheby support for [Claude Code](https://code.claude.com): a plugin that connects the Cheby language server, `cheby lsp`, to `.cheby` files.

With it, Claude Code reads the diagnostics `cheby check` reports after each edit of a Cheby file, and can ask the server for definitions, references, types, symbols and call hierarchies.

## Install

1. Install `cheby` and put it on your `PATH`. From a checkout of [cheby](https://github.com/cheby-lang/cheby):

   ```sh
   cargo install --path crates/cheby_cli --locked
   ```

2. Add this repository as a marketplace and install the plugin. From a clone:

   ```sh
   claude plugin marketplace add /path/to/claude-cheby
   claude plugin install cheby@cheby-lang
   ```

   From GitHub, the first line is `claude plugin marketplace add cheby-lang/claude-cheby`.

3. Start Claude Code in a Cheby package. The server starts with the first `.cheby` file Claude edits.

After you pull a new version, run `claude plugin marketplace update cheby-lang`.

## What it runs

The plugin runs `cheby lsp`, with `cheby` found on the `PATH` of the shell that starts `claude`. It sends no settings, so the server uses its defaults. The server is the one the [Zed extension](https://github.com/cheby-lang/zed-cheby) runs.

The server is as new as the `cheby` on your `PATH`. After you update Cheby, install it again, or Claude Code keeps the diagnostics of the old version.

## If it does not work

- `which cheby` must print a path in the shell you start `claude` from.
- `/plugin` in Claude Code lists the plugin and, under Errors, says why a server did not start.
- `claude --debug` writes a log under `~/.claude/debug/`, with a line for a server that fails to start.

## Layout

| Path                                       | What it is                                    |
| ------------------------------------------ | --------------------------------------------- |
| `.claude-plugin/marketplace.json`          | The marketplace, with one plugin              |
| `plugins/cheby/.claude-plugin/plugin.json` | The plugin's manifest                         |
| `plugins/cheby/.lsp.json`                  | The language server: its command and its files |
