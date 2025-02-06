# Go Race Condition Example

This repository demonstrates a common race condition in Go using channels and goroutines.  The program sends values to a channel and attempts to receive them concurrently, without proper synchronization, resulting in potential issues.

## The Problem

The `bug.go` file contains a Go program that creates two goroutines. One goroutine sends values (0-9) to a channel, then closes the channel. The other goroutine receives these values from the channel.

However, there is no synchronization mechanism to ensure that the channel is closed only after all the values are received.

This can lead to a race condition where the channel is closed prematurely, causing the receiving goroutine to exit before it has consumed all the values from the channel, potentially resulting in lost values and/or a program panic.

## The Solution

The `bugSolution.go` file shows a corrected version of the program. A `sync.WaitGroup` is used to synchronize the goroutines, ensuring that all values are received before the channel is closed and the program terminates.

## How to Run

1. Clone this repository.
2. Navigate to the repository's directory.
3. Run `go run bug.go` to see the potential issue and `go run bugSolution.go` to see the solution.  

This example highlights the importance of proper synchronization when working with concurrent operations in Go. 