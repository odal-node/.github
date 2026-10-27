## Summary

<!-- What this change does and why, in one paragraph, for someone who has not read
     the issue. -->

## Related issue

<!-- "Closes #123", or "none" and the reason this did not need one. -->

## Changes

<!-- The main changes, as bullets. -->

## Regulatory claims

<!-- Delete this section if the change touches no regulation.

     Otherwise, for every date, threshold, product scope, act number or standard
     reference added or changed, name the PRIMARY SOURCE you read yourself.
     A secondary summary is not a source. If a value comes from a secondary source
     and you could not verify it, say so here and do not encode it as a constant. -->

## Checklist

- [ ] The repository's full check suite passes locally, not only the unit tests
- [ ] Tests cover the new behaviour, including the failure it prevents
- [ ] Commits are signed off (`git commit -s`) and carry no AI attribution
- [ ] No secrets, credentials, keystores or `.env` files in the diff
- [ ] No real company name in a test fixture
- [ ] No hard-coded version, date or deadline added to a document
- [ ] Nothing stubbed or marked `TODO` (otherwise, open this as a draft)
- [ ] Public API or schema changes are documented, and the CHANGELOG entry is under
      the right heading (a breaking change is never `Added`)
- [ ] Documentation follows the [style guide](https://github.com/odal-node/.github/blob/main/DOCS-STYLE.md)
- [ ] No non-public repository, path or internal planning identifier is named
