# Dockerfile Review Guide

Apply this guide to Dockerfiles, including named variants such as
`Dockerfile.dev` and `app.Dockerfile`. Use it alongside the guides for the
application code and build tools involved; a Dockerfile does not replace those
guides.

## Image and build correctness

- Verify the selected base image, architecture, and runtime match the
  application. Treat mutable tags as a reproducibility risk; check whether
  pinning to a digest is appropriate for the repository's update process.
- Check multi-stage builds and `COPY --from` paths so build-only tools and
  development dependencies do not leak into the runtime image unnecessarily.
- Review instruction ordering, cache behavior, and package installation for
  reliable rebuilds. Confirm cleanup is effective in the same layer where
  package caches are created; do not recommend cache-busting or pinning without
  considering the project's update and security workflow.
- Check `WORKDIR`, `COPY`/`ADD` sources, file ownership, and the final
  `ENTRYPOINT`/`CMD` against the app's expected paths, startup behavior, and
  graceful signal handling. Prefer exec-form commands when shell behavior is
  not needed.
- Treat `EXPOSE` as image metadata, not as a network access control. Verify
  health checks against an actual application readiness signal when one is
  defined, and avoid duplicating orchestration-specific checks without reason.

## Security

- Check the final runtime user and file permissions. Flag root execution,
  added Linux capabilities, or privileged behavior only with evidence about
  the workload and its deployment constraints.
- Trace build inputs and scripts, including `ARG`, remote downloads, package
  sources, and shell commands. Avoid unsafe downloads or execution of
  unverified scripts; preserve integrity and provenance checks where used.
- Ensure secrets are not passed through `ARG` or persisted in image layers
  through `ENV`, copied files, generated artifacts, or build output. Use the
  repository's supported build-secret mechanism and keep runtime secrets in
  the deployment's secret-management path.
- Check that the build context is appropriately constrained by `.dockerignore`,
  especially for credentials, local configuration, source-control metadata,
  and generated files that are not required by the build.
- Review package and image sources for unexpected registries, untrusted
  versions, and supply-chain changes. Do not treat a version pin alone as
  proof that an artifact is trustworthy.
