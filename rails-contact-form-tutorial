# Contact Form for Rails App in 25 steps

![](drop-me-a-line.gif)


## Usage

Let's assume that you already have a Rails application and you own the github repository. 

1. Before creating a new branch, pull the changes from master. Your master needs to be up to date, run:

   `git pull origin master`

   then create new branch `git checkout -b contact-form`


2. Create model

   run `rails g model contact name email message:text`
   
   migrate contacts table to database `rails db:migrate`

   commit change, run `ga . && gc -m 'generate contact model`


3. Create controller

   run `rails g controller contacts new create`
   
   commit change, run `ga . && gc -m 'generate contacts controller`


4. Add bootstrap 

   run `yarn add bootstrap`


5. Open Gemfile and add:

   ```ruby
   gem 'simple_form'
   gem 'mail_form'
   gem 'invisible_captcha'
   ```
   
   then run `bundle install`
   

6. Run the generator of simple_form and mail_form

   ```ruby
   rails g simple_form install --bootstrap
   rails g mail_form
   ```
  

7. Open `app/asset/stylesheets/application.css`

   rename the file into `application.scss`
    
   then add `@import "bootstrap/scss/bootstrap";`
    
 
8. Open `routes.rb` and add:

   ```ruby
   Rails.application.routes.draw do
     root to: "contacts#new"
     post "/contacts", to: "contacts#create"
   end
   ```
   
    
9. Remove or uncomment this line in `development.rb` and `production.rb`:

   `config.action_mailer.raise_delivery_errors = false `
    
    
10. Open `development.rb` and add:

    ```ruby
    config.action_mailer.default_url_options = { host: 'localhost:3000' }
    config.action_mailer.delivery_method = :smtp
    config.action_mailer.smtp_settings = {
      address: 'smtp.gmail.com',
      port: 587,
      domain: 'gmail.com',
      authentication: 'plain',
      enable_starttls_auto: true,
      user_name: ENV['GMAIL_EMAIL'],
      password: ENV['GMAIL_PASSWORD']
    }
    ```
    
    
    
11. Open `production.rb` and add:

    ```ruby
    config.action_mailer_default_url_options = { host: 'https://gmail.com' }
    Rails.application.routes.default_url_options[:host] = 'https://gmail.com'
    config.action_mailer.delivery_method = :smtp
    config.action_mailer.smtp_settings = {
      address: 'smtp.gmail.com',
      port: 587,
      domain: 'gmail.com',
      authentication: 'plain',
      enable_starttls_auto: true,
      user_name: ENV['GMAIL_EMAIL'],
      password: ENV['GMAIL_PASSWORD']
    }
    ```
   
    
12. Open Gemfile and add:

    `gem 'dotenv-rails', groups: [:development, :test]`
    
    then run `bundle install`
    

13. Create env file to store your email and password, run:
    
    ```ruby
    touch .env
    echo '.env*' >> .gitignore
    ```
    
    commit change, run `ga . && gc -m 'create dotenv'`
    

14. Open `.env` and add:

    ```ruby
    GMAIL_EMAIL=your-email@gmail.com
    GMAIL_PASSWORD=abcdefghij
    ```
    
    * You should share `app password`, ~~not actual password~~. Follow [this](https://support.google.com/mail/answer/185833?hl=en-GB) to create one (for gmail).
    
    
 15. Setup model. Open `contact.rb` and add:
 
     ```ruby
     class Contact < MailForm::Base
      attribute :name, validate: true
      attribute :email, validate: /\A([\w\.%\+\-]+)@([\w\-]+\.)+([\w]{2,})\z/i
      attribute :message, validate: true
 
      # Declare the e-mail headers. It accepts anything the mail method
      # in ActionMailer accepts.
      def headers
       {
         subject: "Contact Form",
         to: "your-email@gmail.com",
         from: %("#{name}" <#{email}>)
       }
      end
     end
     ```
     
     commit change, run `ga . && gc -m 'setup contact model`
     

16. Setup controller. Open `contacts_controller.rb` and add:

    ```ruby
    class ContactsController < ApplicationController
      require 'mail_form'
      invisible_captcha only: [:create, :update], honeypot: :subtitle
      def new
        @contact = Contact.new
      end
      def create
        @contact = Contact.new(contact_params)
        if @contact.deliver
          flash.now[:error] = nil
        else
          flash.now[:error] = 'Cannot send message'
          render 'contacts/new'
        end
      end
     
      private
     
      def contact_params
        params.require(:contact).permit(:name, :email, :message, :subtitle)
      end
    end
    ```
    
    commit change, run `ga . && gc -m 'setup contacts controller`
    
    
17. Create partial form file, run:

    `touch app/views/contacts/_form.html.erb`
        
    then add:
        
    ```ruby
    <%= simple_form_for @contact, :html => {:class => 'form-horizontal' } do |f| %>
      <div class="form-inputs">
        <%= f.input :name, required: true %>
        <%= f.input :email, required: true %>
        <%= f.input :message, as: :text, required: true %>
        <%= f.invisible_captcha :subtitle %>
      </div>
      <div class="form-actions mt-5">
        <a href="https://64.media.tumblr.com/tumblr_m2oxi5nGWI1rr3l61o1_500.png" class="btn-c btn-nm mr-auto">Never Mind</a>
        <%= f.button :submit, "Send", class: "btn-c btn-send" %>
      </div>
    <% end %>
    ```
   
   
18. Open `app/views/contacts/new.html.erb` and add:

    ```ruby
    <div class="form-container">
      <div class="form-box">
        <h1 class="form-title">Drop me a line here!</h1>
        <%= render 'form', contact: @contact %>
      </div>
    </div>
    ```
  
  
19. Open `app/views/contacts/create.html.erb` and add:

    ```ruby
    <div class="form-container">
      <div class="form-box d-flex flex-column">
          <h1 class="form-title">Thanks for your message!!</h1>
          <p class="mb-5">I will get back to you soon.</p>
          <div class="mt-5"><%= link_to 'Drop Me A Line', root_path, class: "btn-c btn-send" %></div>
        </div>
    </div>
    ```
    
    commit change, run `ga . && gc -m 'setup contacts controllers and views`
    
    
20. Modify form and views **[here](https://github.com/novatogatorop/drop-me-a-line/blob/master/app/assets/stylesheets/_contacts.scss)**.


21. Run `rails s`

    open [localhost:3000](localhost:3000) then fill out the form and check your email if you receive the contact form.
    

22. Push branch to github, run `git push origin contact-form`

    open your github to create `pull request`
    
    then `merge the pull request`
    

23. Make sure your contact-form branch is clean, run `gst`

    switch to master branch `gco master`
    
    merge contact-form branch to master `git pull origin master`
    
    Do step **number 21** to test contact form
    

24. Set the .env file config vars in on heroku, run:
    
    ```ruby
    heroku config:set GMAIL_EMAIL=your-email@gmail.com
    heroku config:set GMAIL_PASSWORD=abcdefghij
    ```
    

25. Deploy contact form in Heroku. Run:
    
    ```ruby
    git push heroku master
    heroku run rails db:migrate
    ```

    open rails app in heroku, run `heroku open` 

    then fill out the form in the browser and check your email if you receive the contact form.
    
    
    
