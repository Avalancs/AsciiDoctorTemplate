# AsciiDoc(tor) with IntelliJ Idea and Gradle

### Tl;DR
A starter template for writing a document in AsciiDoc markup language and converting it with [AsciiDoctor](https://asciidoctor.org/) into HTML and/or PDF. 
You can do it locally or on a build server by running it as a [Gradle](https://gradle.org/) build, and you can version your changes using Git.

* Writers only need to install IntelliJ Idea Community and live editing of the document is possible with the [AsciiDoc Idea plugin](https://plugins.jetbrains.com/plugin/7391-asciidoc)
* The build server will need to run the Gradle wrapper which will download the necessary tools, so you do not need to install or configure anything
  * Or you can use Gradle itself if you have it installed on your build server already

### How to create a new document based on this repository
1. Copy/download this repository
2. Remove the `.git` folder and `license.txt`
3. Make it into a git repository again with your favourite Git client, or the `git init` command in the terminal
4. Edit `docs/index.adoc` file which is the main document 
   1. It comes with some sample markup from the AsciiDoctor homepage
   2. If you want multiple html pages or PDF files after conversion, create the desired files with `.adoc` extension in the `docs` folder
   3. If you want to create a page that is included in one of the html pages/pdfs', but not converted to an actual separate html/PDF file then create it under a subfolder in `docs` (the template uses the `docs/inc` folder for this)
5. TODO: figure out how css customization works with AsciiDoc
6. TODO: figure out how to add custom fonts to the PDF
7. TODO: more about diagrams and charts
8. Commit+push to your own Git repository

### Converting to PDF or HTML
If you're using the AsciiDoc Idea plugin to live edit the `docs/index.adoc` file, then it has two buttons labeled "HTML" and "PDF" which will do the conversion for you. 
Live edit is also possible in Visual Studio Code, but I haven't tried it out.

If you are using IntelliJ Idea (or any other IDE that has Gradle integration) then 
* the `asciidoctor` task generates HTML into the `build/docs/asciidoctor` folder
  * You need to copy/archive all files from this folder
* the `asciidoctorPdf` task generates PDF into the `build/docs/asciidoctorPdf` folder
  * You only need to copy/archive the pdf file(s)

If you want to use this from terminal, or a build server then you will need to issue the following command.

For Linux:
```shell
# set the execute permission on the Gradle Wrapper file and then run it
chmod +x gradlew
./gradlew asciidoctor asciidoctorPdf
```

For Windows:
```cmd
gradlew.bat asciidoctor asciidoctorPdf
```

### Customizing the build process
If you open `build.gradle` you will see that it is using the [Gradle AsciiDoctor plugin](https://asciidoctor.github.io/asciidoctor-gradle-plugin/development-3.x/user-guide) to generate HTML and PDF.

Refer to their documentation to see how you can customize the conversion process (e.g.: Set where the Table of Contents appear in the HTML version etc.)

TODO: figure out how to add custom CSS to the conversion process

### Software used
* [IntelliJ Idea as IDE](https://www.jetbrains.com/idea)
  * [AsciiDoc Idea plugin](https://plugins.jetbrains.com/plugin/7391-asciidoc)
* [Gradle build tool](https://gradle.org/)
  * Uses 7.1 currently, which requires Java JDK 11 
  * [AsciiDoctor Gradle plugin](https://asciidoctor.github.io/asciidoctor-gradle-plugin/development-3.x/user-guide)
    * It uses [AsciiDoctorJ](https://github.com/asciidoctor/asciidoctorj) internally

### Motivation
I worked on a typical Java software project where the requirements doc was in Microsoft Word stored on SharePoint.

The architect who wrote it would complain that every time we opened the docx file, 
a new "version" would be created in the file history because of how Microsoft Word+SharePoint would auto-save the document. 
We could never know if anything was changed based on the file history. 
Every time there was a change they would have to add it to the changelog in the document per customer requirements.

The solution to that was that whenever someone would modify the doc they would export it to PDF and put it next to the docx file, 
so other people just wanting to read it would open the PDF instead. But sometimes the person editing it would forget to update the PDF afterwards, which would cause confusion when they would say "but I added X to the document!" and it would not be there in the PDF.

Later on the requirements would change on a daily basis when the customer started actively giving feedback, 
and the changelog would no longer be updated as there wasn't enough time for it anymore. 
Developers would not get notified about changes to the spec, or would not find the exact changes and conversations like this would occur regularly:

```
BA:  Hey, the software doesn't work according to the requirements!
Dev: But this is the behaviour that we agreed to last week.
BA:  But the requirements changed a few days ago, didn't you see it in the docs?
Dev: I didn't get notified/I didn't see that particular change in that huge doc! 
```

I thought _If these docs were in plaintext like code, then storing them in git would make it easy to see changes and get notified of them via email_. 
Then I learned about [doc-as-code](https://www.writethedocs.org/guide/docs-as-code/) which is exactly what I was looking for!

I wanted to create a proof of concept that would require the minimum amount of installation/configuration
to make it easy for people to get started with AsciiDoctor, and here it is!

### License
This template is provided with an MIT-style license, but you do not need to keep the copyright, or reference the author in any way. 