---
layout: page
title: Advanced
permalink: /advanced/
nav_order: 4
---

# Advanced topics
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Multiword and empty nodes
[Multiword tokens](https://universaldependencies.org/format.html#words-tokens-and-empty-nodes) are supported and can be accessed by calling `n.multi_word`. If `n` belongs to any multiword token, an instance of `udon2.MultiWordNode` will be returned, otherwise the accessor will return `None`. Mutators for multi-word nodes are currently not available. Getting a textual representation of a subtree (by calling `n.get_subtree_text()`) accounts for the multiword nodes. Each multiword node has three accessors: `mw.min_id` (the first ID of a multi-word expression), `mw.max_id` (the last ID of a multiword expression) and `mw.token` (the multiword token itself).

[Empty nodes](https://universaldependencies.org/format.html#words-tokens-and-empty-nodes) are currently ignored while reading CoNLL-U files.

## Pruning vs ignoring [under development]
Suppose we want, as a step in text simplification, to split all coordinate clauses in a sentence into separate sentences. This requires identifying the nodes corresponding to the roots of coordinate clauses, by using the querying functionality from the previous section. Each clause should then be converted to a separate dependency tree, and all coordinate conjunctions should be removed. UDon2 makes this possible via its `n.prune(<rel>)` and `n.make_root()` methods, where `<rel>` corresponds to the chain of dependency relations pointing at the node to be pruned.

![A visualized dependency tree for the sentence "You should study these topics or you will fail the exam"](/assets/images/en_dep_example.png)
To exemplify, consider the tree above and let `r = root.children[0]`, then the following code is valid:
```
r.prune("conj")
r.make_root() # corresponds to the tree of "You should study these topics"
```

If the same tree is going to be used multiple times, destructive pruning might not be a viable option. In order to avoid copying trees, which might be a time-intensive (currently not implemented) operation, UDon2 allows ignoring individual nodes or subtrees by calling `n.ignore(<label>)` (`n.ignore_subtree(<label>)`), which assigns an ignore label `<label>` to `n` (all nodes in a subtree induced by `n`). All ignored nodes (no matter the label) will be excluded for all the queries presented in the previous section and during calling `n.get_subtree_text()`.

Reverting to the original state, possible by calling `n.reset(<label>)` (`n.reset_subtree(<label>)`), will unignore only nodes with a matching ignore label. The `<label>` argument defaults to 0 for all mentioned methods. If all nodes should be reset (no matter the label), `n.hard_reset()` or `n.hard_reset_subtree()` should be used.

## Grouping nodes
Nodes can be grouped based on their properties using `n.group_by(prop)` method, where `prop` is one of `form`, `lemma`, `upos`, `xpos` or `deprel`. The method returns `udon2.GroupedNodes`, which is basically a dictionary with a value of the selected property, as a key, and a `udon2.NodeList` of Nodes having the specified property with this key, as a value.
```
r.group_by("upos")
# returns a udon2.GroupedNodes equivalent to the following dict:
# {
#    'VERB': [Node<study>, Node<fail>],
#    'PRON': [Node<You>, Node<you>],
#    'AUX': [Node<should>, Node<will>],
#    'DET': [Node<these>, Node<the>],
#    'NOUN': [Node<topics>, Node<exam>],
#    'CCONJ': [Node<or>]
# }
```

## Transformations
TBD

## Convolution kernels
TBD
