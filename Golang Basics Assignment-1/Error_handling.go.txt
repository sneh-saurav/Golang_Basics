package main 
  
import ( 
    "errors"
    "fmt"
) 

func main() { 
    err := errors.New("Error Occurs") 
    if err != nil { 
        fmt.Print(err) 
    } 
} 