package main

import (
	"encoding/json"
	"log"
	"os"
)

func main() {
	dec := json.NewDecoder(os.Stdin)
	enc := json.NewEncoder(os.Stdout)
	for {
		var s map[string]interface{}
		if err := dec.Decode(&s); err != nil {
			log.Println(err)
			return
		}
		for i := range s {
			if i != "Name" {
				delete(s, i)
			}
		}
		if err := enc.Encode(&s); err != nil {
			log.Println(err)
		}
	}
}
