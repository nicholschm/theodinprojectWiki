#### 1. Add the new Section to the Seeds

1. First find the path you want to add the section to in `db/fixtures/paths/`.
2. Next find the course in that path you want the section to appear in `db/fixtures/paths/<selected_path>/courses/`.
3. When you have found the course the section should be in, you next have to determine what where the section will appear in the course. The order that sections are added to the course seed file matters as it uses that to position the section on the site. A good rule of thumb is to find the section your new section will appear after on site. 
4. When you have the position figured out add the section:

```
course.add_section do |section|
end
```

5. Give the section a title:
```
course.add_section do |section|
  section.title = 'A New Section Title'
end
```

6. Give the section a description:
```
course.add_section do |section|
  section.title = 'A New Section Title'
  section.description = 'A brief description of what the section covers.'
end
```

7. [Generate a unique uuid](https://www.uuidgenerator.net/version4) and give the section an identifier_uuid attribute:
```
course.add_section do |section|
  section.title = 'A New Section Title'
  section.description = 'A brief description of what the section covers.'
  section.identifier_uuid = '<paste the uuid you generated here>'
end
```

8. Add lessons to the section, [use this guide](https://github.com/TheOdinProject/theodinproject/wiki/Adding-a-Lesson-to-the-Curriculum) to find out how to add lessons:
```
course.add_section do |section|
  section.title = 'A New Section Title'
  section.description = 'A brief description of what the section covers.'
  section.identifier_uuid = '<paste the uuid you generated here>'

  section.add_lessons(
    ruby_lessons.fetch('A new lesson'),
    ruby_lessons.fetch('Another new lesson'),
  )
end
```

#### 2. Verify the Section has been Successfully Added
1. Run the seeds task rails db:seed
2. Run the app locally and check the section is where it should be.
3. All done 🎉