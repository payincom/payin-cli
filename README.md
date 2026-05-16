# PayIn CLI

`payin` is the operator CLI for PayIn runtimes. It is a runtime operations client, not an installer or deployment tool.

It is intended to work with:

- PayIn Open self-hosted runtimes
- PayIn Cloud hosted runtimes
- future enterprise/partner PayIn runtime overlays

## Install

During local development:

```bash
npm install
npm run build
npm run dev -- --help
```

After package publishing:

```bash
npm install -g @payin/cli
payin --help
```

or:

```bash
npx @payin/cli --help
```

## Profiles

```bash
payin profile add open-local http://localhost:3000
payin profile use open-local
payin profile list
```

Profiles are stored under `PAYIN_CONFIG` when set, otherwise in the user config directory.

## Runtime diagnostics

```bash
payin --profile open-local doctor
payin --profile open-local smoke --create-order --webhook-id <endpoint-id> --require-live
```

## Operator commands

```bash
payin --profile open-local login --username <email> --password <password> --save
payin --profile open-local whoami
payin --profile open-local chains
payin --profile open-local tokens
payin --profile open-local api-key list
payin --profile open-local api-key create --name agent-integration
payin --profile open-local address-pool status --protocol evm
payin --profile open-local address-pool import addresses.txt --protocol evm
payin --profile open-local webhooks list
payin --profile open-local webhooks test <endpoint-id>
```

All runtime operation commands support `--json` for Agent-friendly structured output.

## Boundary

The CLI talks to PayIn runtimes through HTTP APIs. It must not depend on PayIn Open internals, processor internals, database schemas, or deployment-specific infrastructure.

Deployment remains the responsibility of Docker, Compose, Railway/Fly/Render/VPS/Kubernetes, Terraform/Helm/Ansible, and PayIn Open self-hosting runbooks.
