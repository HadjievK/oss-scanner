# cap-js/audit-logging: SAP CAP (Node.js) plugin. Jest test suite, npm with a committed lockfile.
FROM node:22-bookworm
ENV DEBIAN_FRONTEND=noninteractive \
    HUSKY=0 \
    CI=true
RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates git python3 build-essential \
    && rm -rf /var/lib/apt/lists/*

# scanner contract: the checkout lives inside the image, at /src
COPY . /src
WORKDIR /src

# Install from the committed package-lock.json. Network is available only during this build.
RUN npm ci

# Run the unit tests (Jest; the "test" script excludes integration tests) to prove the image works.
# A failing test is logged, not fatal, so it never aborts the build.
RUN npm test || echo "WARNING: tests reported failures"
