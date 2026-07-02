# gcp-terraform

**Purpose:** Terraform practice project that provisions a static website on GCP served over HTTPS via a global HTTP(S) load balancer + CDN, with a DNS A-record.

## Stack
Terraform, GCP (`google` + `google-beta` providers). Resources in `infra/main.tf`:
- `google_storage_bucket` (`jans_website`, EU) + public `index.html` object.
- Global external IP, managed SSL cert, backend bucket (CDN enabled), URL map, target HTTPS proxy, forwarding rule (`443`).
- DNS `A` record in an existing managed zone `website`.

## Run
```bash
cd infra
terraform init
terraform plan
terraform apply
```
Requires vars `gcp_svc_key`, `gcp_project`, `gcp_region` (see `terraform.tfvars`) and a GCP service-account key JSON.

## Structure
- `infra/` — `.tf` files, `terraform.tfvars`, and committed `terraform.tfstate(.backup)`.
- `website/index.html` — the static site uploaded to the bucket.

## Status/Notes
Practice project (Nov 2023). WARNING: repo contains committed `terraform.tfstate` and a GCP service-account key JSON (`terraformed-404408-*.json`) at the root — treat as sensitive; rotate/remove before sharing.
