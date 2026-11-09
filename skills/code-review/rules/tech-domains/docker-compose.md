# Docker Compose Review Guide

Apply this guide to Docker Compose manifests such as `docker-compose.yml`,
`docker-compose.yaml`, `compose.yml`, and `compose.yaml`. When a change also
touches a Dockerfile or application code, load those applicable guides too.

## Service behavior and operability

- Check that each service's image or build context, command, working
  directory, environment, mounts, and exposed ports match the intended
  runtime. Verify relative paths against the Compose project directory and
  any explicit project configuration.
- Check startup ordering separately from readiness. When a dependent service
  must be ready before another starts, verify a meaningful health check and a
  supported readiness condition rather than relying on container start order.
- Review restart policies, stop timeouts, health checks, and resource settings
  against the deployment environment and Compose implementation. Do not assume
  a setting is enforced identically by local Compose, Swarm, and other
  orchestrators.
- Check named volumes, bind mounts, and mount modes for data persistence,
  expected host paths, and accidental overwrites of image files. Consider
  backup and migration implications when persistent data paths change.
- Review service-to-service networks and published ports for the intended
  reachability. A published port may be reachable beyond the local machine
  depending on its host binding and environment.

## Security

- Check for unnecessary `privileged` mode, host namespace sharing, devices,
  added capabilities, Docker socket mounts, and writable host mounts. Treat
  these as high-impact access to the host and verify whether each is required.
- Ensure credentials are not committed in the manifest or environment files.
  Check environment interpolation and the deployment path for required values;
  use Compose secrets or the platform's secret manager where supported by the
  target environment. Environment variables are not, by themselves, a secure
  secret store.
- Review `user`, filesystem permissions, `read_only`, and writable
  `tmpfs`/volume paths in context. Verify the service can operate without
  granting broader access than needed.
- Check network exposure, including published host ports and networks shared
  with unrelated services. Do not assume an internal application port is
  externally reachable unless it is published or exposed by another layer.
- Verify profiles, overrides, and interpolated configuration do not
  unintentionally enable debug services, weaken protections, or expose
  development-only credentials in the target deployment.
