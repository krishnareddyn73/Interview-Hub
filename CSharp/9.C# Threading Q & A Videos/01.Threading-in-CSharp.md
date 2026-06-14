# Threading in C# - Complete Interview Notes

## What is Threading?

Threading means executing multiple pieces of code concurrently (in parallel) instead of executing them one after another.

Without threading:

```csharp
Function1();
Function2();
```

Execution Flow:

```text
Function1 --> Completes
             |
             V
Function2 --> Completes
```

This is called **Synchronous** or **Sequential Execution**.

---

## Synchronous Process Example

```CSharp
static vid Main(string[] args)
{
    Function1();
    Function2();
}

static void Function1()
{
    for(int i=0;i<10;i++)
    {
        Console.WriteLine("Function1 Executed");
    }
}

static void Function2()
{
    for(int i=0;i<10;i++)
    {
        Console.WriteLine("Function2 Executed");
    }
}
```


## Why Use Threading?

Suppose:

- Function1 takes 10 seconds
- Function2 takes 10 seconds

Without threading:

```text
Total Time = 20 Seconds
```

With threading:

```text
Function1 ----|
              |---- Run Together
Function2 ----|
```

Total Time ≈ 10 Seconds (depends on CPU scheduling).

---

# Types of Threads in C#

1. Foreground Thread
2. Background Thread

## Foreground Thread

By default every thread created using:

```csharp
Thread t = new Thread(Function1);
```

is a Foreground Thread.

### Characteristics

- Keeps application alive
- Continues execution even after Main() ends
- Application closes only after all foreground threads complete

## Background Thread

Create using:

```csharp
Thread t = new Thread(Function1);
t.IsBackground = true;
```

### Characteristics

- Depends on Main thread
- Terminates automatically when Main thread exits
- Suitable for logging, monitoring, cache cleanup

## Foreground vs Background Thread

| Feature | Foreground Thread | Background Thread |
|----------|------------------|------------------|
| Default Thread Type | Yes | No |
| Keeps Application Alive | Yes | No |
| Continues After Main Ends | Yes | No |
| Killed When Main Ends | No | Yes |

## Modern C# Approach

Prefer:

- Task
- Task<T>
- async/await
- ThreadPool

Example:

```csharp
Task.Run(() =>
{
    Console.WriteLine("Running in background");
});
```

## Interview Summary

- Thread = Smallest unit of execution.
- Threading = Parallel execution of code.
- Default thread type = Foreground Thread.
- Foreground Thread keeps application alive.
- Background Thread dies when Main Thread exits.
- Modern .NET prefers Task and async/await.
