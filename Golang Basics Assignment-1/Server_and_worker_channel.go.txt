

package main

import (
	"fmt"
	"time"
)

func worker(id int, job <-chan int, result chan<- int) {
	for i := range job {
		fmt.Println("worker", id, "started  job", i)
		time.Sleep(1 * time.Second)
		fmt.Println("worker", id, "finished job", i)
		result <- i * 2
	}
}

func main() {

	job := make(chan int, 50)
	result := make(chan int, 50)

	for i := 1; i <= 3; i++ {
		go worker(i, job, result)
	}

	for j := 1; j <= 5; j++ {
		job <- j
	}
	close(job)

	// collect all the results of the work.
	for k := 1; k <= 5; k++ {
		<-result
	}
}

