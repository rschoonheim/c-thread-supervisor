FROM almalinux:10 AS builder

# Install C compiler and other build dependencies
# -------------------------------------------------------
#
RUN dnf groupinstall -y "Development Tools" \
    && dnf install -y curl \
    && dnf clean all

# Install CMake 4.2
# -------------------------------------------------------
#
RUN curl -fsSL -o /tmp/cmake.sh https://cmake.org/files/v4.2/cmake-4.2.0-linux-x86_64.sh \
    && sh /tmp/cmake.sh --skip-license --prefix=/usr/local \
    && rm -f /tmp/cmake.sh

# Set working directory
# -------------------------------------------------------
#
WORKDIR /build

# Copy source code to the container
# -------------------------------------------------------
#
COPY . /build

# Build the project
# -------------------------------------------------------
#
RUN mkdir -p build && cd build \
    && cmake .. \
    && make


FROM almalinux:10 AS runtime

WORKDIR /app

COPY --from=builder /build/build/thread_supervisor /app/thread_supervisor

CMD ["./thread_supervisor"]