<img src="https://jungsoft.io/static/media/jungsoft_logo.c44eaf52.png" width="300px"/>

# Elixir Style Guide

Welcome to Jungsoft's Elixir Style Guide. Sit down, have a cup of coffee and read this calmly. ☕

## Indroduction

The goal of this guide is to help our team to understand and
follow code style best practices, maintaining a pattern.

As this guide is an extension of the [Christopher Adams Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide), we **highly recommend** reading it before you continue.

# Table of Contents

* [Alias Organization](#alias-organization)
* ['With do' Organization](#with-do-organization)
* [Maps](#maps)
* [Lists](#lists)

## Aliases

### Comma

Aliases with multiple lines should contains a comma in the last module.

Example:

```elixir
# ❌ Bad
alias Jungsoft.{
  Module1,
  Module2
}


# ✅ Good
alias Jungsoft.{
  Module1,
  Module2,
}
```

### Ordering

The aliases should be ordered alphabetically.

Example:

```elixir
# ❌ Bad
alias Jungsoft.{
  CModule,
  BModule,
  AModule,
}


# ✅ Good
alias Jungsoft.{
  AModule,
  BModule,
  CModule,
}
```

### SubModules

The aliases should contains only one 'sub-module'.

Example:

```elixir
# ❌ Bad
alias Jungsoft.{
  Module1.SubModule1,
  Module1.SubModule2,
  Module2.SubModule1.SubSubModule1,
  Module2.SubModule1.SubSubModule2,
}


# ✅ Good
alias Jungsoft.Module1.{
  SubModule1,
  SubModule2,
}
alias Jungsoft.Module2.SubModule1.{
  SubSubModule1,
  SubSubModule2,
}
```

[Back to top ⬆️](#table-of-contents)

## 'With do' Organization

### Space

When `with do` contains multiple lines, it's necessary to add two blank spaces before the first parameter. This is only valid when editor tab size is **2**. If you followed the Jungsoft guidelines this should be your case. 😊

Example:

```elixir
# ❌ Bad
with true <- Jungsoft.function_1(),
      false <- Jungsoft.function_2()
do
  ## DO SOMETHING
end

# ❌ Bad
with true <- Jungsoft.function_1(),
     false <- Jungsoft.function_2()
do
  ## DO SOMETHING
end

# ❌ Bad
with  true <- Jungsoft.function_1() do
  ## DO SOMETHING
end


# ✅ Good
with  true <- Jungsoft.function_1(),
      false <- Jungsoft.function_2()
do
  ## DO SOMETHING
end

# ✅ Good
with true <- Jungsoft.function_1() do
  ## DO SOMETHING
end
```

### Blank lines

The `with do` parameters should not be separated by blank spaces. Except when `case` contains multiple parameters. In this case should use the same logic as `case` and `cond` normal style (see [here](https://github.com/christopheradams/elixir_style_guide#multiline-case-clauses)).

Example:

```elixir
# ❌ Bad
with  %StarWars{} <- Jungsoft.function_1(),
      true <- Jungsoft.function_2()
do

  ## DO SOMETHING

else

  %StarTrek{} ->
    {:error, "Wrong choice"}

  false ->
    ## DO SOMETHING

end


# ✅ Good
with  %StarWars{} <- Jungsoft.function_1(),
      true <- Jungsoft.function_2()
do
  ## DO SOMETHING
else
  %StarTrek{} ->
    {:error, "Wrong choice"}

  false ->
    ## DO SOMETHING
end
```

[Back to top ⬆️](#table-of-contents)

## Maps

### Comma dangle

When map contains multiple lines, the last line should contain a comma.

Example:

```elixir
# ❌ Bad
map = %{
  first: "first",
  second: "second".
  third: "third"
}


# ✅ Good
map = %{
  first: "first",
  second: "second".
  third: "third",
}

```

[Back to top ⬆️](#table-of-contents)

## Lists

### Maximum parameters

When a list contains more than 3 values, it should be breaking into multiple lines.

Example:

```elixir
# ❌ Bad
list = ["value1", "value2", "value3", "value4"]


# ✅ Good
list = [
  "value1",
  "value2",
  "value3",
  "value4"
]

# ✅ Good
list = ["value1", "value2", "value3"]
```

[Back to top ⬆️](#table-of-contents)
