- 0.18.1
  - Fixes:
    - Compatibility with Ruby 3.2:
      - Use `Random` instead of no-longer-available `Random::DEFAULT` on Ruby 3.x.
      - Ensure when a hash is passed (such as in `PropCheck.forall(hash_of(integer, string)) { |hash| ... }` that when an empty hash is generated, `hash` is still `{}` and not `nil`. ([Ruby 3.x treats `fun(**{})` differently than Ruby 2.x](https://www.ruby-lang.org/en/news/2019/12/12/separation-of-positional-and-keyword-arguments-in-ruby-3-0/#other-minor-changes-empty-hash))
- 0.18.0
  - Features:
    - Allows calling `PropCheck::Property#check` without a block, which will just return `self`. This is useful for writing wrapper functions that use `before/after/around/with_config` etc hooks which might themselves optionally want a block so they can be chained. (See the `forall_with_db` snippet in the README for an example)
- 0.17.0
  - Features:
    - Recursive generation using `PropCheck::Generators.tree`.
- 0.16.0
  - Features:
    - New option in `PropCheck::Property::Configuration` to resize all generators at once.
    - Wrapper functions to modify this easily in `PropCheck::Property` called `#resize`, `#grow_fast`, `#grow_slowly`, `#grow_exponentially`, `#grow_quadratically`, `#grow_logarithmically`.
- 0.15.0
  - Features:
    - Generators for `Date`, `Time` and `DateTime`.
      - Basic work done by @Haniyya. Thank you very much!
      - Extra functions to generate dates/times/datetimes in the future or the past.
      - Allow overriding the epoch that is used.
      - A new option in `PropCheck::Property::Configuration` to set the default epoch.
    - Generator to generate `Set`s.
    - New builtin float generators (positive, negative, nonzero, nonnegative, nonpositive). Both in 'normal' flavor and in 'real' flavor (that will never generate infinity or other special values).
    - `PropCheck::Generator#with_config` which enables the possibility to inspect and act on the current `PropCheck::Property::Configuration` while generating values.
  - Fixes:
    - Preserve backwards compatibility with Ruby 2.5 by not using infinite ranges internally (c.f. #8, thank you, @hlaf!)
    - Make a flaky test deterministic by fixing the RNG. (c.f. #9, thank you, @hlaf!)
    - Fix a crash when using a hash where not all keys are symbols. (c.f. #7, thank you, @Haniyya!)
    - Fix situations in which `PropCheck::Generators.array` would for certain config values never generate empty arrays.
- 0.14.1 - Swap `awesome_print` for `amazing_print` which is a fork of the former that is actively maintained.
- 0.14.0 - Adds `uniq: true` option to `Generators.array`. Makes `PropCheck::Property` an immutable object that returns copies that have changes whenever reconfiguring, allowing re-usable configuration.
- 0.13.0 - Adds Generator#resize
- 0.12.1 - Fixes shrinking when filtering bug.
- 0.12.0 - `PropCheck::Generators#instance`
- 0.11.0 - Improved syntax to support Ruby 2.7 and up without deprecation warnings, full support for `#where`.
- 0.10.0 - Some bugfixes, support for `#where`
- 0.8.0 - New syntax that is more explicit, passng generated values to blocks as parameters.
