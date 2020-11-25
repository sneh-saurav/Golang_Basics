package main

import (
	"bufio"
	"fmt"
	"net"
)

func check(err error, message string) {
	if err != nil {
		panic(err)
	}
	fmt.Printf("%s\n", message)
}

func main() {
	len, err := net.Listen("tcp", ":5050")
	check(err, "Welcome to my server :")

	for {
		conn, err := len.Accept()
		check(err, "Connection establish.")

		go func() {
			buf := bufio.NewReader(conn)
			for {
				chk, err := buf.ReadString('\n')
				if err != nil {
					fmt.Printf("WELCOME \n")
					break
				}

				conn.Write([]byte("Hello_Everyone, " + chk))
			}
		}()
	}
}
