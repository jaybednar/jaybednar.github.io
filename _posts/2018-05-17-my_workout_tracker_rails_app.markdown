---
layout: post
title:      "My Workout Tracker Rails App"
date:       2018-05-17 20:43:55 +0000
permalink:  my_workout_tracker_rails_app
---


Continuing on with the theme of fitness, my Rails app is a workout tracker to complement the diet tracker app that I built for my Sinatra project.  

The app consists of 3 models; User, Workout, and Exercise.   A `User has_many :workouts and has_many exercises, through: :workouts`, a `Workout belongs_to :user and has_many exercises`, and an `Exercise belongs to :workout`.  

A user may create an account through our own authentication form, or login/sign up through Github, via the Omniauth gem.  

The app is designed so that a User can log in and add workouts to their log.  A workout is created with a Date, Weekday, Bodypart (area worked that day), and Comments on the workout for later reference.  Once a Workout is created, from the workout show page, you are able to add an exercise, edit the workout, or delete the workout. When you click add a workout, you are taken to the new exercise form.

When adding an exercise, you are able to select an exercise and a bodypart from a pulldown select menu.  For convenience, you have the option to filter the select menu by bodypart, which automatically updates the bodypart select.  You then type in the number of sets and reps you did for that exercise and create the exercise.  

You are then directed back to the workout show page, where you will see the exercise you just added.  If you need to edit or delete an exercise that has been added to a workout, simply click on the exercise and you will be taken to the edit exercise page.  Here you can update all aspects of that particular exercise, or delete the exercise if you so choose. 

If you need ideas about exercises for an upcoming workout, visit the exercises page, where you can view all of the exercises in the database.  Here you have the ability to again filter exercises by bodypart.  You also have the ability to view your exercises, which are the exercises you have used in a previous workout.  

And that is pretty much it.  It is a very simple but useful app for those looking to keep track of their workouts.  

You can check it out here: 

https://github.com/jaybednar/my-workout-tracker-rails-app
