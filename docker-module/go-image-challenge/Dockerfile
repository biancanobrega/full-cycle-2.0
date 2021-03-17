FROM golang:alpine AS builder
WORKDIR /build

COPY go.mod .
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o  main .

FROM scratch AS release
WORKDIR /dist

COPY --from=builder /build/main .

# Command to run when starting the container
CMD ["/dist/main"]