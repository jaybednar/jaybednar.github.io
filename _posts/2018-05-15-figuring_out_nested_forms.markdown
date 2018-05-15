---
layout: post
title:      "Figuring Out Nested Forms"
date:       2018-05-15 17:56:54 +0000
permalink:  figuring_out_nested_forms
---


I'm in the middle of building out my rails app, and ran into some issues while building a nested form.  

My app is a simple workout tracker where you can post your workout for the day and add the Exercises, including sets and reps, for the workout.  The models in this app are: User, Workout, and Exercise.  A user `has_many :workouts` and `has_many :exercises, through: :workouts`.  Also, workouts routes were nested under user routes as such: 

```
resources :users do 
 	resources :workouts 
 end 
```

I was building the form to Create a New Workout.  Trying to follow best practices, I Initially built out the form using the following code: 

```
<%= form_for(@user, {url: user_workouts_path(@user), method: :post}) do |f| %>
    <%= f.fields_for :workouts do |w| %>
		    Date:     <%= w.date_field :date, {value: Date.today}
				Weekday:     <%= w.text_field :weekday, {value: calc_weekday(Date.today.wday)}
				Bodypart: <%= w.text_field :bodypart %>
				Comments: <%= w.text_area :comments%> 
				<%= w.submit %>
	   <% end %>
<% end %>
```

Notice the arguments for the form_for . Initially, I just had the @user as the argument, however this was causing issues.  Doing it this way, the form was being interpretted as an update user form, which means it would be submitting a patch request to the edit_user_path.   Since we need to be submitting this to the user_workouts_path via a post request, I put in the options to specify those changes.  This got the form working correctly, but it just didn't seem right to have to do that, knowing how smart rails is.  Also, on the controller side of things, the way of handling the params to create the new workout was very cumbersome.   Using this setup, the form submitted the params as such: 

```
params = {"user" => {"workouts_attributes" => {"0" => {workout_attributes}} }
```

This, while doable, definitely made the create method in the workouts_controller quite cumbersome.  

So I started to question if I even needed to use the fields_for helper method.  So in the workouts_controller, I added the following: 

```
def new
    @user = User.find(params[:user_id])
    @workout = @user.workouts.build
  end
```

Then I built the form around the @workout instance instead of the @user instance.  

```
<%= form_for(@workout, url: user_workouts_path(@user, @workout)) do |w| %>
		    Date:     <%= w.date_field :date, {value: Date.today} %>
				Weekday:     <%= w.text_field :weekday, {value: calc_weekday(Date.today.wday)} %>
				Bodypart: <%= w.text_field :bodypart %>
				Comments: <%= w.text_area :comments%> 
				<%= w.submit %>
	   <% end %>
```

But again, I had to add the url of user_workouts_path to get the correct url, or I would have to add a hidden_field which submitted the user_id to be able to associate the workout to the user in the workouts_controller.  Not clean code in my opinion.  

So, off to Google!  I soon found the correct way to set up this form, using both the @user and @workout instances as the arguments for form_for.  Since I had the workouts routes nested under users, voila, we are working!  

Here is the form that I settled on (for now lol)

```
<%= form_for([@user, @workout]) do |w| %>
		    Date:     <%= w.date_field :date, {value: Date.today} %>
				Weekday:     <%= w.text_field :weekday, {value: calc_weekday(Date.today.wday)} %>
				Bodypart: <%= w.text_field :bodypart %>
				Comments: <%= w.text_area :comments%> 
				<%= w.submit %>
<% end %>
```

And this gets the job done.  I think thats kind of the beauty of Rails.  If it seems like you are taking too many steps or having to add too many work-arounds, you probably aren't following best practices.  
