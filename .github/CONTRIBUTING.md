# Contributions

ClassicPress is a volunteer-driven open source project that thrives when we have multiple contributors working towards a common goal.

Before contributing to this repository, please read our [Democracy page](https://www.classicpress.net/democracy/) to understand how we make decisions about what is included in ClassicPress, and our [roadmap](https://www.classicpress.net/roadmap/) to see what's already planned for the next couple of releases.

The **petitions process** mentioned in our Democracy document is very important to help us prioritize new features based on the needs of our users. There are some [exceptions](https://www.classicpress.net/democracy/#democracy-exceptions) to this process for minor changes and bugfixes, but generally speaking it is a good idea to search or ask in one of our communication channels (see below) before undertaking a change, because most changes should go through the petitions process.

Also, please be sure to follow our [code of conduct](https://www.classicpress.net/democracy/#democracy-conduct) in all interactions with ClassicPress community members.

## Communication channels

We encourage you to join and ask any questions you have about contributing.

- [Slack](https://www.classicpress.net/join-slack/) - great for real-time chat, posting screenshots and asking questions about anything you're stuck on. Or just socializing.
- [Petitions website](https://petitions.classicpress.net/) - for proposing new features or major changes for consideration by the community.
- [GitHub issues](https://github.com/ClassicPress/ClassicPress/issues) - for proposing or discussing bugfixes, or minor improvements. Generally it is a good idea to create a petition for anything that may take a significant amount of time or that may have backwards compatibility implications.
- [Forums](https://forums.classicpress.net/) - if you're not sure where to post your questions, searching and then posting on the forums is a good start. The forums are our most active community channel other than Slack.

## Review criteria

When evaluating bug fixes and other code changes in pull requests (PRs), we look for these things, ideally all of them:

  1. The change impacts existing ClassicPress users. Otherwise, there are literally thousands of things we could look at, but we need to prioritize our development time. Right now the best tool we have for this is the [petitions site](https://petitions.classicpress.net/).
  2. The change is not going to break backward compatibility, and has minimal effects on the existing plugin and theme ecosystem. A good way to evaluate the effects of a change on plugins or themes is to do a search on https://wpdirectory.net. (Major changes are also a possibility but require a planning effort around when and how they will be released, as well as agreement from the community per our [democratic process](https://www.classicpress.net/democracy/).)
  3. The change has automated tests.
  4. We understand the code change very well or can ask questions of someone who understands it very well.

If your change meets all of these criteria then we will most likely accept it.

We take a lot of care with our platform, and ClassicPress is maintained by volunteers in our free time. This means there may be some delays in merging pull requests.

## What to work on?

If you're not sure where to start contributing, here are some ideas:

  - Review and test [existing PRs](https://github.com/ClassicPress/ClassicPress/pulls), especially looking at how well they fit the criteria described above. Let us know how you tested the changes and what you found. We need to be thorough and careful with any changes we make, and the more eyes we can get on our PRs the better.
  - Bugfixes, you can find a list of known bugs on our [issues page](https://github.com/ClassicPress/ClassicPress/issues).
  - Issues with the [`help wanted`](https://github.com/ClassicPress/ClassicPress/labels/help%20wanted) or [`good first issue`](https://github.com/ClassicPress/ClassicPress/labels/good%20first%20issue) labels.
  - [Planned](https://petitions.classicpress.net/?view=planned) or [most wanted](https://petitions.classicpress.net/?view=most-wanted) feature requests from our petitions site.
  - Exploratory PRs with your own suggested changes, but please remember these will be subject to review to make sure they are in line with the project's direction.

## More information

Here is some more information about a few subjects where we've noticed some frequent questions from contributors.

### Automated tests

Any change that introduces new code or changes behavior should have automated tests. These tests mostly use [PHPUnit](https://phpunit.de/) to verify the behavior of the many thousands of lines of PHP code in ClassicPress.

If you're not familiar with automated tests, the concept is basically **code that runs other code** and verifies its behavior. There are lots of [existing examples](https://github.com/ClassicPress/ClassicPress/tree/develop/tests/phpunit/tests) already in the codebase.

A good place to start with automated tests is to **run the existing test suite**. Here are brief steps to make this work:

0. **Linux and OS X are supported.** Windows users will probably have an easier time using a Linux virtual machine or the "Windows Subsystem for Linux" shell available for recent versions of Windows.

1. **Be sure your PHP installation supports the `mbstring` module.** If you're not sure, run `php -m` and look for `mbstring` in the list. If it's not present, and you're on Ubuntu or Debian Linux, you can run `sudo apt-get install php-mbstring` to fix this.

2. **Install `phpunit` version `6.x`.** Example terminal commands:

```
wget https://phar.phpunit.de/phpunit-6.5.9.phar
chmod +x phpunit-6.5.9.phar
sudo mv phpunit-6.5.9.phar /usr/local/bin/phpunit
phpunit --version
```

3. **Clone the ClassicPress `git` repository to your computer:**

```
git clone https://github.com/ClassicPress/ClassicPress.git
cd ClassicPress
```

4. **Install MySQL and create an empty MySQL database.** The test suite will **delete all data** from all tables for whichever MySQL database is configured. *Use a separate database from any ClassicPress or WordPress installations on your computer*.

5. **Set up a config file for the tests.** Copy `wp-tests-config-sample.php` to `wp-tests-config.php`, and enter your database credentials from the step above. *Use a separate database from any ClassicPress or WordPress installations on your computer*, because data in this database **will be deleted** with each test run.

6. **Run the tests:**

```
phpunit
```

7. **Explore the existing tests** in the `tests/phpunit/tests` directory, look at how they work, edit them and break them, and write your own.

_Note: this document is adapted from https://make.wordpress.org/core/handbook/testing/automated-testing/phpunit/ which contains more detail, but there are some differences in how automated tests work with recent versions of WordPress._

### Backporting changes from WordPress

ClassicPress version `1.0.0` is a fork of WordPress `4.9.x`, and since then, a number of changes have been made to WordPress for performance, bugfixes or new features.

ClassicPress is mainly committed to keeping compatibility with the WordPress 4.9 branch. However, we're also open to merging bugfixes and enhancements from later versions of WordPress, **as long as they meet the criteria listed above**.

There are some changes that we already know we want to backport because they fit into our plans for future versions of ClassicPress. You can find some examples under the [`WP backport` label](https://github.com/ClassicPress/ClassicPress/labels/WP%20backport).

Otherwise, if you're interested in backporting a change from WordPress, then please explain in a pull request or issue what the change is, how it works, and why it's something that makes sense for ClassicPress to adopt. Often there is a lot of good discussion about each change in the relevant WordPress Trac tickets, and it makes the maintainers' job much easier to see this discussion summarized and linked.

If you're not sure about any of that, then it's a good idea to ask first. A good way is to create an issue for the specific change you're interested in, along with links to the relevant WordPress changesets and tickets, and any other information you have about how the change works.

Finally, when you're ready to backport a code change, identify the WordPress **changeset number** that you'd like to port, and run the `bin/backport-wp-commit.sh` script to apply the change to the code. If you're porting multiple changesets, you can use the `-c` option to this script to apply all the changesets to the same branch. With each commit there may be some merge conflicts to resolve.

Using this script for all backports saves time for you and for the maintainers, and it also helps us track which WordPress changes we've already included. You can see a list of those changes [here](https://bots.classicpress.net/).
