# birb

[![Gem Version](https://badge.fury.io/rb/irb.svg)](https://badge.fury.io/rb/irb)
[![Static Badge](https://img.shields.io/badge/docs-repo-blue)](https://github.com/OhMyRuby/birb/tree/master/doc)
[![build](https://github.com/OhMyRuby/birb/actions/workflows/test.yml/badge.svg)](https://github.com/OhMyRuby/birb/actions/workflows/test.yml)

`birb` is OhMyRuby's fork of IRB: same interactive Ruby foundation, but with room for faster experiments, fork-specific polish, and a home that can move at its own pace.

IRB stands for "interactive Ruby", and `birb` is still that tool under the hood: a REPL for interactively executing Ruby expressions read from standard input.

For now, the shipped gem and executable are still named `irb`, so the familiar `irb` command starts the interpreter.

## Installation

> [!Note]
>
> Upstream IRB is a default gem of Ruby so you shouldn't need to install it separately.
>
> `birb` currently tracks that packaging shape, so if you want to run this fork directly you still install and execute it through the `irb` gem/executable names for now.

To install it with `bundler`, add this line to your application's Gemfile:

```ruby
gem 'irb'
```

And then execute:

```shell
$ bundle
```

Or install it directly with:

```shell
$ gem install irb
```

## Usage

> [!Note]
>
> Upstream has been steadily closing the gap with Pry's feature set, and this fork intends to keep building on that base. The comparison notes still live in [the upstream document](https://ruby.github.io/irb/COMPARED_WITH_PRY_md.html).

### The `irb` Executable

You can start a fresh `birb` session by typing `irb` in your terminal.

In the session, you can evaluate Ruby expressions or even prototype a small Ruby script. An input is executed when it is syntactically complete.

```shell
$ irb
irb(main):001> 1 + 2
=> 3
irb(main):002* class Foo
irb(main):003*   def foo
irb(main):004*     puts 1
irb(main):005*   end
irb(main):006> end
=> :foo
irb(main):007> Foo.new.foo
1
=> nil
```

### The `binding.irb` Breakpoint

If you use Ruby 2.5 or later versions, you can also use `binding.irb` in your program as breakpoints.

Once a `binding.irb` is evaluated, a new IRB session will be started with the surrounding context:

```shell
$ ruby test.rb

From: test.rb @ line 2 :

    1: def greet(word)
 => 2:   binding.irb
    3:   puts "Hello #{word}"
    4: end
    5:
    6: greet("World")

irb(main):001:0> word
=> "World"
irb(main):002:0> exit
Hello World
```

### Debugging

You can use `birb`'s IRB core as a debugging console with `debug.gem` with these options:

- In `binding.irb`, use the `debug` command to start an `irb:rdbg` session with access to all `debug.gem` commands.
- Use the `RUBY_DEBUG_IRB_CONSOLE=1` environment variable to make `debug.gem` use IRB as the debugging console.

To learn more about the current debugging flow, see the upstream [Debugging with IRB](https://ruby.github.io/irb/#label-Debugging+with+IRB) guide.

## Documentation

Until fork-specific docs diverge, the upstream IRB docs at https://ruby.github.io/irb/ remain the best reference for behavior and configuration, and this repo's [doc/](./doc/) directory is the local source of truth for future `birb`-specific updates.

## Configuration

See the upstream [Configuration page](https://ruby.github.io/irb/Configurations_md.html) in the documentation.

## Extending IRB

IRB `v1.13.0` and later versions allow users/libraries to extend its functionality through official APIs, and `birb` inherits that extension surface.

For more information, please visit the upstream [IRB Extension Guide](https://ruby.github.io/irb/EXTEND_IRB_md.html).

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for more information about working on the fork.

## Releasing

```
rake release
gh release create vX.Y.Z --generate-notes
```

## License

The gem is available as open source under the terms of the [2-Clause BSD License](https://opensource.org/licenses/BSD-2-Clause).
