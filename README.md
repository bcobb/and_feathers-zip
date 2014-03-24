# AndFeathers::Zip

Works with [and-feathers](http://github.com/bcobb/and_feathers) to turn in-memory archives into zip files.

## Installation

Add this line to your application's Gemfile:

    gem 'and_feathers-zip'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install and_feathers-zip

## Usage

### Writing a ZIP to disk

```ruby
require 'and_feathers'
require 'and_feathers/zip'

# This is a simple archive
archive = AndFeathers.build('archive') do |root|
  root.file('README')
end

File.open('archive.zip', 'w+') do |f|
  f << archive.to_io(AndFeathers::Zip).read
end
```

### Zip an existing directory, plus a few changes/additions

```ruby
require 'and_feathers'
require 'and_feathers/zip'

archive = AndFeathers.from_path('spec') do |spec|
  spec.file('end_to_end_spec.rb') { '# whoops' }
  spec.file('spec_helper.rb') { '# everyone needs one of these' }
end

File.open('spec.zip', 'w+') do |f|
  f << archive.to_io(AndFeathers::Zip).read
end
```
