# Updating Lessons in Dev Environment

The Odin Project uses a rake task to update the curriculum on a daily basis.  We can use this method to update the content in the development environment.

After `rake db:seed` in the setup process, open the `app/services/lesson_content_import.rb` file and find the `def repo` method.  Change the url to your github username, 

```
def repo
  "your-github-user-name/#{lesson.repo}"
end
```

Please note: it is necessary to have a copy of the lesson repositories forked to your github account.

After saving, run `rake curriculum:update_content` to pull new lesson content.  Now, when working in development on `localhost:3000` the new lessons will be pulled from your curriculum repositories.

