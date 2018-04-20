---
layout: post
title:      "Diet Tracker - Sinatra Portfolio Project"
date:       2018-04-20 21:47:36 +0000
permalink:  diet_tracker_-_sinatra_portfolio_project
---


One of the main reasons I began learning to build web applications  is to be able to build out the ideas I have for apps.  The app which has all of my focus (or will have all of my focus once I graduate Flatiron) is my fitness app.  

I have a fairly extensive background in Physiology (while in College and grad school, I tallied up about 100 hours of Anatomy, Physiology, Biochemistry, and Nutrition).  I have also been a competitive powerlifter and bodybuilder for 16 years,  and worked as a personal trainer for 6 years.  So on top of the 100+ hours of formal education, I have spent countless hours researching foods and supplements, in order to be able to optimize my own training and nutrition, as well as that of my clients.  

I love fitness and exercise, so I decided I wanted to get back into the industry.  What better way to do so than with an app?!   My app will be focused on younger athletes that want to compete in bodybuilding & fitness related competitions.  The goal of the app is have it auto-generate a custom diet and workout schedule that will be calculated off information input by the user.  Now I know what you're thinking, theres already myfitnesspal and a bunch of other apps like this, but this will be truly unique, and way more customized to the user than anything currently out there.  

ANYWAY, I said all that just to say how excited I was to work on the Sinatra portfolio project, because it was going to be my first opportunity to begin a super super simplified rough draft of the beginning of my app.  Ergo the title of my Sinatra project is The Diet Tracker, which represents the calorie-calculating portion of my overall app.  

The Diet Tracker simply does that, tracks your calories.  It consists of 4 models; User, Food, Meal, and Diet (as well as a join model food_meal).   A Diet belongs_to a User, and a User has_many Diets.  A Meal belongs_to a Diet and a Diet has_many Meals.  A Meal has_many Foods through Food_Meals and vice versa.  

The app is set up so that a 'Diet' represents 1 whole day of eating.   The functionality would be as follows.  A User would create an account.  Then each day, they should login and create a new Diet.  Then everytime they eat, they should login and add that Meal to today's Diet.  The User has the ability to choose from 20 preprogrammed foods (my favorite 20 :) ) as well as the option to add their own foods.  They then choose the foods they eat and how many servings of each. Everytime a meal is added to the diet, the Diet recalculated the protein, carbohydrate, fat, and calorie totals for the day, so the User will know how to adjust his or her eating for the rest of the day to meet their desired targets. 

The app is a super simple way to keep track of how many calories you are consuming, which in my experience has been the best way to ensure results.  

If you'd like an easy way to calculate your calories, clone the repository and check it out! Instructions are in the README.  I hope you enjoy!

https://github.com/jaybednar/diet-tracker-sinatra-app
