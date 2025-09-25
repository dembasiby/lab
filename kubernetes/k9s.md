# K9S

## Installation

```bash
# Remove the broken snap
sudo snap remove k9s

# Get latest version (adjust if newer is out)
curl -L https://github.com/derailed/k9s/releases/latest/download/k9s_Linux_amd64.tar.gz -o k9s.tar.gz

# Extract and install
tar -xvzf k9s.tar.gz
sudo mv k9s /usr/local/bin/

# Verify
k9s version
```

