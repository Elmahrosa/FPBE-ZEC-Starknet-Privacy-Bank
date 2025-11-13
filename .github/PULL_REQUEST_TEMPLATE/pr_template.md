## Title

<!-- Brief, conventional commit style title e.g. feat(zk): implement zec_light_client with verifier integration -->

## Summary

<!-- One‑paragraph summary of what this PR changes and why -->

## Files changed / added
- List key files touched (e.g., cairo_modules/..., specs/..., tests/..., .github/workflows/...)

## Purpose and scope
- What this PR achieves (spec, implementation, tests, CI, artifacts)
- What it does NOT do (important boundaries)

## Reviewer checklist
- [ ] Spec present and linked: specs/<module>.md
- [ ] Unit tests added and passing: tests/<module>_test.cairo
- [ ] Compiled artifacts: compiled-contracts (Actions → Artifacts)
- [ ] Test artifacts: test-results/combined_test_results.json
- [ ] Proof artifacts: proof-artifacts (circuits job)
- [ ] Verifier smoke tests: verifier-integration job (accepts good, rejects tampered)
- [ ] At least two independent reviewers approve
- [ ] Governance signoff referenced if requesting production activation (issue #)

## How to reproduce (smoke)
Linux (WSL/macOS):
```bash
python3 -m pip install --user cairo-lang
cairo-compile cairo_modules/example.cairo --output /tmp/example.json
cairo-test cairo_modules/example.cairo --test-output /tmp/example_test.json
```