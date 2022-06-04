package main

import (
	"fmt"
	"net/http"
	"os"
	"time"
)

func main() {
	fmt.Println("Hello,World")
	http.HandleFunc("/healthz", getData)
	err := http.ListenAndServe("0.0.0.0:80", nil)
	if err != nil {
		fmt.Println("ListenAndServe error:", err.Error())
	}
}

func getData(res http.ResponseWriter, req *http.Request) {
	time.Sleep(time.Second)
	req.Header.Set("Authorization", "bearer simaop")
	for key := range req.Header {
		_value := req.Header.Get(key)
		res.Header().Set(key, _value)
	}
	go_version := os.Getenv("VERSION")
	res.Header().Set("version", go_version)

	fmt.Println("ip:", req.Header.Get("X-Real-IP"))
	fmt.Println("forward:", req.Header.Get("X-Forward-For"))

	res.WriteHeader(200)
	fmt.Println(res.Header())
}
