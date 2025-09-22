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

## Hash vs Array

Use an Array when *order* matters. Use a Hash when *names/labels* matter. As your data grows, finding by a key in a Hash is still quick. Counting through all the spots in an Array can become slow.

Picture yourself in a mail room with thousands of mailboxes. Each mailbox is numbered starting at 0. Going through each mailbox 1 by 1 until you find what you are looking for would take a long time. Think of a hash as an index mapping name to mailbox number. This makes finding a mailbox much faster!

In computer science we model this using Big O notation. Arrays are O(n) meaning in the worst case scenario you may have to loop through the entire length (n) of the array to find what you are looking for. Hashes are O(1) meaning in the worst case scenario we can still find what we are looking for at first glance.

## Your First Hash

Think of a hash like a dictionary. You look up a "word" (the key) and get its "definition" (the value). The keys/values can be of any data type, but usually we use strings, numbers, or [symbols](#symbol-style) for the keys.

<aside class="tip">
  Some programming languages call the hash data structure a "dictionary".
</aside>

We can use the initializer to create a new instance of a `Hash`.

```ruby
my_hash = Hash.new

pp my_hash
```
{: .repl }

We can also use the shorthand curly braces `{}` to create a hash. This is the most common way to create a hash in Ruby.

```ruby
my_hash = {}

pp my_hash
```
{: .repl }

Now we need to insert some keys and values. We'll use the [Hash#store](https://docs.ruby-lang.org/en/master/Hash.html#method-i-store) method to add keys and values.

```ruby
my_hash = Hash.new

my_hash.store("KEY", "VALUE")

pp my_hash
```
{: .repl }

Just setting a hash with key `"KEY"` and and value `"VALUE"` isn't super useful. Let's build a hash that uses country codes for *keys* and country names for *values*.. We'll use the [Hash#fetch](https://docs.ruby-lang.org/en/master/Hash.html#method-i-fetch) method to access values for a given key.

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

<aside class="tip">
  Try passing in different keys to the <code>countries</code> hash.
</aside>

## Hash Rocket Style

The `=>` operator is used to pair keys with values in a Ruby Hash. We call `=>` a *hash rocket* (or *fat arrow*).

```ruby
fruit_colors = { "apple" => "red", "banana" => "yellow" }

color = fruit_colors.fetch("apple")

pp color
```
{: .repl }

## Adding & Updating Hash Data

You can insert or update data easily using `store`.

```ruby
stock = { "apple" => 10, "banana" => 5 }

# Add new item
stock.store("cherry", 7)

# Update existing item
stock.store("banana", 8)

pp stock
```
{: .repl }

## Checking Keys & Values

Hashes come with helpful methods:

```ruby
stock = { "apple" => 10, "banana" => 8, "cherry" => 7 }

# true
pp stock.key?("banana")

# false
pp stock.key?("grape")

# ["apple", "banana", "cherry"]
pp stock.keys

# [10, 8, 7]
pp stock.values
```
{: .repl }

## Safer Retrieval

Calling `fetch` will raise a `KeyError` if the key doesn't exist on the hash.

```ruby
stock = { "apple" => 10 }
pp stock.fetch("banana")
```
{: .repl }

`Hash#fetch` accepts a second argument `default_value` that is returned when the key doesn't exist. This can help us avoid raising a `KeyError`.

```ruby
stock = { "apple" => 10 }
pp stock.fetch("banana", "Out of stock")
```
{: .repl }

## Iterating Over Hashes

So far, you've learned how to grab values from a hash by key. But what if you want to process every key-value pair in your hash? That's where `.each` comes in.

```ruby
stock = { "apple" => 10, "banana" => 8, "cherry" => 7 }

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
stock = { "apple" => 10, "banana" => 8, "cherry" => 7 }

stock.keys.each do |fruit|
  pp fruit
end

stock.values.each do |quantity|
  pp quantity
end
```
{: .repl }

## Syntax Sugar

### Symbol Style

Ruby lets you write hashes in two ways, "hash rocket" style and "symbol" style.

A symbol is a short, simple label that starts with `:` like `:apple`. We use symbols for keys because they're tidy and don't change.

```ruby
# this is a symbol
:apple
```

```ruby
# we can use symbols for keys in hash
fruit = { :apple => "red" }

pp fruit
```
{: .repl }

Symbols are great for fixed labels (field names, options). Use strings for text people type.

Using symbols for keys is so common in ruby there is a shorthand syntax for creating hashes with symbol keys.

```ruby
# we can use symbol shorthand syntax to create hash with symbol keys
fruit = { apple: "red" }

pp fruit
```
{: .repl }

<aside class="tip">
  Hash keys can be strings, numbers, or symbols (like <code>:apple</code>). Using symbols for keys is faster and more common in Ruby.
</aside>

### Square Bracket Style

You can also use  square brackets `[]` to store and fetch values. The difference between `[]` and `fetch` is that square brackets return `nil` instead of throwing a `KeyError` when the key doesn't exist.
```ruby
stock = {}

stock["apple"] = 10
pp stock["apple"]
pp stock["grape"]
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
