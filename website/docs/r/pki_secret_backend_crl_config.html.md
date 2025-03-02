---
layout: "vault"
page_title: "Vault: vault_pki_secret_backend_crl_config resource"
sidebar_current: "docs-vault-resource-pki-secret-backend-crl-config"
description: |-
  Sets the CRL config on an PKI Secret Backend for Vault.
---

# vault\_pki\_secret\_backend\_crl\_config

Allows setting the duration for which the generated CRL should be marked valid. If the CRL is disabled, it will return a signed but zero-length CRL for any request. If enabled, it will re-build the CRL.

## Example Usage

```hcl
resource "vault_mount" "pki" {
  path                      = "%s"
  type                      = "pki"
  default_lease_ttl_seconds = 3600
  max_lease_ttl_seconds     = 86400
}

resource "vault_pki_secret_backend_crl_config" "crl_config" {
  backend = vault_mount.pki.path
  expiry  = "72h"
  disable = false
}
```

## Argument Reference

The following arguments are supported:

* `namespace` - (Optional) The namespace to provision the resource in.
  The value should not contain leading or trailing forward slashes.
  The `namespace` is always relative to the provider's configured [namespace](/docs/providers/vault#namespace).
   *Available only for Vault Enterprise*.

* `backend` - (Required) The path the PKI secret backend is mounted at, with no leading or trailing `/`s.

* `expiry` - (Optional) Specifies the time until expiration.

* `disable` - (Optional) Disables or enables CRL building.

## Attributes Reference

No additional attributes are exported by this resource.
