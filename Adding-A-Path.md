#### 1. Add the new Path to the Seeds

1. Create a new path directory under `db/fixtures/paths/` - name the new path directory the same as what the new paths title will be on the site. for example `foundations` or `full_stack_javascript` etc.
2. Create a new `seed.rb` file in the path directory you just created.

3. At the top of the `seed.rb` file, create your new path:
 ```
@path = Seeds::PathSeeder.build do |path|
end
```

4. Give the path a title:
```
@path = Seeds::PathSeeder.build do |path|
  path.title = 'Full Stack JavaScript'
end
```

5. Give the path a description:
```
@path = Seeds::PathSeeder.build do |path|
  path.title = 'Full Stack JavaScript'
  path.description = "This path teaches you x and y"
end
```

6. Give the path an identifier_uuid attribute value of `'create_uuid'`. This will be replaced by a real uuid automatically when the seed script is run later.
```
@path = Seeds::PathSeeder.build do |path|
  path.title = 'Full Stack JavaScript'
  path.description = "This path teaches you x and y"
  path.identifier_uuid = 'create_uuid'
end
```

7. Finally give your path a position, this attribute determines what position the path will be displayed at on the https://www.theodinproject.com/paths page.
```
@path = Seeds::PathSeeder.build do |path|
  path.title = 'Full Stack JavaScript'
  path.description = "This path teaches you x and y"
  path.identifier_uuid = 'create_uuid'
  path.position = 3
end
```

8. Add courses, sections and lessons to the path using these guides: 
* [Adding Courses](https://github.com/TheOdinProject/theodinproject/wiki/Adding-a-Course)
* [Adding Sections](https://github.com/TheOdinProject/theodinproject/wiki/Adding-a-Section)
* [Adding Lessons](https://github.com/TheOdinProject/theodinproject/wiki/Adding-a-Lesson-to-the-Curriculum)

9. Add the Clean up step to the bottom of the seed.rb file - This will clean up any removed courses from the path in the future.
```
@path.delete_removed_courses
```


#### 4. Verify the Path has been Successfully Added
1. Run the seeds task: `bin/rails db:seed`
2. Run the app locally and check the path is where it should be and contains the courses, sections and lessons you expect.
3. All done 🎉