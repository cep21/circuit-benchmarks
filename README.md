# circuit-benchmarks

This repository does benchmarking for [cep21/circuit](https://github.com/cep21/circuit).

## Benchmarking

Circuit is more efficient than go-hystrix in every configuration.  It has comparable efficiency
to other implementations, faster for most when running with high concurrency. Run benchmarks with `go test -v -benchmem -run=^$ -bench=. . 2> /dev/null`.

I benchmark the following alternative circuit implementations.  I try to be fair and if
there is a better way to benchmark one of these circuits, please let me know!

* [hystrix-go](https://github.com/afex/hystrix-go)
* [rubyist](https://github.com/rubyist/circuitbreaker)
* [sony/gobreaker](https://github.com/sony/gobreaker)
* [handy/breaker](https://github.com/streadway/handy/tree/master/breaker)
* [iand-circuit]("github.com/iand/circuit")

```bash
> go test -v -benchmem -run=^$ -bench=. . 2> /dev/null
```

```console
goos: darwin
goarch: amd64
pkg: github.com/cep21/circuit-benchmarks
cpu: Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz
BenchmarkCiruits
BenchmarkCiruits/cep21-circuit
BenchmarkCiruits/cep21-circuit/Hystrix
BenchmarkCiruits/cep21-circuit/Hystrix/passing
BenchmarkCiruits/cep21-circuit/Hystrix/passing/1
BenchmarkCiruits/cep21-circuit/Hystrix/passing/1-12       	 1469689	       849.6 ns/op	     240 B/op	       4 allocs/op
BenchmarkCiruits/cep21-circuit/Hystrix/passing/75
BenchmarkCiruits/cep21-circuit/Hystrix/passing/75-12      	 4492564	       258.4 ns/op	     240 B/op	       4 allocs/op
BenchmarkCiruits/cep21-circuit/Hystrix/failing
BenchmarkCiruits/cep21-circuit/Hystrix/failing/1
BenchmarkCiruits/cep21-circuit/Hystrix/failing/1-12       	 4487305	       272.3 ns/op	      16 B/op	       1 allocs/op
BenchmarkCiruits/cep21-circuit/Hystrix/failing/75
BenchmarkCiruits/cep21-circuit/Hystrix/failing/75-12      	17190705	        78.92 ns/op	      16 B/op	       1 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal
BenchmarkCiruits/cep21-circuit/Minimal/passing
BenchmarkCiruits/cep21-circuit/Minimal/passing/1
BenchmarkCiruits/cep21-circuit/Minimal/passing/1-12       	 4412586	       273.3 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/passing/75
BenchmarkCiruits/cep21-circuit/Minimal/passing/75-12      	16031582	        73.30 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/failing
BenchmarkCiruits/cep21-circuit/Minimal/failing/1
BenchmarkCiruits/cep21-circuit/Minimal/failing/1-12       	 4413255	       235.4 ns/op	      16 B/op	       1 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/failing/75
BenchmarkCiruits/cep21-circuit/Minimal/failing/75-12      	28415378	        51.44 ns/op	      16 B/op	       1 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo
BenchmarkCiruits/cep21-circuit/UseGo/passing
BenchmarkCiruits/cep21-circuit/UseGo/passing/1
BenchmarkCiruits/cep21-circuit/UseGo/passing/1-12         	  859346	      1338 ns/op	     272 B/op	       5 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/passing/75
BenchmarkCiruits/cep21-circuit/UseGo/passing/75-12        	 4132455	       277.2 ns/op	     272 B/op	       5 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/failing
BenchmarkCiruits/cep21-circuit/UseGo/failing/1
BenchmarkCiruits/cep21-circuit/UseGo/failing/1-12         	  722814	      1685 ns/op	     304 B/op	       7 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/failing/75
BenchmarkCiruits/cep21-circuit/UseGo/failing/75-12        	 3615490	       333.8 ns/op	     304 B/op	       7 allocs/op
BenchmarkCiruits/GoHystrix
BenchmarkCiruits/GoHystrix/DefaultConfig
BenchmarkCiruits/GoHystrix/DefaultConfig/passing
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/1
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/1-12     	  230498	      4716 ns/op	    1249 B/op	      22 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/75
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/75-12    	  477273	      2650 ns/op	    1290 B/op	      24 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/failing
BenchmarkCiruits/GoHystrix/DefaultConfig/failing/1
BenchmarkCiruits/GoHystrix/DefaultConfig/failing/1-12     	  318826	      3800 ns/op	    1270 B/op	      23 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/failing/75
BenchmarkCiruits/GoHystrix/DefaultConfig/failing/75-12    	 1000000	      1095 ns/op	    1245 B/op	      24 allocs/op
BenchmarkCiruits/rubyist
BenchmarkCiruits/rubyist/Threshold-10
BenchmarkCiruits/rubyist/Threshold-10/passing
BenchmarkCiruits/rubyist/Threshold-10/passing/1
BenchmarkCiruits/rubyist/Threshold-10/passing/1-12        	  731997	      1497 ns/op	     372 B/op	       6 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/passing/75
BenchmarkCiruits/rubyist/Threshold-10/passing/75-12       	 2178349	       649.3 ns/op	     346 B/op	       5 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/failing
BenchmarkCiruits/rubyist/Threshold-10/failing/1
BenchmarkCiruits/rubyist/Threshold-10/failing/1-12        	10023756	       111.5 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/failing/75
BenchmarkCiruits/rubyist/Threshold-10/failing/75-12       	 1000000	      1146 ns/op	     335 B/op	       5 allocs/op
BenchmarkCiruits/gobreaker
BenchmarkCiruits/gobreaker/Default
BenchmarkCiruits/gobreaker/Default/passing
BenchmarkCiruits/gobreaker/Default/passing/1
BenchmarkCiruits/gobreaker/Default/passing/1-12           	 5648436	       192.4 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/passing/75
BenchmarkCiruits/gobreaker/Default/passing/75-12          	 2886820	       426.9 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/failing
BenchmarkCiruits/gobreaker/Default/failing/1
BenchmarkCiruits/gobreaker/Default/failing/1-12           	11147300	       110.4 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/failing/75
BenchmarkCiruits/gobreaker/Default/failing/75-12          	 5916306	       172.0 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy
BenchmarkCiruits/handy/Default
BenchmarkCiruits/handy/Default/passing
BenchmarkCiruits/handy/Default/passing/1
BenchmarkCiruits/handy/Default/passing/1-12               	  960382	      1081 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/passing/75
BenchmarkCiruits/handy/Default/passing/75-12              	  959074	      1118 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/failing
BenchmarkCiruits/handy/Default/failing/1
BenchmarkCiruits/handy/Default/failing/1-12               	 1000000	      1037 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/failing/75
BenchmarkCiruits/handy/Default/failing/75-12              	 1164082	      1023 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit
BenchmarkCiruits/iand_circuit/Default
BenchmarkCiruits/iand_circuit/Default/passing
BenchmarkCiruits/iand_circuit/Default/passing/1
BenchmarkCiruits/iand_circuit/Default/passing/1-12        	15529444	        75.03 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/passing/75
BenchmarkCiruits/iand_circuit/Default/passing/75-12       	 8886270	       134.2 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/failing
BenchmarkCiruits/iand_circuit/Default/failing/1
BenchmarkCiruits/iand_circuit/Default/failing/1-12        	65668842	        16.09 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/failing/75
BenchmarkCiruits/iand_circuit/Default/failing/75-12       	474891303	         2.462 ns/op	       0 B/op	       0 allocs/op
PASS
ok  	github.com/cep21/circuit-benchmarks	50.511s
```

Limiting to just high concurrency passing circuits (the common case).

```
BenchmarkCiruits/cep21-circuit/Minimal/passing/75-12      	16031582	        73.30 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/75-12    	  477273	      2650 ns/op	    1290 B/op	      24 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/passing/75-12       	 2178349	       649.3 ns/op	     346 B/op	       5 allocs/op
BenchmarkCiruits/gobreaker/Default/passing/75-12          	 2886820	       426.9 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/passing/75-12              	  959074	      1118 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/passing/75-12       	 8886270	       134.2 ns/op	       0 B/op	       0 allocs/op
```