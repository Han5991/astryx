---
'@astryxdesign/build': patch
---

[fix] Declare `postcss` as an optional peer dependency of `@astryxdesign/build`, which the `./postcss` entry requires at load time
@Han5991

The PostCSS entry has required `postcss` since it was introduced, but the
package never declared it, so it resolved only where the installer happened to
hoist a copy; strict installs such as Yarn Plug'n'Play refuse an undeclared
require. It is a peer, as the PostCSS plugin guidelines ask, so the plugin works
on the host's `postcss` AST rather than its own copy, and it is optional because
the Babel, Vite and Next entries never load it.
