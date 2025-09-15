# Ruby Hash

The fast way to store and find things.

## Goal

Today you'll learn how to store and retrieve information using the [Ruby Hash](https://docs.ruby-lang.org/en/master/Hash.html) data structure, one of the most powerful tools in programming.

## Lists vs Dictionaries

Before we dive into hashes, let's recall arrays. Arrays are great for storing lists of things in order:

```ruby
fruit = ["apple", "banana", "cherry", "grape"]
banana = fruit[1]

pp banana
```
{: .repl }

Arrays use numbers (indexes) to find items. But what if you want to look up a fruit by name, or a country by its code? That's where Hashes come in.

<aside class="tip">
  Think of a hash like a <strong>dictionary</strong>. You look up a "word" (the key) and get its "definition" (the value).
</aside>

## Your First Hash

<!-- TODO: start with a simpler example? explain curly braces {} and Hash.new -->

We can use the initializer to create a new instance of a `Hash`.

```ruby
my_hash = Hash.new
```

<!-- TODO: explain how to pass in key to access value -->
<!-- TODO: use .store and .fetch first -->
<!-- TODO: use square bracket syntax -->

Now we need to insert some values. Let's build a hash that uses country codes for *keys* and country names for *values*.

We'll use the [Hash#store](https://docs.ruby-lang.org/en/master/Hash.html#method-i-store) method to add keys and values.

```ruby
countries = Hash.new
countries.store("USA", "United States")
countries.store("FR", "France")
countries.store("CN", "China")
countries.store("ES", "Spain")

pp countries
```
{: .repl }

Now we can use the [Hash#fetch](https://docs.ruby-lang.org/en/master/Hash.html#method-i-fetch) method to access values for a given key.

```ruby
countries = Hash.new
countries.store("USA", "United States")
countries.store("FR", "France")
countries.store("CN", "China")
countries.store("ES", "Spain")

pp countries.fetch("USA")
```
{: .repl }

Instead of remembering that "USA" is at position 0, we just use "USA" as the key. Much easier!

## Hash Syntax

We can also use the shorthand curly braces `{}` to create a hash. This is the most common way to create a hash in Ruby.

```ruby
my_hash = {}
```
{: .repl }

<!--

Ruby Symbol vs Hash Rocket
In Ruby, the choice between using a symbol with a hash rocket (=>) and the newer colon syntax (:) affects the key type and the flexibility of the hash.

When using the hash rocket syntax (=>), the key retains its original data type. This allows for keys that are strings, symbols, integers, or other objects. For example, { 'A' => 1 } creates a hash where the key 'A' is a string, and { 1 => 'one' } uses an integer key.
 This syntax is necessary when the key is not a valid symbol identifier, such as one containing special characters like :$$set => value, or when using non-symbol keys like strings or integers.

The newer colon syntax (:) is a shorthand that only works for symbol keys.

-->

<!-- TODO: what is a symbol? -->

Ruby lets you write hashes in two ways:

## Hash Rocket Style

```ruby
fruit_colors = { "apple" => "red", "banana" => "yellow" }

color = fruit_colors.fetch("apple")

pp color
```
{: .repl }

## Symbol Style (most common)

<!-- TODO: explain what a symbol is -->

```ruby
fruit_colors = { apple: "red", banana: "yellow" }

color = fruit_colors.fetch(:apple)

pp color
```
{: .repl }

<aside class="tip">
  Hash keys can be strings, numbers, or symbols (like <code>:apple</code>). Symbols are faster and common in Ruby.
</aside>

## Adding & Updating Hash Data

You can insert or update data easily:

```ruby
stock = { apple: 10, banana: 5 }

# Add new item
stock[:cherry] = 7

# Update existing item
stock[:banana] = 8

pp stock
```
{: .repl }

## Checking Keys & Values

Hashes come with helpful methods:

```ruby
stock = { apple: 10, banana: 8, cherry: 7 }

# true
pp stock.key?(:banana)

# false
pp stock.key?(:grape)

# [:apple, :banana, :cherry]
pp stock.keys

# [10, 8, 7]
pp stock.values
```
{: .repl }

## Safer Retrieval

Using `[]` will return nil if the key isn't found:

```ruby
stock = { apple: 10 }

# nil
pp stock[:banana]  
```
{: .repl }

But `.fetch` gives you control:

```ruby
stock = { apple: 10 }
pp stock.fetch(:banana, "Out of stock")
```
{: .repl }

<aside>
  Note that calling <code>fetch</code> without a default value will raise a <code>KeyError</code>.
</aside>

## Iterating Over Hashes

So far, you've learned how to grab values from a hash by key. But what if you want to process every key-value pair in your hash? That's where `.each` comes in.

```ruby
stock = { apple: 10, banana: 8, cherry: 7 }

stock.each do |fruit, quantity|
  pp "We have #{quantity} #{fruit}s in stock."
end
```
{: .repl }

<aside class="tip">
  The first variable (fruit) holds the <strong>key</strong>, and the second variable (quantity) holds the <strong>value</strong>.
</aside>

### Why This Works

The `.each` method goes through every item in the hash and gives you both the key and the value. It's like flipping through a dictionary one entry at a time.

### Iterating Only Keys or Values

Sometimes you only care about keys or values. You can use the `.keys` or `.values` methods to get an array and then loop through using `.each`.

```ruby
stock = { apple: 10, banana: 8, cherry: 7 }

stock.keys.each do |fruit|
  pp fruit
end

stock.values.each do |quantity|
  pp quantity
end
```
{: .repl }

## Wrap-Up

- Arrays = ordered lists (great for sequences).
- Hashes = dictionaries of key-value pairs (great for lookups).
- Keys can be strings, numbers, or symbols.
- Use `[]` or `.fetch` to retrieve values.
- Hashes make data retrieval fast and meaningful.
- Loop through a hash using `.each`, `.keys`, and/or `.values`.

## Quiz

- Why would you use a hash instead of an array?
- To store items in a meaningful way using keys.
  - Correct! Hashes let you look things up by name instead of number.
- Because arrays don't work in Ruby.
  - Not correct. Arrays are useful, but for different problems.
- To make the program run slower.
  - Nope! Hashes are actually faster for lookups.
{: .choose_best #hash_vs_array title="When to Use a Hash" answer="1"}

## Project: Hash

In this project, you will write Ruby programs that leverage these hash methods. This project includes automated tests, so click this link to get started <https://github.com/dpi-tta-projects/ruby-hash/fork>, fork the repository and create a codespace.

<aside class="warning">
  In order to get credit for completing this project you'll need to open the assignment link from canvas to generate an access token.
</aside>

## References

- Ruby Docs: [Hash](https://docs.ruby-lang.org/en/master/Hash.html)
- [How the Hash Works in Ruby](https://geekhmer.github.io/blog/2015/06/16/how-the-hash-works-in-ruby/)
- [Ruby Hash Methods](https://www.rubyguides.com/2020/05/ruby-hash-methods/)
