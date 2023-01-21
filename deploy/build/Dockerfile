FROM golang:1.19-alpine AS builder

WORKDIR /app
COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -ldflags "-s -w" -o /app/go-template

RUN apk add upx
RUN upx --ultra-brute /app/go-template

FROM scratch AS prod
COPY --from=builder /app/go-template /bin/go-template
ENTRYPOINT ["/bin/go-template"]
