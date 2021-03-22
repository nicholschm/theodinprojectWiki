### Adding a New Lesson

#### 1. Adding the Lessons Attributes
1. Go to `db/fixtures/lessons` and choose the appropriate file that the lesson should go in.
2. Add the new lessons attributes to the bottom of the list.
3. [Generate a unique uuid](https://www.uuidgenerator.net/) and use it for the identifier_uuid attribute for the new lesson.

This is what your new lesson attributes should look like when you are done:
```
},
  'Your New Lesson Title' => {
    title: 'Your New Lesson Title',
    description: 'This is a new lesson',
    url: '/foundations/new_lesson_github_path.md',
    identifier_uuid: 'a4baeee4-7bab-47ba-8157-c8f52b204734',
  },
}
```

#### 2. Add the Lesson to a Course.
1. First find the path you want to add the lesson to in `db/fixtures/paths/`
2. Next find the course in that path you want the lesson to appear in `db/fixtures/paths/<selected_path>/courses/`
3. When you have found the correct path and course, you next have to find the section within that course you want the lesson to be in.
4. When you have found the correct section simply add the lesson to the section by fetching the lesson using the title you provided in the attributes in step one of this guide:
```
section.add_lessons(
  foundation_lessons.fetch('Existing Lesson'),
  foundation_lessons.fetch('My New Lesson'),
)
```

#### 3. Verify the Lesson has been Successfully Added

1. Run the seeds task `rails db:seed`
2. Run the app locally and check the lesson is where it should be.
3. All done 🎉 