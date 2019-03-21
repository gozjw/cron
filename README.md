## Cron
a cron library for go

## Usage

Callers may register Funcs to be invoked on a given schedule.  Cron will run
them in their own goroutines. A name must be provided.

```go
c := cron.New()
//c := cron.NewWithLocation(time.FixedZone("CST", 8*3600))

c.AddFunc("*/2 * * * *",  func(name string) { fmt.Println("Every 2 seconds",name) }, "Often")
c.AddFunc("@hourly",      func(name string) { fmt.Println("Every hour",name) }, "Frequent")
c.AddFunc("@every 1h30m", func(name string) { fmt.Println("Every hour thirty",name) }, "Less Frequent")
c.Start()

// Add a func to a running Cron
c.AddFunc("@daily", func(name string) { fmt.Println("Every day") }, "My Job")
// Remove an entry from the cron by name.
c.RemoveJob("My Job")

time.Sleep(30*time.Second)
c.Stop()  // Stop the scheduler (does not stop any jobs already running).
```