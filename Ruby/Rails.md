# Ruby on Rails Notes and Commands

## Getting Started On MacOS

### Set up ruby environment

Initialize the environment:

```bash
rbenv init
```

Create a path export and append to `./zshrc` file:

```bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
```

Add `eval "$(rbenv init -)"` to `~/.zshrc` file, to ensure rbenv works properly.

```bash
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
```

This runs `rbenv init -` and executes its output as shell commands, setting up rbenv's shims system in shell; it is set up to run automatically every time the terminal is opened.

Exit the terminal session and then start a new one.

Reload zsh configuration file:

```bash
source ~/.zshrc
```

### Verify rbenv is working

Check which version of ruby is installed.

```bash
rbenv --version
```

Or

```bash
which rbenv
```

Print out the path to verify it contains `.rbenv/shims` early on in the path.

```
echo $PATH
```

### Install and set ruby version

List available versions:

```bash
rbenv install --list
```

Install ruby with specific version number [changes depending on which one you want to use]:

```bash
rbenv install 3.3.9
```

Set a specific version globally:

```bash
rbenv global 3.3.9
```

Verify the version set is the version being used, with one of the following:

```bash
ruby --version

ruby -v

which ruby
```

### Install Rails

```bash
gem install rails
```

Verify which gem version is available:

```bash
which gem
```

### Run a new rails project

```bash
rails new demo
```
