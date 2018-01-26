# README

For running App Demo


* Install Ruby

* Install Rails

* In the root project directory type bundle to install all dependecies

* In the root directory type rake db:migration to run migrations and create database and tables

* Then run rails -s to start service

* In your browser type localhost:3000/books

* Now you are in the index books

* You have 2 diferent buttos to the same actions create a new book in HTML or create a new book in Ajax options


Understanding, what I did:

* Open project/app/views/books/index.html.erb you will see:

<div class="ajax"> 
  <%= render partial: 'index' %>
</div>
  
 the div.class=ajax content will receive content if ajax, above it we find 
 <%= link_to 'New Book HTML', new_book_path %> this generate a normal link
<%= link_to 'New Book AJAX', new_book_path, remote: true %> and this one gives ajax link to the same action, now lets see in the controller:

* Open in the project project/app/controllers/books_controller.rb, Rails has 6 actions (new=>create, index, edit=>update, destroy, to the same 4 related actions in cake php new, edit, delete, index). But we will make in create (after submiting action create a render):

    if @book.save if save book:
        format.html { redirect_to @book, notice: 'Book was successfully created.' } and format is html
        format.json { render :show, status: :created, location: @book } and format is json
        format.js   { render :index, book: @books} and format is ajax
      else
        #is request html? render new.html.erb
        format.html { render :new }
        #is request ajax? render new.js.erb with new errors.
        format.js   { render :new}
        format.json { render json: @book.errors, status: :unprocessable_entity }
      end

For all of this work in Ajax we mayght have a new.js.erb and a index.js.erb with the content

$('.ajax').hide('slow',function (){
	$('.ajax').html("<%= escape_javascript(render :partial => 'books/form') %>").show('slow');
}); or similar, actually for index.js.erb whe just change books/form to books/index and this will render index when the action is executed, very simple, uhum? I don't need to create a ajax function in js for this, and this would be great in CakePHP too, very fast development.
