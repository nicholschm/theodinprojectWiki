#### 1. Add the new Course to the Seeds

1. First find the path you want to add the course to under the `db/fixtures/paths/` directory.
2. Create a new file under the `db/fixtures/paths/<selected_path>/courses/` directory which will store your course structure - name the new file the same as what you intend to display as the course name on the site. For example `javascript_basics.rb` or `ruby.rb` etc.
3. Find the `seed.rb` file for the path you will be adding the course to `db/fixtures/paths/<your selected path name>/seed.rb`
4. Within the paths seed.rb file, load your course by adding this line to the courses list: 
```
load './db/fixtures/paths/<your selected path>/courses/<your new course name>.rb'
```
5. The order of the course list matters, they are displayed on the site in the same order so ensure you add your new course to the position in the list that you want it to be displayed on the site. 

#### 2. Structure Your Course
1. At the top of the new course file create your new course:
 ```
course = @path.add_course do |course|
end
```

2. Give the course a title:
```
course = @path.add_course do |course|
  course.title = 'JavaScript Basics'
end
```

3. Give the course a description:
```
course = @path.add_course do |course|
  course.title = 'JavaScript Basics'
  course.description = 'A JavaScript Basics course'
end
```

4. [Generate a unique uuid](https://www.uuidgenerator.net/version4) and give the course an identifier_uuid attribute:
```
course = @path.add_course do |course|
  course.title = 'JavaScript Basics'
  course.description = 'A JavaScript Basics course'
  course.identifier_uuid = '<paste the uuid you generated here>'
end
```

5. Add sections and lessons to the course using these guides: 
* [Adding Sections](https://github.com/TheOdinProject/theodinproject/wiki/Adding-a-Section)
* [Adding Lessons](https://github.com/TheOdinProject/theodinproject/wiki/Adding-a-Lesson-to-the-Curriculum)

9. Add the cleanup step to the bottom of the course file - this will take care of any sections and lessons that are removed from the course in the future.
```
course.delete_removed_seeds
```

#### 4. Verify the Course has been Successfully Added
1. Run the seeds task rails db:seed
2. Run the app locally and check the course is where it should be.
3. All done 🎉