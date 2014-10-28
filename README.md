# Simple Lnmpa Server Management: mtenv

mtenv lets you easily switch between multiple versions of softwares [Linux + Nginx + MySQL/MariaDB + PHP + Apache]. It's
simple, unobtrusive, and follows the UNIX tradition of single-purpose
tools that do one thing well.

This project was inspired by [rbenv](https://github.com/sstephenson/rbenv) and
[NewEraCracker](http://www.mtimer.cn/open/server-config/104-neweracracker-best-wamnp-nts-fix.html), and modified for LNMPA.

**Powerful in development.** Compile made easy. Keep server under your control. No
  headaches running apps on different versions of softwares. Auto setup common develop environment. Working with command line start to feel easier. It's unbelievably flexible and expandable. 

**Rock-solid in production.** It includes almost everything you need. It will keep you updated with latest MTEnv versions. The way to manage the environment could not be easier. You can use web control panel or just use commad line even if you know very little about bash language.

**One thing well.** mtenv is made to save time on installing and working with your develop or production environment. It will do more than just help you setup basic server.


### mtenv _does..._

* Let you **change or switch the software versions** with one line command.
* Provide support for **mtenv command of single-purpose**.
* Setup basic environment quickly.


### In contrast with other lnmpa script, mtenv _does not..._

* **Depend on source packages.** mtenv was made from pure shell scripts and compiles softwares.
    There is no bootstrap problem of LNMPA.
* **Need to be loaded into your shell.** Instead, mtenv's shim
    approach works by adding a directory to your `$PATH`.
* **Deny evolution.** Compiling makes mtenv easy to be modified to suit your needs.


----


## Table of Contents

* **[How It Works](#how-it-works)**
  * [Understanding PATH](#understanding-path)
  * [Understanding Shims](#understanding-shims)
  * [Choosing the MTEnv Version](#choosing-the-mtenv-version)
  * [Locating the MTEnv Installation](#locating-the-mtenv-installation)
* **[Installation](#installation)**
  * [Basic GitHub Checkout](#the-manual-way)
    * [Upgrading](#upgrading)
    * [Uninstalling MTEnv](#uninstalling-mtenv)
* **[Command Reference](#command-reference)**
* **[Development](#development)**
  * [Version History](#version-history)
  * [License](#license)


----


## How It Works

At a high level, mtenv intercepts LNMPA commands using shim
executables injected into your `PATH`, and passes your commands along
to the LNMPA installation.


### Understanding PATH

When you run a command like `mtenv` or `mtenv --version`, your operating system
searches through a list of directories to find an executable file with
that name. This list of directories lives in an environment variable
called `PATH`, with each directory in the list separated by a colon:

    /usr/local/bin:/usr/bin:/bin

Directories in `PATH` are searched from left to right, so a matching
executable in a directory at the beginning of the list takes
precedence over another one at the end. In this example, the
`/usr/local/bin` directory will be searched first, then `/usr/bin`,
then `/bin`.


### Understanding Shims

mtenv works by inserting a directory of _shims_ at the front of your
`PATH`:

    ~/.mtenv/libexec:/usr/local/bin:/usr/bin:/bin

Shims are lightweight executables that simply pass your command along
to mtenv. So with mtenv installed, when you run, say, `mtenv httpd`, your
operating system will do the following:

* Search your `PATH` for an executable file named `mtenv-httpd`
* Find the mtenv shim named `mtenv-httpd` at the beginning of your `PATH`
* Run the shim named `mtenv-httpd`, which in turn passes the command along to
  mtenv


### Choosing the MTEnv Version

MTEnv version is taged by release date. You are always recommend to use the latest version.

### Locating the MTEnv Installation

MTEnv is installed into its own directory under
`~/.mtenv`.


----


## Installation

It works on Linux.


### The automatic way

via `curl`

    bash <(curl -sSL git.io/WTRR5Q)

via `wget`

    bash <(wget --no-check-certificate -qO- git.io/WTRR5Q)


### The manual way

This will get you going with the latest version of mtenv and make it
easy to fork and contribute any changes back upstream.

1. **Check out mtenv where you want it installed.**
   A good place to choose is `$HOME/.mtenv` (but you can install it somewhere else).

        $ cd ~
        $ git clone git://github.com/MTimer/mtenv.git .mtenv


2. **Add `~/.mtenv/libexec` to your `$PATH` for access
   to the `mtenv` command-line utility.

        $ echo 'export PATH="~/.mtenv/libexec:$PATH"' >> ~/.bash_profile

    **Zsh note**: Modify your `~/.zshenv` file instead of `~/.bash_profile`.
    **Ubuntu note**: Modify your `~/.bashrc` file instead of `~/.bash_profile`.

3. **Restart your shell so the path changes take effect.**
   You can now begin using mtenv.

        $ exec $SHELL

5. **Install LNMPA included packages.**
   For example, to install LNMPA 2.7.6, download and unpack the source, then run:

        $ mtenv install

   **NOTE:** If you need to use old MTEnv, please use
   ```mtenv install 2014xxxx```.

   **NOTE:** If you are having trouble installing MTEnv,
   please visit the wiki page about
   [Common Build Problems](https://github.com/MTimer/mtenv/wiki/Common-install-problems)


#### Upgrading

If you've installed mtenv using the instructions above, you can
upgrade your installation at any time using git.

To upgrade to the latest development version of mtenv, use `git pull`:

    $ cd ~/.mtenv
    $ git pull


### Uninstalling MTEnv

To remove old MTEnv, `mtenv uninstall` command to automate
the removal process.


----


## Command Reference

See [COMMANDS.md](COMMANDS.md).


----


## Development

The mtenv source code is [hosted on GitHub](https://github.com/MTimer/mtenv).
It's clean, modular, and easy to understand--even if you're not a shell hacker.

Please feel free to submit Pull Requests and report bugs on the
[issue tracker](https://github.com/MTimer/mtenv/issues).


### Version History

See [CHANGELOG.md](CHANGELOG.md).


### License

(This software is not free)

* Copyright (c) 2014 [MTimer](http://www.mtimer.cn)
* Skype: mtimercms@hotmail.com

Buy a license @ www.mtimer.cn
You will get fully-functional MTEnv, lifetime free support and updates.

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.