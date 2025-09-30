# MODELS'25 Tutorial "Using, and contributing to, the MDENet education platform for teaching MDE"

This repository has been set up for a tutorial during the [ACM / IEEE 28th International Conference on Model Driven Engineering Languages and Systems (MODELS'25)](https://2025.models-conf.com/). The tutorial aims to show how the MDENet education platform can be used by students, teachers, and how you can contribute to the platform itself.

This repository contains two example activities that can be run using the MDENet education platform. The platform itself is described in detail in a [SoSyM tools paper](https://doi.org/10.1007/s10270-025-01292-3). It is hosted at https://ep.mde-network.org, where you can also run example activities without requiring a separate repository. The implementation of the education platform can be found on [GitHub](https://github.com/mdenet/educationplatform-docker) and you are welcome to run your own instance or use the [publicly hosted instance](https://ep.mde-network.org).

## Getting started

You can see this repository, so you have already managed to get through the first step of the activity: to get hold of your own repository. Before you can take the next step, we need to take one more preparation step: we need to create a URL that tells the education platform which activity to run.

This repository includes a GitHub Action that is set up to run automatically when the repository is first created. The action will rewrite this README file so that the links in the README will directly open the correct activity. You can see if the action has run by reloading the main page of the repository and checking if the message below is visible as the last commit message.
![Github message on successful preparation of the repository](images/readme_rewrite_success.PNG)

Unfortunately, since 2024, there has been a bug in GitHub Classroom which prevents GitHub Actions to run in new repositories created via GitHub Classroom. As a result, the action we have provided will likely not run automatically and your README file will not be rewritten automatically. I have filed a bug report (and I'm not alone in this), but GitHub haven't been overly responsive. Here are two workarounds to try out:

1. You may be able to get GitHub to allow running the action manually. Follow these steps to try this. It is possible that this will not work. In that case, please try the second approach.

    1. Open [update-private-repo-link.yml](.github/workflows/update-private-repo-link.yml) and click on the edit button in the top right corner: ![pen icon](images/pen_icon.PNG).
    2. Add a space at the top of the file, then remove that space again. This means the file remains unchanged, but you have now enabled the "Commit" button.
    3. Click the "Commit" button to save the file into your repository. Accept the standard commit message and commit directly to `main`. This will trick Github into refreshing its caches and noticing the workflow defined in this file.
    4. Got to the `Actions` tab, then click on `Update privaterepo in README` in the left-hand side menu. Run the workflow from the `Run workflow` dropdown on the right-hand side.
    5. Return to the main page for the repository. Wait and refresh this page until you can see the message below. This indicates that Github has correctly modified this README file and that all links provided below have been customised for your personal use.
    ![Github message on successful preparation of the repository](images/readme_rewrite_success.PNG)

2. Use the [EP URL generator](https://international.mde-network.org/ep_url/) to produce the correct URL for your activity. This will ask you for the URL of your repository (use the text from your browser's address bar) and the path to the activity description -- use the name of the file given for the respective activities below. You can then click on the button to open the education platform with your learning activity.

## Example learning activities

In the tutorial, we first looked at some standard examples using [Epsilon](https://ep.mde-network.org/?activities=https://raw.githubusercontent.com/mdenet/educationplatform-examples/main/epsilon-example/epsilon-example_activity.yml) and [OCL](https://ep.mde-network.org/?activities=https://raw.githubusercontent.com/mdenet/educationplatform-examples/main/ocl/ocl_activity.json), respectively. These are always accessible from the publicly hosted instance of the education platform. Just like the activities in this repository, those standard activities are backed by a [GitHub repository](https://github.com/mdenet/educationplatform-examples/).

Below, I describe the two activities that are contained in the current respository. These are both designed to teach language engineering, in particular the use of Xtext. The first activity looks at how a grammar can be used to generate a metamodel and an editor for a new domain-specific modelling language (DSML). The second activity looks at how ETL can be used to transform models in a student-defined DSML.

### Activity 1: A simple domain-specific modelling language with Xtext

In this activity, students generate and explore a simple DSML with a textual concrete syntax. Students use [Xtext](https://www.eclipse.org/Xtext/) to create the DSML. We will only use the most basic features of Xtext; it can do much more. Check out the [link](https://www.eclipse.org/Xtext/) to find out more.

> You can [do this activity in your browser](https://ep.mde-network.org/?activities=https://raw.githubusercontent.com/mdenet/models25_tutorial/main/basic_xtext_activity.json&privaterepo=true). Click on the link and your browser will open the MDENet Education Platform with the activity pre-loaded. If the link doesn't work correctly, use the [EP URL generator](https://international.mde-network.org/ep_url/) (see above) using the path [`basic_xtext_activity.json`](/basic_xtext_activity.json). You will be asked to sign in to Github; the first time you do this, you will be asked to give the MDENet Application access to your repository. You must do this to complete the activity. The application will only have access to this repository.

#### Exploration

After clicking on the link above (open it in a new tab so you can continue to view these instructions), you will see two panels in your browser. The upper panel contains the grammar of the DSML that we will be developing. This grammar consists of rules; each rule describes the concrete syntax of a bit of the language, starting from the top. Have a look over the grammar and see what of it you can understand -- don't worry too much if you cannot understand everything. A good introduction to the Xtext grammar language can be found [here](https://eclipse.dev/Xtext/documentation/102_domainmodelwalkthrough.html).

For now, you will not make changes to this grammar. Instead, click on the little green "run" button in the top right corner and wait for a bit. When you do this, Xtext runs in the background and generates a lot of code from your grammar. This code implements a full IDE for your language.

Once the generation process has finished (a "Success" popup will appear in the top-right corner of the screen), you will be able to test out the language. For this, click on the link labelled "Try out your language" that has appeared in the left-hand side menu.

This will open a new view (you will be asked again to "sign in with Github"): the left panel is the editor for your new language, the right panel allows us to visualise the internal representation of the language and your model.

First, click on the little diagram button at the top of the *right* panel. This shows a class diagram -- explore it a bit. This is the "meta-model" of your language, sometimes also called the "abstract syntax". It shows the set of classes that Xtext instantiates every time it parses text in your new modelling language. Compare this back to your grammar (you can open a separate copy of the education platform in a separate tab) and see how Xtext has generated classes and attributes from the rules in the grammar. 

Next, look more closely at the left panel. This already contains some text in your new language. Notice the syntax highlighting automatically provided, make some changes, and see how the editor highlights if you are making an error. You can also use `Ctrl+Space` to invoke the auto-completion service. 

Finally, click on the diagram button at the top of the *left* panel. This replaces the contents of the right panel with an object diagram, showing how the classes from the meta-model have been instantiated for your concrete model. Make some changes to the text on the left and regenerate the diagram to explore how the text is translated into a structure of objects. 

#### Make a change

Go back to the first view (you can use the "Define your language" link in the left-hand menu) to see the grammar again. You will now make a change to the grammar.

We want to capture different types of people working on projects: some are regular "Workers" and some are "Bosses". To do this, you will add two new rules and rename one existing one:

1. Rename the existing `Person` rule to `Worker`. This syntax will now capture how regular workers are described.
2. Create a new rule `Boss`. You can place it anywhere in the grammar file, as long as it doesn't come before the initial `Project` rule. It's good practice to put it in a sensible place -- for example, next to your `Worker` rule. The contents of your rule should be
``
Boss:
  'boss' name=ID leads+=[Person] (',' 'and' leads+=[Person])*
;
``
In other words, a boss is someone who leads other people.
3. Add a new rule 
``
Person:
  Boss | Worker
;
``
stating that a person is either a boss or a worker.

Click on the run button and wait until Xtext has successfully generated your new editor. If you get an error message, check if you have done everything correctly.

Explore your new language, checking out the meta-model, object diagram of models, and code completion options. Can you see how Xtext has implemented the new `Person` rule in the meta-model?

### Activity 2: Let's transform our models

In this activity, students take a model in their DSML and transform it into a different model. Because we have limited time, we will experiment with a very simple transformation: we will generate a model listing the deliverables implied by a given project plan. We will also generate a list of authors for each deliverable.

> You can [do this activity in your browser](https://ep.mde-network.org/?activities=https://raw.githubusercontent.com/mdenet/models25_tutorial/main/etl_activity.json&privaterepo=true). Click on the link and your browser will open the MDENet Education Platform with the activity pre-loaded. If the link doesn't work correctly, use the [EP URL generator](https://international.mde-network.org/ep_url/) (see above) using the path [`etl_activity.json`](/etl_activity.json). You will be asked to sign in to Github.

#### Exploration

Again, you first see the Xtext grammar. Click the run button to generate the editor and IDE for your language. Open the generated IDE once the generation has completed successfully.

We now have more panels to explore. We still have the editor for our models in the top-left corner. In the top-right corner, we still have the diagram panel that can show us the meta-model for our language or the object-diagram for our current model as before. Below this, we have four panels for building our transformation:

1. The middle left panel is where students write their transformation code using the [Epsilon Transformation Language (ETL)](https://eclipse.dev/epsilon/doc/etl/). It already contains a basic transformation. Thank you to the Epsilon team, who have written this transformation as part of their library of examples.
2. Once the transformation has been run, you will be able to see an object diagram of the model your transformation has produced in the middle right panel, if the transformation has been successful.
3. The lower left panel is a console view, which will show output from the running transformation, if any. This will show error messages, but you can also send text there by including print statements in your code. Try adding `"Hello World".println();` just above the line that reads `t.title = s.title;` and run the ETL script to see how this works.
4. In the bottom right corner, you can see the definition of the meta-model of the language in which your output model will be produced. This tells you what classes, attributes, and relationships you need to fill out.

Click on the green run button in the ETL panel and see what happens. Compare the object diagram of your model with the object diagram of the transformation result. Follow the ETL description to understand how this is produced.

#### Make a change

Next, try to change the ETL script so that in addition to producing a `Deliverable` object for each `Task`, it fills in the `authors` attribute of the newly created `Deliverable` with a list of the persons working on the task sorted by the percentage of their time they have been working on the task. You can use the `concat(separator : String) : String` operation on the sequence of efforts to turn it into a suitable string.

## Thank you

Many people have helped create the platform and tools for this exercise. I would like to thank:

- Will Barnett, who built the [MDENet Education Platform](https://ep.mde-network.org) building on the [Epsilon Playground](https://eclipse.dev/epsilon/playground/).
- Antonio Garcia-Dominguez, who came up with the Github workflow for rewriting links in README files that makes it easy to run the activities directly from a repository.
- Dimitris Kolovos, Antonio Garcia-Dominguez, and Artur Boronat, who contributed loads of ideas and suggestions as part of the community steering board for the education platform.
- Mehdi Mehtarizadeh, who worked on the platform as a research software engineer and in particular introduced more robust CI/CD support.
- The [UK Engineering and Physical Sciences Research Council (EPSRC)](http://www.epsrc.ac.uk/), who funded the [MDENet network project](https://www.mde-network.org) and the development of the [MDENet Education Platform](https://ep.mde-network.org).