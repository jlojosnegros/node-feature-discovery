---
name: New Patch Release
about: Cut a new patch release
title: Release v0.x.y
assignees: adrianchiris, ArangoGutierrez, fmuyassarov, jjacobelli, kad, marquiz, PiotrProkop, zvonkok

---

## Release Checklist
<!--
Please do not remove items from the checklist
-->
- [ ] Verify that the changelog in this issue is up-to-date
- [ ] Run `hack/prepare-release.sh $VERSION` to turn references to point to the upcoming release
      (README, deployment templates, docs configuration, test/e2e flags), submit a PR against the release branch
- An OWNER prepares a draft release
  - [ ] Create a draft release at [Github releases page](https://github.com/kubernetes-sigs/node-feature-discovery/releases)
  - [ ] Write the change log into the draft release
  - [ ] Upload release artefacts generated by `prepare-release.sh` script above to the draft release
- [ ] An OWNER runs
     `git tag -s $VERSION`
      and inserts the changelog into the tag description.
- [ ] An OWNER pushes the tag with
      `git push $VERSION`
  - Triggers prow to build and publish a staging container image
      `gcr.io/k8s-staging-nfd/node-feature-discovery:$VERSION`
  - Triggers build of the documentation and publish it at
        https://kubernetes-sigs.github.io/node-feature-discovery/0.$MAJ/
- [ ] Submit a PR against [k8s.io](https://github.com/kubernetes/k8s.io), updating `registry.k8s.io/images/k8s-staging-nfd/images.yaml` to promote the container images (both "full" and "minimal" variants) to production
- [ ] Wait for the PR to be merged and verify that the image (`registry.k8s.io/nfd/node-feature-discovery:$VERSION`) is available.
- [ ] Publish the draft release prepared at the [Github releases page](https://github.com/kubernetes-sigs/node-feature-discovery/releases)
      which will also trigger a Helm repo index update to add the latest release
- [ ] Add a link to the tagged release in this issue.
- [ ] For a point release of the latest newest release branch, update README in master branch
  - [ ] Update references e.g. by running `hack/prepare-release.sh $VERSION` but **only** committing README.md, and,
        submit a PR
  - [ ] Wait for the PR to be merged
- [ ] Close this issue


## Changelog
<!--
Describe changes since the last release here.
-->
