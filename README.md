# Node Shelf

Hide the node packs, or the single nodes, you don't use. A hidden node leaves ComfyUI's node search (double click),
the node library and the right-click Add Node menu. It stays installed, so a workflow that uses it still loads and
runs. Nothing is uninstalled and nothing touches the server.

**Status: new (2026-11-12).** Tested on ComfyUI interface 1.59.1 in one browser on one machine.

## Use it

Open the command palette and type **Node Shelf**, or use the Extensions menu.

- **A whole pack:** untick it. Nodes that pack adds in a later update are hidden too.
- **Some nodes of a pack:** open the pack with its arrow and untick them. Nodes the pack adds later will show.
- **Everything except a few:** untick the pack, open it, tick the ones you use.
- **ComfyUI's own nodes** are listed apart, in four groups: built-in nodes, API nodes (paid services), blueprints, and
  interface nodes (notes, reroutes).
- **Search** finds a node in any pack by name, class name or category. **Show: Hidden** lists only what is hidden.
  The line above the list always says how many nodes are hidden; **Show everything** undoes all of it.
- A node the open workflow uses is marked "in this workflow".

Changes apply at once and are kept with your ComfyUI settings (`NodeShelf.Hidden`), so they follow your account
across browsers.

## Install

Clone into `ComfyUI/custom_nodes/` and reload the page:

```
git clone https://github.com/matlowai/comfyui-node-shelf
```

It has no Python dependencies and no nodes of its own.

**With ComfyUI-MAINodes:** MAINodes ships the same file. Installing both is fine: whichever loads first runs, the
other does nothing, and they share the one setting.

## What it needs, and its limits

- A ComfyUI interface with the node filter list: about August 2025 (1.26) or later. On an older one the dialog says so
  and hides nothing. Checked by reading the released code of 1.26.2, 1.32.4, 1.43.18 and 1.49.6; run only on 1.59.1.
- The filter list is ComfyUI's own (it hides deprecated and experimental nodes with it), but an extension reaches it
  through the interface's internals, which are not a documented door. If a future interface moves them, Node Shelf
  says it can't hide anything and your nodes all show again; your saved choices are kept.
- Not tested with a screen reader. Built for one: a native modal dialog, real checkboxes with names, every action by
  keyboard, each change announced.

## Test

`tests/test_node_shelf.js` drives a real ComfyUI page (Playwright). It writes the setting, so point it at a throwaway
server, never your own:

```
NS_EXT=comfyui-node-shelf NS_PACK=core NS_NODE=KSampler NS_QUERY=KSampler \
  NODE_PATH=<playwright's node_modules> node tests/test_node_shelf.js <port>
```

## Licence

GPL-3.0, see `LICENSE`.
