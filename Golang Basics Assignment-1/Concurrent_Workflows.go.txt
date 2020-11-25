package main

import (
	"fmt"
)

func myfun(ch chan int) {

	fmt.Println("The Sum is : ", 234+<-ch)
}
func main() {
	fmt.Println("Starting main")
	var ch = make(chan int)

	go myfun(ch)
	ch <- 23

	fmt.Print("Ending main")

}