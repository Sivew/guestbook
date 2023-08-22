FROM golang as builder
WORKDIR /app/main
COPY main.go .
RUN go mod init greet
RUN go get github.com/gorilla/mux
RUN go get github.com/urfave/negroni
RUN go get github.com/xyproto/simpleredis@v1.2.6.1
RUN go mod tidy
RUN go build

FROM ubuntu:lunar
RUN apt update
COPY --from=builder /app/main /app/guestbook
WORKDIR /app/guestbook/
ADD public ./public/
RUN ls 
CMD ["./greet"]
EXPOSE 3000