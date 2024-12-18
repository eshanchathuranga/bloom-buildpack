# bin/detect
#!/usr/bin/env bash
if [ -f "package.json" ]; then
  exit 0
fi
exit 1

# bin/compile
#!/usr/bin/env bash

# Install Node.js and npm (or yarn)
# (You might need to adjust this based on your Node.js version requirements)
curl -sL https://deb.nodesource.com/setup_22.9 | bash -
apt-get install -y nodejs

# Install dependencies
npm install --production

# Cache node_modules for faster subsequent builds
if [ -d "node_modules" ]; then
  cp -r node_modules $CACHE_DIR
fi

# Clean up any old cached node_modules
rm -rf node_modules
if [ -d "$CACHE_DIR/node_modules" ]; then
  cp -r $CACHE_DIR/node_modules .
fi

# Add  start script to your package.json if it doesn't exist
if ! grep -q '"start":' package.json; then
  echo '"start": "node index.js",' >> package.json
fi

# bin/release (optional)
#!/usr/bin/env bash
cat <<EOF
---
web: npm start
EOF
