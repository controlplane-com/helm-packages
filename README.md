# Control Plane Helm Packages

Pre-packaged Helm charts used as dependencies in Control Plane Helm templates (e.g. postgres, redis, etcd). They are hosted via GitHub Pages at:

```
https://controlplane-com.github.io/helm-packages
```

This makes them publicly referenceable as a Helm repo without requiring a separate chart museum or registry.

## Adding a New Package or Version

**1. Package the chart**

From the directory containing your chart's `Chart.yaml`:

```bash
helm package .
```

This produces a `.tgz` file (e.g. `redis-3.2.1.tgz`).

**2. Copy the `.tgz` here**

```bash
cp redis-3.2.1.tgz /path/to/helm-packages/
```

**3. Update the index**

From this repo root, run:

```bash
helm repo index . \
  --url https://controlplane-com.github.io/helm-packages \
  --merge index.yaml
```

This merges the new entry into `index.yaml` without removing existing entries.

**4. Commit and push**

GitHub Actions will deploy the updated files to GitHub Pages automatically.