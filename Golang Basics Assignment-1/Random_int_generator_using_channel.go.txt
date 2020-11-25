package main

import (
	"fmt"
	"math/rand"
	"time"
)

func Ran(ch chan int) {
	for i := 0; i < 20; i++ {
		ch <- rand.Intn(1000)
	}
}
func main() {
	var ch = make(chan int)
	go Ran(ch)

	for j := 0; j < 20; j++ {
		a := <-ch
		fmt.Println(a)
		time.Sleep(1 * time.Second)
	}
}