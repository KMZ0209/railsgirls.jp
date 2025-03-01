---
layout: default
title: Rails Girls Diary tutorial
permalink: diary-app
---

# Create your first diary app with Ruby on Rails

*Created by Piotr Szotkowski ([chastell](http://chastell.net)) and Tomasz Stachewicz ([tomash](http://tomash.wrug.eu/about.html))*

We will create a little voting app from scratch using a web development framework for Ruby called Rails. Think what your first application should be about – ideally something simple that includes a collection of some sort: e.g., a to-do list, a diary, etc. We’ll use a diary as the base here.

__COACH__: For the rationale behind this slightly different beginners tutorial, take a look at this [post](http://dotclass.org/rails-girls-warsaw-programme/).


**Make sure you have Rails installed.** [**Follow the installation guide**](/install) to get set up.


## Get to know the tools

<div class="indent" markdown="1">

<h3><i class="icon-text-editor">&nbsp;</i></h3>

### Text Editor

* [Visual Studio Code](https://code.visualstudio.com/), [Sublime Text](http://www.sublimetext.com),  Vim and Emacs are examples of text editors your can use for writing code and editing files.

<h3><i class="icon-prompt">&nbsp;</i></h3>

### Terminal (known as Command Prompt on Windows)

* Where you start the rails server and run commands.

<h3><i class="icon-browser">&nbsp;</i></h3>

### Web browser

* (Firefox, Safari, Chrome) for viewing your application.

__COACH__: Assist with the installation; make sure the text editor is set up properly (e.g., check whether the encoding is UTF-8).

</div>

### Important

It is important that you select the instructions specific to your operating system - the commands you need to run on a Windows computer are slightly different to Mac or Linux. If you're having trouble check the Operating System switcher at the bottom of the commands. In case you're using a cloud service (e.g. nitrous), you need to run the Linux commands even if you are on a Windows computer.

## Pure HTML

### File and folder

Create a new directory (folder) and create a file named `index.html` in it. Open that file in your editor and web browser.

__COACH__: Explain that browsers can open local files, only the URL looks stranger than usual.

### HTML skeleton

Start by adding a general skeleton for your HTML by writing the below into the `index.html` file:

{% highlight erb %}
<!doctype html>
<html>
  <head>
    <title>My Little Webapp: Coding Is Magic</title>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="https://rawgithub.com/krzysztofbialek/Rails-Girls-Warsaw-App/master/style.css" />
  </head>
  <body>
  </body>
</html>
{% endhighlight %}

__COACH__: Explain the two main parts of HTML, `<head>` and `<body>`. Explain the `<title>` tag and (briefly) `<meta>` , `<link>` and `<script>` if needed. Bootstrap is there so that CSS can be skipped altogether (unless participants want to cover it).

### First visible content

Add the following HTML between the `<body>` and `</body>` tags (feel free to adjust the contents…):

{% highlight erb %}
<h1>My Rails Girls Diary</h1>
  <div>
    <h2>Submitted a Rails Girls application</h2>
      <p>1.02.2014</p>
      <p>Just submitted an application to a Rails Girls workshop. Can’t wait to see whether I’ll get in!</p>
      <h2>Got in!</h2>
      <p>15.02.2014</p>
      <p>Received an email that my application got accepted! I’ll be at a RG workshop next week!</p>
    <h2>The first day starts…</h2>
      <p>22.02.2014</p>
      <p>Today is the first day of the Rails Girls workshop. My coach is quite strange but it seems we all have Rails installed now and can start learning.</p>
  </div>
{% endhighlight %}

These are your first three diary entries. Note how the different tags get displayed and note the recurring structure.

__COACH__: Tell a bit about HTML tags and their semantic meaning.

### More HTML

Add the following either before or after the above diary entries (again, do adjust to taste):

{% highlight erb %}
<div>
  <h1>My favourite websites</h1>
    <ul>
      <li><a href="http://railsgirls.com">Rails Girls</a></li>
      <li><a href="https://en.wikibooks.org/wiki/Ruby_Programming">Wikibooks</a></li>
      <li><a href="http://guides.rubyonrails.org">Ruby on Rails Guides</a></li>
    </ul>
  </div>
  <img src="https://railsgirls.com/images/rg-warsaw.png" />
{% endhighlight %}

This is an HTML unordered list with some list items containing anchors (links) with hypertext references (URLs) to other pages. It’s followed by a paragraph containing an image – and the image’s source is at the given URL.

__COACH__: Explain how the Web works and talk a bit about HTML elements and attributes.

[Here](https://github.com/krzysztofbialek/Rails-Girls-Warsaw-App)'s a link to repo with styled basic app you can use.

## Moving to Rails

__COACH__: If your students are on Windows, consider using Nitrous.IO as the basis for the following parts.

### New Rails application

Open a terminal window (Command Prompt on Windows), change to the directory where your files are (using the `cd` command) and run `rails new diary` – this will take some time and end up creating a new Rails application. Run `cd diary` to change to the app’s directory.

__COACH__: Explain how to navigate directories and run commands.

### Running the server

Once in the `diary` directory run `rails server` and (once it finishes starting up) go to [http://localhost:3000](http://localhost:3000) in your browser. You should see the ‘Welcome aboard’ page. Stop the server by pressing `ctrl-c`.

__COACH__: Explain what has happened and what’s the output in the terminal window. If the server fails to start due to a missing JavaScript runtime, `gem install therubyracer` and uncomment the relevant line in `Gemfile`.

### First route and view

Create the controller and the route

Run `rails generate controller welcome index` – this will generate your first controller and a route that leads to it. Start your server and go to [http://localhost:3000](http://localhost:3000) to see that your application indeed does support the `/welcome/index` route.

Stop the server and run `rake routes` to see all the routes supported by your application.

__COACH__: Explain URLs and the URL hierarchy. Explain how in Rails URLs map to ‘what happens behind the scene’.

### Move the view to be the top of your site

Edit the `config/routes.rb` file and uncomment (remove the `#` from the front) the `root ’welcome#index’` line (this will probably be the 7th line). This will make the root of your application be the view rendered by the `Welcome#index` action. Go to [http://localhost:3000](http://localhost:3000) and see that indeed the main page of your application now serves this view (rather than the ‘Welcome aboard’ page).

__COACH__: Explain how the main page of an application is the root of the URL hierarchy and that it’s the page that people visit when they just put the host name into the browser’s address bar.

### Move the existing HTML to the right view

Edit the `app/views/welcome/index.html.erb` file and copy the contents of the `<body>` tags from your original `index.html` file (i.e., the list of diary entries and the website links) there, replacing the two lines (with `<h1>` and `<p>`) in the view. Refresh the browser to see that the page now indeed contains the right contents.

__COACH__: Explain that the view only contains the part between `<body>` and `</body>`, as the rest is common to the whole application and is defined elsewhere.

## Iteration

### Repeated content

If you look at the structure of your list of links, it seems that every list item looks similar to the others – it contains a URL (where the link should take the user when clicked) and a name (what should the user see and be able to click on). Rather than writing the links as raw HTML (and potentially make a mistake with some of them) let’s abstract this a bit and iterate over a collection of URL-and-name pairs.

Replace the contents of the `<ul>` tags with the following:

{% highlight html %}
<%
  @websites = [
    ["http://railsgirls.com", "Rails Girls"],
    ["https://en.wikibooks.org/wiki/Ruby_Programming", "Wikibooks"],
    ["http://guides.rubyonrails.org", "Ruby on Rails Guides"],
  ]
%>
<% for url, name in @websites %>
  <li><a href="<%= url %>"><%= name %></a></li>
<% end %>
{% endhighlight %}

Refresh the browser window to see whether your page still has the same links.

__COACH__: Explain what happened – what is an array, what do `<%` and `<%=` ERb tags mean (and how they differ), how iteration works.

Keeping code or data (like the above `@websites` array) in views is simple, but a bad practice and can bite in the long run. For starters let’s move the `@websites` array from the view to the controller. Remove it from the view and put it in `app/controllers/welcome_controller.rb` in the `index` method so it looks like this:

{% highlight ruby %}
class WelcomeController < ApplicationController
  def index
    @websites = [
      ["http://railsgirls.com", "Rails Girls"],
      ["https://en.wikibooks.org/wiki/Ruby_Programming", "Wikibooks"],
      ["http://guides.rubyonrails.org", "Ruby on Rails Guides"],
    ]
  end
end
{% endhighlight %}

Note that after refreshing your browser window nothing should change – this is because variables starting with @ (called ‘instance variables’) can be accessed by both the view and the controller.

__COACH__: Explain the connection between the `WecomeController#index` action and the view; note and emphasise the difference between @-starting `@websites` and plain `url` or `name`.

### Create the model

With the website links out of the hard-coded way, let’s do something with the diary entries. This time we won’t (ab)use a simple Ruby structure like an array, but a proper model that represents a given entry’s data. Let’s start with generating the model – run `rails generate model Entry title:string date:date contents:text` to create an `Entry` model that can represent a diary entry with a title, a publication date and some contents.

__COACH__: Explain what models are and the `field:type` notation for generating them; explain the difference between `string` and `text` types if necessary.

### Migrate the database

Run `rake db:migrate` to migrate the database so that its structure contains a table for entries.

__COACH__: Explain what databases are (in abstract terms, as vessels for storing our application’s data and providing model structures) and why they are needed. Explain that things which are in memory won’t get persisted by default and they need to be persisted explicitly to be available on the next request.

### Play with the model in the Rails console

Now that we have a model, we can start creating instances of that model – i.e., actual diary entries that aren’t hard-coded in the HTML view. For this, we’ll learn a new tool: the Rails console. Start it with `rails console` and, once it boots and shows: you the `>>` prompt, create a few entries:

{% highlight sh %}
>> Entry.create "title" => "Submitted a Rails Girls application", "date" => Date.new(2014, 2, 1), "contents" => "Just submitted an application to a Rails Girls workshop. Can’t wait to see whether I’ll get in!"
…
>> Entry.create "title" => "Got in!", "date" => Date.new(2014, 2, 15), "contents" => "Received an email that my application got accepted! I’ll be at a RG workshop next week!"
…
>> Entry.create "title" => "The first day starts…", "date" => Date.new(2014, 2, 22), "contents" => "Today is the first day of the Rails Girls workshop. My coach is quite strange but it seems we all have Rails installed now and can start learning."
{% endhighlight %}

Note how the console – just like `rails server` – shows you a log of what happens in the background. You can always get an array of all existing entries via `Entry.all`.

__COACH__: Explain what’s going on. Slowly.

## Viewing the persisted contents

### Add the model instances to the existing view

Edit the `WelcomeController#index` action (in the `app/controllers/welcome_controller.rb` file) and add the following either before or after the lines containing `@websites` definition:

{% highlight ruby %}
@entries = Entry.all
{% endhighlight %}

Edit the `app/views/welcome/index.html.erb` view and replace the lines with the diary entries with the following:

{% highlight erb %}
<% for entry in @entries %>
  <h2><%= entry.title %></h2>
    <p><%= entry.date %></p>
    <p><%= entry.contents %></p>
<% end %>
{% endhighlight %}

__COACH__: Discuss what happened; discuss what’s the order of the entries and how they can be reordered (say, by reverse date) and where it should happen.

### Create a controller for diary entries

Now that we have a model we need to create a controller for handling actions related to the instances of the model (creating new entries, showing, editing and deleting existing ones). Run `rails generate controller Entries` – this should generate the `EntriesController` class. Check `rake routes` – notice that the controller isn’t enough, we still need to point URLs to the controller’s actions.

Edit `config/routes.rb` and add a `resources "entries"` line somewhere inside the `Diary::Application.routes.draw` block. Run `rake routes` again: notice how now your application has all kinds of new routes.

__COACH__: Explain how Rails’ route resources work and how they make URLs spring to existence and map to controller actions by default.

### A view of all the entries

As can be seen in the `rake routes` output, the URLs are wired to their relative controller actions. Let’s see what’s missing – visit [http://localhost:3000/entries](http://localhost:3000/entries) in your browser. Uh-oh, it seems like the ‘index’ action is missing – let’s add it – open `app/controllers/entries_controller.rb` and add the below empty method inside the class definition:

{% highlight ruby %}
def index
end
{% endhighlight %}

Now refresh the browser – we no longer have an ‘unknown action’ problem, we now have a ‘template is missing’ problem. Save an empty file as `app/views/entries/index.html.erb` (note it’s just like the `index.html.erb` file in the ‘welcome’ directory before, but this time it’s in the ‘entries’ directory) and refresh the browser again – it should display an empty page. This is good, as our view is quite empty at the moment.

__COACH__: Explain how actions render the related views by default.

Now go to the `app/controllers/welcome_controller.rb` file and find the `WelcomeController#index` method (the one that starts with `def index`). Find the line that sets the `@entries` variable (it should start with `@entries =`) and copy it to `EntriesController#index` (so to the `index` method of the `EntriesController`, which can be found in `app/controllers/welcome_controller.rb`). Similarly, go to the `app/views/welcome/index.html.erb` view and copy the `@entries.each` block (all of the indented lines up to and including the matching `end`) to the `app/views/entries/index.html.erb` view. Refresh the browser: it should now show the list of all your diary entries.

__COACH__: Explain that even though this might look like little to no progress, there is a significant change: we’re no longer operating in the context of the main page of our app, but rather a list of diary entries only (without the links to other websites, for example).

### A view of a single entry

Note how, when you run `rake routes`, the output says that the `/entries/:id(.:format)` pattern maps to the `entries#show` controller action. Go to [http://localhost:3000/entries/1](http://localhost:3000/entries/1) – the URL for your first diary entry; notice how we’re, again, missing an action of the `EntriesController`. Add that (empty for now) action, then refresh the browser and add the (likewise, empty) missing view.

__COACH__: Guide through adding the missing action and view if needed; make sure the process (all the way from deciphering the right `rake routes` line) is well understood.

Now, let’s figure out how to interpret the `1` from the end of the URL to display the right entry. Make the `EntriesController#show` action look like this:

{% highlight ruby %}
def show
  @entry = Entry.find(params["id"])
end
{% endhighlight %}

This line means ‘take the `id` parameter and use it in the `Entry.find` method to find the right entry’. Now edit the `app/views/entries/show.html.erb` view and put there the following:

{% highlight erb %}
<h2><%= @entry.title %></h2>
  <p><%= @entry.date %></p>
  <p><%= @entry.contents %></p>
{% endhighlight %}

Visit [http://localhost:3000/entries/1](http://localhost:3000/entries/1) and compare it with [http://localhost:3000/entries/2](http://localhost:3000/entries/2) to see how using `params[’id’]` means that different diary entries get displayed.

__COACH__: Explain that the `:id` part of the URL template from `rake routes` is made into a key for the `params` hash; discuss what else can be found in the `params` hash.

### Linking entries

Run `rake routes` again; notice how the row for the `entries#show` action starts with `entry` in the ‘prefix’ column. Go to the `app/views/entries/index.html.erb` view and change the line responsible for displaying the title to the below:

{% highlight erb %}
<h2><%= link_to(entry.title, entry_path(entry)) %></h2>
{% endhighlight %}

Note how we use the `link_to` method that takes two parameters, the text to display (`entry.title`) and the path to link to. Check the source of the page to see what is the path for subsequent titles. Note how the path is created by calling the `entry_path` method with `entry` as its argument.

__COACH__: Remind how the HTML for links looks like. Explain the relation between `entry_path` and the `entry` prefix from `rake routes`. Explain why the `entry_path` method needs the `entry` argument. Explain what the `entry_url` method does (and how it differs from the `entry_path`  method) if you want to.

Now let’s try to get back from an entry screen to the index of all entries: edit the `app/views/entries/show.html.erb` template and add a link to the entries index, like this:

{% highlight erb %}
<p><%= link_to("Back to all entries", entries_path) %></p>
{% endhighlight %}

Note, again, how the `entries` prefix from `rake routes` is used to construct the `entries_path` method name. Note how this method does not need a parameter.

## Creating entries via the UI

### Adding the ‘new entry’ form

Now that we have a way to display a list of all entries and a single entry, let’s add a way to create new diary entries. Run `rake routes` and try to figure out which URL (and action) is responsible for new entry creation.

Go to the index of all entries and add a link for creating new entry:

{% highlight erb %}
<%= link_to("New entry", new_entry_path) %>
{% endhighlight %}

Click the link – and add the missing action and view.

__COACH__: Make sure this process is well understood by now.

Edit the `app/views/entries/new.html.erb` view and paste in the below:

{% highlight erb %}
<%= form_for(Entry.new) do |form| %>
  <p><%= form.label("title") %></p>
  <p><%= form.text_field("title") %></p>
  <p><%= form.label("contents") %></p>
  <p><%= form.text_area("contents") %></p>
  <p><%= form.submit %></p>
<% end %>
<p><%= link_to("Back to all entries", entries_path) %></p>
{% endhighlight %}

**Note:** we can skip labels for now

__COACH__: Show how the HTML produced by the `form_for` helper looks like and try to explain how it works.

### Handling the ‘new entry’ form

Refresh the browser and try adding a new entry – you should see the well-known-by-now ‘unknown action’ error. Add the action to the `EntriesController`, but for starters let’s display what the action receives:

{% highlight ruby %}
def create
  render(:text => params.inspect)
end
{% endhighlight %}

Refresh the browser and inspect what exactly the action gets as its params.

__COACH__: Explain how filling a text field and a text area and submitting the form ends up with all the params being POSTed to the controller’s action. Explain what .inspect does.

### Creating and persisting the new entry

Edit the `create` action and make it look like this:

{% highlight ruby %}
def create
  entry_params = params["entry"]
  entry = Entry.create(entry_params)
  redirect_to(entry_path(entry))
end
{% endhighlight %}

Note how we try to get the parameters of the new entry (its title and contents) from the `params` hash and then create a new entry from them, just like in the console. Try submitting the form again – notice that we’re still not there yet, as we get a `ActiveModel::ForbiddenAttributesError`.

- Note: we can skip strong_parameters in the beginning, keeping the application not secure from parameter injection.
- config.action_controller.permit_all_parameters = true
- ^^ yeah, but it will be removed soon.
- maybe not before workshops ;)

This error is because of security measures – it’s relatively simple to POST whatever parameters a user wants to, and Rails protects us from a rogue user that would want to set parameters that they’re not supposed to set (like ‘id’). We need to declare which parameters can be set by the user; change the first line of the `create` action to the below:

{% highlight ruby %}
entry_params = params["entry"].permit("title", "contents")
{% endhighlight %}

Now try submitting the form again – this time it should work and you should get redirected to the newly-created entry.

__COACH__: Make sure the plucking of the new entry’s parameters from `params` is well understood and that it’s accepted that certain fields need to be permitted explicitly.
Editing via the UI

### Adding the ‘edit entry’ form

Now that we can view and create entries, let’s also add the option to edit them. Run `rake routes` and try to guess which route is responsible for editing an entry.

__COACH__: Make sure this is well understood by now.

Edit the `app/views/entries/show.html.erb` view and add the below line somewhere:

{% highlight erb %}
<p><%= link_to("Edit this entry", edit_entry_path(@entry)) %></p>
{% endhighlight %}

Refresh a given entry’s view and click the link. Add the missing action and an empty view.

__COACH__: Again, make sure this is well understood.

Let’s first make sure our `edit` action exposes the right entry to the view. Make sure the `edit` action looks just like the `show` action – i.e., it grabs the right entry based on the id from the URL:

{% highlight ruby %}
def edit
  @entry = Entry.find(params["id"])
end
{% endhighlight %}

Now copy the contents of the `app/views/entries/new.html.erb` view to the `app/views/entries/edit.html.erb` view, but change the first line so that it’s a form for this particular entry – and, optionally, add a link back to this entry’s show screen:

{% highlight erb %}
<%= form_for(@entry) do |form| %>
  <p><%= form.label("title") %></p>
  <p><%= form.text_field("title") %></p>
  <p><%= form.label("contents") %></p>
  <p><%= form.text_area("contents") %></p>
  <p><%= form.submit %></p>
<% end %>
<p><%= link_to("Back to this entry", entry_path(@entry)) %></p>
<p><%= link_to("Back to all entries", entries_path) %></p>
{% endhighlight %}

__COACH__: Make sure all of this is well understood.

Now try to submit the form – which action is still missing? Create it in the controller:

{% highlight ruby %}
def update
  entry_params = params["entry"].permit("title", "contents")
  entry = Entry.find(params["id"])
  entry.update(entry_params)
  redirect_to(entry_path(entry))
end
{% endhighlight %}

Check whether this all works and whether you can now edit the entries.

__COACH__: Make sure the `update` action’s contents are well understood – from permitting params through finding entries to redirecting to the right path.

## Further ideas

Play with your application! Here are some further ideas you might want to add:

- extract form to a partial
- links for editing an entry straight from the index of entries,
- a way to delete an entry,
- a way to edit entry dates,
- a model for tracking website URLs and names (the list on the main page),
- setting entry dates to the future and not displaying future entries in the index until their day comes,
- automatic embedding of video URLs,
- support for different entry authors,
- support for different categories of entries,
- upload and display of images.
