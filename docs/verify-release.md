# Verifying the Package Release

This package is published as an OCI artifact, signed with Sigstore [Cosign](https://docs.sigstore.dev/cosign/overview), and associated with a [SLSA Provenance](https://slsa.dev/provenance) attestation.

Using `cosign`, you can display the supply chain security related artifacts for the `ghcr.io/kadras-io/package-for-service-binding` images. Use the specific digest you'd like to verify.

```shell
cosign tree ghcr.io/kadras-io/package-for-service-binding
```

The result:

```shell
📦 Supply Chain Security Related artifacts for an image: ghcr.io/kadras-io/package-for-service-binding
└── 💾 Attestations for an image tag: ghcr.io/kadras-io/package-for-service-binding:sha256-23498b64d519fdbe964817cb683359010d0bb8f203ab91e46cfdbcec26cf9df6.att
   └── 🍒 sha256:4854b4a9e42b021a3a668b04b815ba26b1d8980f951ad5f8518f70c4fcf95189
└── 🔐 Signatures for an image tag: ghcr.io/kadras-io/package-for-service-binding:sha256-23498b64d519fdbe964817cb683359010d0bb8f203ab91e46cfdbcec26cf9df6.sig
   └── 🍒 sha256:9cbaac0c56f9823666a9be774f8ba5b188611817c064698cd8edd39c7187dcbb
```

You can verify the signature and its claims:

```shell
cosign verify \
   --certificate-identity-regexp https://github.com/kadras-io \
   --certificate-oidc-issuer https://token.actions.githubusercontent.com \
   ghcr.io/kadras-io/package-for-service-binding | jq
```

You can also verify the SLSA Provenance attestation associated with the image.

```shell
cosign verify-attestation --type slsaprovenance \
   --certificate-identity-regexp https://github.com/slsa-framework \
   --certificate-oidc-issuer https://token.actions.githubusercontent.com \
   ghcr.io/kadras-io/package-for-service-binding | jq .payload -r | base64 --decode | jq
```
