package main

import "fmt"

type Emp struct {
	eID   int
	eName string
	eData []string
}

func main() {
	a := Emp{
		eID:   14,
		eName: "SNEH SAURAV",
		eData: []string{
			"Bihar",
			"7978668403",
		},
	}
	fmt.Println(a)
	fmt.Print(a.eData)

}