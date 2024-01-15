### What are they?
[Review apps](https://devcenter.heroku.com/articles/github-integration-review-apps) are temporary and disposable instances of the Odin Project app attached to pull requests. They allow us to test changes made in a given pull request within a safe testing environment before we hit merge - without all the hassle of pulling down the changes to our local machines.

### How do I create them?
* Review apps will be automatically created and attached to any pull request an Odin team member opens.
* They cost money for the length of time they exist. So we have them set up to be deleted 24 hours after creation. If you need to recreate a review app, simply add the "create-review-app" label to the PR and a GitHub action will take care of the rest.  

#### Manually creating review apps
We only have a limited number of seats on Heroku, which means only a few maintainers have access to manually create review apps for the moment.

If you need a review app created manually, reach out to these maintainers.
* @CouchofTomato
* @rlmoser99
* @ChargrilledChook
* @KevinMulhern

### How can I access them?
Look for the "View deployment" button within the pull requests activity feed. That will take you directly to the attached review app

### Working with review apps:

#### Signing up/in
You cannot use Google/Github Oauth on review apps. Those services require a static callback url but each of our review apps has a different domain name. However, you can use our [tester account](https://github.com/TheOdinProject/theodinproject/blob/main/db/seeds/test_admins.rb) to sign in using an email and password. 
  
Tester credentials:
> email: tester@odin.com

> password: password

### Testing learner solutions
* When you need to QA anything related to solutions. The best project to use is the recipes project on the Foundations path. We populate that project with a few dummy solutions to save you the time of doing it yourself. 
