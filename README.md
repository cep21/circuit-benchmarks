# circuit-benchmarks

This repository does benchmarking for [cep21/circuit](https://github.com/cep21/circuit).

## Benchmarking

Circuit is more efficient than go-hystrix in every configuration.  It has comparable efficiency
to other implementations, faster for most when running with high concurrency. Run benchmarks with `make bench`.

I benchmark the following alternative circuit implementations.  I try to be fair and if
there is a better way to benchmark one of these circuits, please let me know!

* [hystrix-go](https://github.com/afex/hystrix-go)
* [rubyist](https://github.com/rubyist/circuitbreaker)
* [sony/gobreaker](https://github.com/sony/gobreaker)
* [handy/breaker](https://github.com/streadway/handy/tree/master/breaker)
* [iand-circuit]("github.com/iand/circuit")

```
> make bench
cd benchmarking && go test -v -benchmem -run=^$ -bench=. . 2> /dev/null
goos: darwin
goarch: amd64
pkg: github.com/cep21/circuit/benchmarking
BenchmarkCiruits/cep21-circuit/Hystrix/passing/1-8       	 2000000	       896 ns/op	     192 B/op	       4 allocs/op
BenchmarkCiruits/cep21-circuit/Hystrix/passing/75-8      	 3000000	       500 ns/op	     192 B/op	       4 allocs/op
BenchmarkCiruits/cep21-circuit/Hystrix/failing/1-8       	10000000	       108 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Hystrix/failing/75-8      	20000000	        82.5 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/passing/1-8       	10000000	       165 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/passing/75-8      	20000000	        87.7 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/failing/1-8       	20000000	        64.4 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/Minimal/failing/75-8      	100000000	        19.6 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/passing/1-8         	 1000000	      1300 ns/op	     256 B/op	       5 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/passing/75-8        	 5000000	       374 ns/op	     256 B/op	       5 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/failing/1-8         	 1000000	      1348 ns/op	     256 B/op	       5 allocs/op
BenchmarkCiruits/cep21-circuit/UseGo/failing/75-8        	 5000000	       372 ns/op	     256 B/op	       5 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/1-8     	  200000	      8146 ns/op	    1001 B/op	      18 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/75-8    	  500000	      2498 ns/op	     990 B/op	      20 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/failing/1-8     	  200000	      6299 ns/op	    1020 B/op	      19 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/failing/75-8    	 1000000	      1582 ns/op	    1003 B/op	      20 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/passing/1-8        	 1000000	      1834 ns/op	     332 B/op	       5 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/passing/75-8       	 2000000	       849 ns/op	     309 B/op	       4 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/failing/1-8        	20000000	       114 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/failing/75-8       	 5000000	       302 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/passing/1-8           	10000000	       202 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/passing/75-8          	 2000000	       698 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/failing/1-8           	20000000	        90.6 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/gobreaker/Default/failing/75-8          	 5000000	       346 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/passing/1-8               	 2000000	      1075 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/passing/75-8              	 1000000	      1795 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/failing/1-8               	 1000000	      1272 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/failing/75-8              	 1000000	      1686 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/passing/1-8        	10000000	       119 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/passing/75-8       	 5000000	       349 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/failing/1-8        	100000000	        20.4 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/failing/75-8       	300000000	         5.46 ns/op	       0 B/op	       0 allocs/op
PASS
ok      github.com/cep21/circuit/benchmarking   59.518s
```

Limiting to just high concurrency passing circuits (the common case).

```
BenchmarkCiruits/cep21-circuit/Minimal/passing/75-8      	20000000	        87.7 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/GoHystrix/DefaultConfig/passing/75-8    	  500000	      2498 ns/op	     990 B/op	      20 allocs/op
BenchmarkCiruits/rubyist/Threshold-10/passing/75-8       	 2000000	       849 ns/op	     309 B/op	       4 allocs/op
BenchmarkCiruits/gobreaker/Default/passing/75-8          	 2000000	       698 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/handy/Default/passing/75-8              	 1000000	      1795 ns/op	       0 B/op	       0 allocs/op
BenchmarkCiruits/iand_circuit/Default/passing/75-8       	 5000000	       349 ns/op	       0 B/op	       0 allocs/op
```