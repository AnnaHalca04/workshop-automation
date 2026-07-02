# Step 1: Build environment. Use a full development image to compile the code.
FROM ubuntu:24.04 AS builder
RUN apt-get update && apt-get install -y gcc
WORKDIR /build
COPY bye.c .
# Compile statically so the binary doesn't depend on external libraries
RUN gcc bye.c -o program_bye -static

# Step 2: Final runtime environment. Extremely lightweight (around 5 MB), contains only the executable.
FROM alpine:latest
WORKDIR /app
COPY --from=builder /build/program_bye .
CMD ["./program_bye"]