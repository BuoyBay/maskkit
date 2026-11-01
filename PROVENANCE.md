# Source and scope

Inspected [npalardy/MaskedEditField](https://github.com/npalardy/MaskedEditField)
at commit `6588676311f223e0a8e4105252cf59ed8a27a91f` on 2026-10-31.
The repository's LICENSE is MIT, copyright 2022 npalardy. Its README and
`MaskedField.xojo_code` were inspected, particularly the embedded documentation
and matching/input event methods. No upstream source or artwork is copied into
this independently implemented package.

The original subclasses an edit field, intercepts typing/paste, supports multiple
masks and includes `#`, `L`, `l`, `A`, `.`, `*`, escapes and `^` negation. MaskKit
implements the common positive grammar as an independent pure model, with
explicit raw formatting, prefix/complete states, bounded alternatives and error
coordinates. It does not implement negation, TextField subclass events,
selection-aware replacement, caret behavior, key rejection notifications,
native undo or IME guarantees. ASCII classes are intentional and need not match
every legacy Xojo character-class behavior.

Verification uses independent expected formatting and actual sealed package
imports. The original implementation is context, not a correctness oracle.
