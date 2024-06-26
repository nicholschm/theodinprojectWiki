Thank you for expressing interest in contributing!

If you would like to contribute, but are not sure how, find an [issue tagged with "help wanted"](https://github.com/TheOdinProject/theodinproject/labels/Help%20Wanted) to work on.
* Please comment on the issue stating what you'd like to work on and wait to be assigned before working on it. 
* After being assigned, address each item listed in the acceptance criteria. 

If you would like to propose a small change (fixing a typo, updating a link, etc.) that is not part of an existing issue, you are welcome to make the change and submit a PR.

If you would like to propose a change that is not covered in an open issue, please start by creating a new issue or discussing this in our [Discord's contribution-suggestions channel](https://discordapp.com/channels/505093832157691914/540903304046182425).

## How to Contribute
1. Install Ruby [here](https://www.theodinproject.com/lessons/ruby-installing-ruby)

2. Install Rails [here](https://www.theodinproject.com/lessons/ruby-on-rails-installing-rails)

3. Install the app on your local machine.

 * Fork and clone the app to your local machine. Use [this guide](https://help.github.com/articles/fork-a-repo/) if you don't know how to do that.
 * Set the upstream remote so you can keep your copy of the app synced with the original. To do that, go to your terminal and `cd` into your cloned odin project app directory. Then, use one of the following commands:

    If you have ssh set up with Git
    ```
    $ git remote add upstream git@github.com:TheOdinProject/theodinproject.git
    ```
    Otherwise
    ```
    $ git remote add upstream https://github.com/TheOdinProject/theodinproject.git
    ```

 * Use one of the following operating system specific guides to set up The Odin Project app on your machine:
    * [Linux installation guide](https://github.com/TheOdinProject/theodinproject/wiki/Linux-Installation-Guide)
    * [Mac installation guide](https://github.com/TheOdinProject/theodinproject/wiki/OSX-Installation-Guide)

 * Follow this guide to [run The Odin Project app locally](https://github.com/TheOdinProject/theodinproject/wiki/Running-The-Odin-Project-Locally).

4. Before you start working on your issue, create a branch and name it like the following examples:

    If it's a new feature
    ```
    $ git checkout -b feature/new-feature-name
    ```
    If it's a bug fix
    ```
    $ git checkout -b fix/fixed-bug-name
    ```

5. When you have finished, ensure that the code is formatted correctly and all tests pass:
 
    ```
    $ rubocop
    ```
 
    ```
    $ yarn eslint
    ```

    ```
    $ rspec
    ```

6. Submit a pull request:

  * Push your branch to your fork
    ```
    $ git push origin <your branch name here>
    ```

  * Create a pull request
    * Go to your fork on Github after you have pushed up your branch. A new button should be visible near the top of the page. It will allow you to create a pull request to the original Odin Project Repo.

    * If the PR is related to an existing issue, link it in the body of your pull request, such as "resolves #1234".

## Need Help with Anything Here?
Please let us know if you require any help doing any of the steps in this guide in our [Discord's contribution-suggestions channel](https://discordapp.com/channels/505093832157691914/540903304046182425).
