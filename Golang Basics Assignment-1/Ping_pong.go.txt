package main

import (
	"fmt"
	"time"
)

// The pinger prints a ping and waits for a pong
func pinger(pinger <-chan int, ponger chan<- int) {
	for i := 0; i < 5; i++ {
		<-pinger
		fmt.Println("ping")
		time.Sleep(1 * time.Second)
		ponger <- 1
	}
}

// The ponger prints a pong and waits for a ping
func ponger(pinger chan<- int, ponger <-chan int) {
	for j := 0; j < 5; j++ {
		<-ponger
		fmt.Println("pong")
		time.Sleep(1 * time.Second)
		pinger <- 1
	}
}

func main() {
	ping := make(chan int)
	pong := make(chan int)

	go pinger(ping, pong)
	go ponger(ping, pong)

	// The main goroutine starts the ping/pong by sending into the ping channel
	ping <- 1

	for {
		// Block the main thread until an interrupt occurs
		time.Sleep(time.Second)
	}
}