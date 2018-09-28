# MultiStringReplace

A fast multiple string replace library for ruby. Uses a C implementation of the Aho–Corasick Algorithm based
on https://github.com/morenice/ahocorasick while adding support for on the fly multiple string replacement.

If Regex is not needed, this library offers significant performance advantages over String.gsub() for large string and with a large number of tokens.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'multi_string_replace'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install multi_string_replace

## Usage

```ruby
MultiStringReplace.match("The quick brown fox jumps over the lazy dog brown", ['brown', 'fox'])
# { 0 => [10, 44], 1 => [16] }
MultiStringReplace.replace("The quick brown fox jumps over the lazy dog brown", {'brown' => 'black', 'fox' => 'wolf'})
# The quick black wolf jumps over the lazy dog black
```

You can also pass in a Proc, these will only get evaluated when the token is encountered.

```ruby
MultiStringReplace.replace("The quick brown fox jumps over the lazy dog brown", {'brown' => 'black', 'fox' => ->() { "cat" }})
```

Also adds a mreplace method to String which does the same thing:

```ruby
"The quick brown fox jumps over the lazy dog brown".mreplace({'brown' => 'black', 'fox' => ->() { "cat" }})
```

## Performance

Performing token replacement on a 200K text file repeated 100 times

```
                         user     system      total        real
multi gsub           1.740000   0.020000   1.760000 (  1.790068)
MultiStringReplace   0.260000   0.010000   0.270000 (  0.277135)
mreplace             0.260000   0.020000   0.280000 (  0.281935)
```

Benchmark sources can be found here: <https://github.com/jedld/multi_word_replace/blob/master/bin/benchmark.rb>

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/multi_string_replace. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the MultiStringReplace project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/multi_string_replace/blob/master/CODE_OF_CONDUCT.md).
