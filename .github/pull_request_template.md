## Summary

<!-- What does this change do, and why? One paragraph. Write it for someone who has
     not read the issue. -->

## Related issue

<!-- Closes #123 — or "none, and here is why this did not need one". -->

## Changes

<!-- The main changes, as bullets. -->

## Regulatory claims

<!-- Delete this section if the change touches no regulation.

     Otherwise: for every date, threshold, product scope, act number or standard
     reference added or changed, name the PRIMARY SOURCE you personally read.
     A secondary summary is not a source. If a value is secondary-sourced and
     you could not verify it, say so here and do not encode it as a constant. -->

## Checklist

- [ ] The repository's own checks pass locally — not only the test subset
- [ ] Tests cover the new behaviour, including the failure it is meant to prevent
- [ ] Commits are signed off (`git commit -s`) and carry no AI attribution
- [ ] No secrets, credentials, keystores or `.env` files in the diff
- [ ] No real company name in a test fixture
- [ ] No hardcoded version, date or deadline added to a document
- [ ] Nothing left stubbed or `TODO`-ed — otherwise open this as a draft
- [ ] Public API or schema changes are documented, and the CHANGELOG entry is filed
      under the correct heading (a break is never `Added`)
- [ ] This PR names no non-public repository, path, or internal planning identifier
