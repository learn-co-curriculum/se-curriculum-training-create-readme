# Creating a Readme (Page)

## Learning Goals

- Create a lesson repository in GitHub
- Create a lesson in Canvas with the contents of the GitHub repository
- Add a lesson to a module

## Introduction

It's time to create your first lesson! This is a fairly substantial task, but
it's one that will give you the best overview of the full curriculum creation
process. We'll take things one step at a time and show you how to check your
work along the way.

The type of lesson we're creating is referred to as a "Readme". It's a lesson
that doesn't have any code associated with it for students to interact with, and
doesn't require the student to submit their work. In Canvas, this type of lesson
is known as a "Page".

## Creating a Readme Lesson

Start by making a new directory for your lesson (replacing `your-name` with your
name) and initializing Git:

```console
$ mkdir se-curriculum-training-your-name-readme
$ cd $_
$ git init
```

Each lesson needs a few key files:

- `README.md`: the contents of the lesson that the students will see in Canvas
- `LICENSE.md`: an Educational Content License that accompanies all of our
  public GitHub repositories
- `CONTRIBUTING.md`: a file explaining how students can contribute to curriculum
  development
- `.github/workflows/canvas-sync.yml`: a special file that defines a [GitHub
  action][github action] that will be used later to sync changes between the
  repo and Canvas

Starter code for these files are available in this repository:

- [readme template](https://github.com/learn-co-curriculum/se-curriculum-templates/tree/main/readme)

Copy these files into your new directory. Change the top-level heading of the
`README.md` file to:

```md
# Your Name First Readme
```

Commit your changes:

```console
$ git add .
$ git commit -m 'Initialize readme lesson'
```

Your repo is good to go!

Before moving ahead, check that your repo matches this file structure:

```txt
se-curriculum-training-your-name-readme\
  .github\
    workflows\
      canvas-sync.yml
  CONTRIBUTING.md
  LICENSE.md
  README.md
```

Also check that you've committed your work.

## Creating a GitHub Repo

Before creating our page in Canvas, we need to create a GitHub remote for our
repository. We need to do this so the github-to-canvas gem will have the
necessary data to create links between the Canvas page and the GitHub repo.

We can use the GitHub CLI to create a new remote repository and push up our
code. Run the following command from the
`se-curriculum-training-your-name-readme` directory:

```console
$ gh repo create learn-co-curriculum/${PWD##*/} --public --source=. --push
```

This will create a new repository in the learn-co-curriculum organization, using
the name of the folder as the repository name.

- `--public` sets the repository access to public (so students can access it)
- `--source=.` sets the path to the local repository in the current folder
- `--push` pushes the local commits

We can view our new repository on GitHub with this command:

```console
$ gh repo view -w
```

## Creating the Page in Canvas

Now that we've created the lesson, it's time to push it up to Canvas using the
github-to-canvas gem!

Run the following command from the `se-curriculum-training-your-name-readme`
directory:

```console
$ github-to-canvas --create-lesson 5465 -lr --type page
```

This command will do **a lot**. If all goes well, we should see something like:

```txt
Canvas lesson created. Lesson available at https://learning.flatironschool.com/courses/5465/pages/lesson-title
```

Head to the link in Canvas and verify that our lesson was created successfully.
Sweet!

Let's break down that CLI command a bit:

- `--create-lesson 5465`: creates a new lesson from a local Git repository, in
  the Canvas course with an ID 5465 (the course we're working in now).
- `-l`: adds additional Flatiron School HTML after markdown conversion (the
  icons that appear in Canvas in the top-right corner of a lesson).
- `-r`: removes top lesson header (the first `#` header in the markdown file)
  from the HTML body, since that appears as the page title in Canvas.
- `--type page`: specifies that the type of lesson is a page rather than an
  assignment, since there's nothing for students to submit for this lesson. If
  the type isn't specified, the gem will infer it based on the folder structure.
  It's safest to specify a type directly, though.

In addition to creating the lesson in Canvas, the gem also generates a special
`.canvas` YAML file that contains information about the lesson:

```yml
---
:lessons:
  - :id: 154615
    :course_id: 5465
    :canvas_url: https://learning.flatironschool.com/courses/5465/pages/lesson-title
    :type: page
```

This file is **extremely** important, as it allows us to automatically sync
updates to Canvas when we make changes to the repo.

Make a new commit for the `.canvas` file, and push it up:

```console
$ git add .canvas
$ git commit -m 'Add .canvas file'
$ git push
```

## Adding a Lesson to a Module

Even though we've created the lesson in Canvas, until we place it in a module,
students won't have any way to access it.

Modules in Canvas are ways to group sets of lessons together, and establish the
order in which those lessons should be completed.

We'll be adding our newly created lesson to the "Lessons Created By Staff"
module:

- Return to the [course homepage][] in Canvas
- Click the "+" button in the "Lessons Created By Staff" module
- From the dropdown, select "Page"
- Select your lesson
- Click "Add Item"

![Adding page to module](https://curriculum-content.s3.amazonaws.com/curriculum-training/create-readme/canvas-add-page.png)

We'll also add a [module requirement][] for the lesson. This is a required step
for all lessons that will allow students to keep track of which lessons they've
completed. To add a module requirement:

- Click the three dots in the "Lessons Created By Staff" module
- Select "Edit"
- Click "Add requirement"
- From the new requirement, select your lesson, and leave "view the item" as the
  requirement
- Click "Update Module"

![Adding a requirement](https://curriculum-content.s3.amazonaws.com/curriculum-training/create-readme/canvas-add-requirement.png)

Now when a student views this lesson in Canvas, it will be marked as complete.

You can verify that this worked successfully by checking if "View" is listed
under the lesson title in the module.

![Module requirement validation](https://curriculum-content.s3.amazonaws.com/curriculum-training/create-readme/canvas-module-requirement-validation.png)

Nice work!

## Conclusion

That's it, we've done it! We've successfully created a new lesson in GitHub,
pushed the lesson to Canvas, and added it to a module.

[github action]: https://github.com/features/actions
[course homepage]: https://learning.flatironschool.com/courses/5465
[module requirement]:
https://community.canvaslms.com/t5/Instructor-Guide/How-do-I-add-requirements-to-a-module/ta-p/1131
