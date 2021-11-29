# Lean HTML documentation generator

A tool to generate documentation for [mathlib](https://github.com/leanprover-community/mathlib/).

## Requirements

This script is not Windows friendly.

It depends on features of Lean 3.5c added in
<https://github.com/leanprover-community/lean/pull/81>.

```
pip install -r requirements.txt
rm -rf _target
```

If generating documentation for mathlib:
  ```
  leanproject up
  ./gen_docs
  ```

If generating documentation for a project that depends (transitively) on mathlib:
  Remove `mathlib` from `leanpkg.toml`.
  Add `scripts/mk_all.sh` and `scripts/rm_all.sh` to your project at the root.
  Add `your_project_name` to `leanpkg.toml` (it must be a git repo with remote `origin` to a public url).
  Upgrade `lean_version` in `leanpkg.toml` to match the version used by your project.
  ```
  leanpkg configure
  ./gen_docs -r _target/deps/your_project_name/
  ```

The directory `html` will contain the generated documentation.

Make sure that olean files are generated for mathlib in `_target`, otherwise this will be extremely slow.

## Usage

The links will point to `/` as the root of the site.
I typically host a server from the `html` directory with `python3 -m http.server`.
If you intend to host the site somewhere else than the root,
call for example `./gen_docs -w 'https://lean.com/my-documentation/'`.

`gen_docs -l` will symlink the css file, so you can edit `style.css` in the root directory
without regenerating anything. This is useful for local development.
