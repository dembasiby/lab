# Secret Management with SOPS

## Installation

### Install SOPS

```bash
# Download the binary
curl -LO https://github.com/getsops/sops/releases/download/v3.11.0/sops-v3.11.0.linux.amd64

# Move the binary in to your PATH
mv sops-v3.11.0.linux.amd64 /usr/local/bin/sops

# Make the binary executable
chmod +x /usr/local/bin/sops
```

## Generate key locally

```bash
age-keygen -o age.agekey

cat age.agekey
```
