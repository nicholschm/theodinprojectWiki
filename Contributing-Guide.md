##How to Contribute
1. Find a [issue tagged with "help wanted"](https://github.com/TheOdinProject/theodinproject/labels/Help%20Wanted) to work on. Please comment on the issue to say you are working on it.
2. Install the app on your local machine.

  * Fork and clone the app to your local machine, use [this guide](https://help.github.com/articles/fork-a-repo/) if you don't know how to do that
  * Set the upstream remote so you can keep your copy of the app synced with the original. To do that go to your terminal and `cd` into your cloned odin project app directory. Then use one of the following commands:

 If you have ssh set up with Git
 ```
 $ git remote add upstream git@github.com:TheOdinProject/theodinproject.git
 ```
 Otherwise
 ```
 $ git remote add upstream https://github.com/TheOdinProject/theodinproject.git
 ```

 * Now set the app up using one of the following operating system specific guides
   * [Linux installation guide](https://github.com/TheOdinProject/theodinproject/wiki/Linux-Installation-Guide)
   * [Mac installation guide](https://github.com/TheOdinProject/theodinproject/wiki/OSX-Installation-Guide)

3. Before you start working on your issue create a branch and name it like the following examples:

  If its a new feature
  ```
  $ git checkout -b feature/new-feature-name`
  ```
  If its a bug fix
  ```
  $ git checkout -b fix/fixed-bug-name
  ```

4. When you have finished and are ready to submit a Pull request:

  **Before you submit your pull request ensure all the tests pass**
  rspec tests
  ```
  $ rspec
  ```
  cucumber tests
  ```
  $ cucumber
  ```

  **Push your branch to your fork**
  ```
  $ git push origin <your branch name here>
  ```
  **Create a pull request**
   * Go to your fork on github and create a pull request, a button should appear when you go to your fork on Github that will allow you to create a pull request to the original Odin Project Repo.

  * Please Link to the issue your pull request resolves in the body of your pull request.

##Need Help with Anything Here?
Please let us know if you require any help doing any of the steps in this guide in our [contributing channel on gitter](https://gitter.im/TheOdinProject/Contributing)