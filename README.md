# NSubstitute FSharp Wrapper

Travis master: [![Build Status](https://travis-ci.org/Offline24/NSubstituteFSharpWrapper.svg?branch=master)](https://travis-ci.org/Offline24/NSubstituteFSharpWrapper) develop: [![Build Status](https://travis-ci.org/Offline24/NSubstituteFSharpWrapper.svg?branch=develop)](https://travis-ci.org/Offline24/NSubstituteFSharpWrapper)

## Description

Provides simple F# syntax for NSubstitute.

## Installation

Avaiable on nuget: [NSubstituteFSharpWrapper](https://www.nuget.org/packages/NSubstituteFSharpWrapper/)

## Usage examples

Check unit tests to see all possible uses: [MockTests.fs](NSubstituteFSharpWrapper.Tests/MockTests.fs)

### Mock create

```fsharp
open NSubstituteFSharpWrapper

let mock = mock<MyInterface> ()
```

```fsharp
let systemUnderTest = new system mock.Object
```

### Mocking field value

```fsharp
mock |> arrange (fun x -> x.IntField) |> returns 1
```

### Mocking function return value

```fsharp
mock |> arrange (fun x -> x.AddFunction arg.any arg.any) |> returns 1
```

```fsharp
mock |> arrange (fun x -> x.AddFunction (arg.is 1) (arg.is 2)) |> returns 3
mock |> arrange (fun x -> x.AddFunction arg.any arg.any) |> returns 5
```

```fsharp
mock |> arrange (fun x -> x.AddFunction arg.any (arg.match' (fun arg -> arg > 2))) |> returns 3
```

### Checking function calls

```fsharp
mock |> check (fun x -> x.AddFunction (arg.is 1) (arg.is 2)) |> wasCalledAtLeastOnce
```

```fsharp
mock |> check (fun x -> x.AddFunction arg.any arg.any) |> wasCalled 5 times
```
