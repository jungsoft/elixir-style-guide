<img src="https://jungsoft.io/static/media/jungsoft_logo.c44eaf52.png" width="300px"/>

# Elixir Style Guide

Welcome to Jungsoft's Elixir Style Guide. Sit down, have a cup of coffee and read this calmly. ☕

## Indroduction

The goal of this guide is to help our team to understand and
follow code style best practices, maintaining a pattern.

As this guide is an extension of the [Christopher Adams Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide), we **highly recommend** reading it before you continue.

# Table of Contents

* __[Formatting](#formatting)__
  * [Breaking Lines](#breaking-lines)
  * [Blank Lines](#blank-lines)
  * [Dangling Commas](#dangling-commas)
* __[Schemas](#schemas)__
  * [Ecto Schema](##ecto-schema)
  * [GraphQL Schema](##graphql-schema)
* __[Regular Expressions](#regular-expressions)__
  * [Aliases](#aliases)
  * ['With do' Indentation](#with-do-indentation)

# Formatting
## Breaking Lines

When an enumerable contains more than 3 arguments, it should be broken into multiple lines. See an example for Lists below.

```elixir
# ❌ Bad
list = ["value1", "value2", "value3", "value4"]


# ✅ Good
list = [
  "value1",
  "value2",
  "value3",
  "value4",
]

# ✅ Good
list = ["value1", "value2", "value3"]
```

```elixir
# ❌ Bad
map = %{a: 1, b: 2, c: 3, d: 4}


# ✅ Good
map = %{
  a: 1,
  b: 2,
  c: 3,
  d: 4,
}

# ✅ Good
map = %{a: 1, b: 2, c: 3}
```

**This is also valid for Keyword Lists.**

[Back to top ⬆️](#table-of-contents)

## Blank Lines

Blank lines are important in some cases, but in some others can make the code less readable.
The examples below will give more details about this.

#### Module

Modules should not contain a blank line between the `moduledoc` and the module name.

```elixir
# ❌ Bad
defmodule Jungsoft.NicePlaceToWork do

  @moduledoc false

  # DO SOMETHING
end


# ✅ Good
defmodule Jungsoft.NicePlaceToWork do
  @moduledoc false

  # DO SOMETHING
end
```

The module `end` should not contain a blank space either.

```elixir
# ❌ Bad
defmodule Jungsoft.BestPeople do
  @moduledoc false

  def foo do
    true
  end

end


# ✅ Good
defmodule Jungsoft.BestPeople do
  @moduledoc false

  def foo do
    true
  end
end
```

#### Function

Different functions should contain exactly one blank space between each other.

```elixir
# ❌ Bad
defmodule Jungsoft.GoodCoffee do
  @moduledoc false

  def foo, do: true


  def bar, do: true
  def func, do: true
end


# ✅ Good
defmodule Jungsoft.GoodCoffee do
  @moduledoc false

  def foo, do: true

  def bar, do: true

  def func, do: true
end
```

Functions should not contain a blank line between the function call and the parameters. In addition, they should not end with a blank line.

```elixir
# ❌ Bad
defmodule Jungsoft.BeautifulOfficeView do
  @moduledoc false

  def foo do

    1 + 1

  end
end


# ✅ Good
defmodule Jungsoft.BeautifulOfficeView do
  @moduledoc false

  def foo do
    1 + 1
  end
end
```

#### With

The `with do` parameters should not be separated by blank spaces. Except when `else` contains multiple options. In this case should use the same logic as `case` and `cond` normal style (see [here](https://github.com/christopheradams/elixir_style_guide#multiline-case-clauses)).

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

## Dangling Commas

Objects with the possibility to span in multiple lines should contain a comma dangle in the last parameter. See an alias example below.

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

**This is also valid for Maps, Lists and Keyword Lists.**

[Back to top ⬆️](#table-of-contents)

# Schemas

The schemas should respect a pattern for organizing the parameters.

Independent of the schema type, the parameters should be grouped by type:
```elixir
# ❌ Bad
schema "foo" do
  field :name, :string

  field :age, :integer

  has_one :one, Bar

  has_one :two, Module
  timestamps()
end


# ✅ Good
schema "foo" do
  field :name, :string
  field :age, :integer

  has_one :one, Bar
  has_one :two, Module

  timestamps()
end
```

The other patterns are different based on the type of schema (Ecto or GraphQL). These differences are listed below.

## Ecto Schema

The Ecto schema parameters need to be organized in a order of importance:

| Importance | Field |
|---|---|
| 1º | field |
| 2º | belongs_to |
| 3º | has_one |
| 4º | has_many |
| 5º | timestamps |

In this way, `field` should be inserted before `belongs_to`, and so on.

## GraphQL Schema

The GraphQL schema parameters need to be organized in a order of importance:

| Importance | Field |
|---|---|
| 1º | normal fields |
| 2º | custom fields (with the `resolve`) |
| 3º | associations |

In this way, `normal fields` should be inserted before `custom fields`, and so on.

Remember, the first schema rule should be respected here as well (see [here](#schemas)). Therefore, `normal fields` should be grouped and separated with a blank space. Same is valid with `custom fields` and `associations`.

[Back to top ⬆️](#table-of-contents)

# Regular Expressions
## Aliases

#### Ordering

The aliases should be ordered alphabetically.

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

#### SubModules

The aliases should contain only one 'sub-module'.

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

## 'With do' Indentation

#### Space

When `with do` contains multiple lines, it's necessary to add two blank spaces before the first parameter. This is only valid when editor tab size is **2**. If you followed the Jungsoft guidelines this should be your case. 😊

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

[Back to top ⬆️](#table-of-contents)
