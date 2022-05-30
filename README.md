# Eureka-QNA-Application

This project is aimed at building an application that can help people collaborate with each other to help the community in solving critical questions. The main aim of this project is to express my knowledge for applications that use relational database schemas.

# Here is a quick demo of the system

## Table of Contents

- [ER Diagram](#ER)
- [Assumptions](#assumptions)
- [Relational Schema](#schema)
- [Description of the system](#description)
- [Points System](#points)
- [Customized Search Algorithm](#search)
- [Security Features](#security)
- [Challenges Faced](#challenges)
- [Future Scope](#futurescope)
- [Contact Me](#contact)


***

<a id='ER'></a>
## ER Diagram

<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/ER.png" width = 700><p>
  
<a id='assumptions'></a>
## Assumptions
  
Below are few assumptions that I made in constructing the functionality of the system.
  
1) I do not want to store the first name and last name of the user, assuming display name is more than enough and not many would be keen on revealing identity.
2) Subtopic_id  is global ID for a subtopic throughout the system.
3) There could be the same subtopic name associated with 2 different subtopic_ids .For example programming can a subtopic in the parent topic algorithms and also a subtopic in the parent topic Java with different subtopic_id
4) Each subtopic_id is associated with a parent_topic and the parent_topic_name is unique
  
Incase none of these assumptions make sense right now, nothing to worry, a short description of the entire system is described below and therefore it'll be a lot more clear after going through that part.
  
<a id='schema'></a>
## Relational Schema
  
**users**(display_name, emailhash, passcode, city, state, country,user_level,aboutme, points)

**questions**(question_id, title, body, questioner_display_name, posted_datetime,question_status,resolved_datetime)

  questioner_display_name references users(display_name)

**answers**(answer_id, answer_text,answerer_display_name, question_id, posted_datetime,is_best,is_accepted)

  answerer_display_name references users(display_name)

  question_id references questions(question_id)

**votes**(voter_display_name, answer_id, votetype, votedatetime)

  voter_display_name references users(display_name)

  answer_id references answers(answer_id)

**topics**(subtopic_id,subtopic_name,parent_topic_name)

**question_topic_mapping**(subtopic_id,question_id)

  question_id references questions(question_id)

  subtopic_id references topics(subtopic_id)
  
<a id='description'></a>
## Description Of The System
  
**Modules constituting the overall system**
  
1) User signup
2) User login and logout
3) User edit profile
4) Add a new question and tag the questions with relevant topics
5) View all questions added by me (in a separate window)
6) View all answers added by me ( in a separate window)
7) View all questions
7.1) For each question in the system: add a new answer, edit my answer, delete my answer, upvote any answer, downvote any answer, flag any answer, also undo any of my current votes.
7.2) For each question added by me: delete question, edit question, add answer,mark answer as best, mark answer as accepted, unmark all of these, mark question as resolved and all the features in 7.1
8) View my user level
9) Search for a question or answer based on keywords.
  
## Short Description of each module, screenshots and the query associated with it
  
**1) User Signup module:**

The user signs up to the service. The users table stores the unique display_name, passcode, email address and country as they are required fields. So we only ask the users to enter the required fields. The passcodes are MD5 hashed and stored into the database. He may also have a short description about himself stored under about_me of type longtext, and also enter his state and city, and all these can entered after signing up and logging into the system using the edit profile option in the homepage. Only users signed up for the system can access all the modules of the system. Once the credentials entered during signup is verified the user is asked to log in or if there are any errors the user is prompted with what needs to be corrected. A password mismatch, invalid email format are alerted to the user.
  
**Screenshot**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/usersignup.png" width = 700><p>
  
**Associated Query**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/usersignupcode.png" width = 700><p>  
  
**2) User Login and Logout module:**
	
The user logs into the system with his unique display_name, passcode.The MD5 passcodes are decoded and compared in the backend. If the display_name or the passcode is wrong , it prompts you to enter a valid display name, or a password mismatch.It also means you havent registered yet and it asks you to register first. Upon logging in to the system, they can see their display_name on the questions/answers asked/answered by them.They can access all other modules of the systems. A logout functionality is also available for the user to log out of the system.It takes the user back to the login/signup page. 

**3) User edit profile:**

This option is provided to the user once he has logged into the system and can be found on the navigation bar of the homepage. All his existing data will be present on the text area and all text areas will be editable. On clicking the submit button the update will happen. 

**Screenshot**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/editprofile.png" width = 700><p>
  
**Associated Query**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/updateprofilequery.png" width = 700><p>
 
**4) Add a new question and tag the questions with relevant topics**
  
The ask a question on the homepage allows user to ask their question. They need to enter the title and body of the question, and will be alerted if either of them is empty. He also may want to tag his questions with one or more predefined set of topics in the system.Once a question is added, it gets displayed on the homepage immediately for him and other user to view and answer. Adding a questions, shows them under the User’s my questions tab.It also updates the user points by 1 for each question asked. 
  
**Screenshot**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/addandtagquestion.png" width = 700><p>
  
**Associated Query**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/addandtagquestionquery.png" width = 700><p>
  
**5) View all questions added by me**
  
This is also another option provided to logged in user as part of the navigation bar to view only the questions posted by him with latest questions first. A simple select query on question table to get all questions posted by logged in user which can be found in the session variable would do this.
  
**Screenshot**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/myquestions.png" width = 700><p>
  
**Associated Query**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/myquestionsquery.png" width = 700><p>
  
**6) View all answers added by me**
  
This is also another option provided to logged in user as part of the navigation bar to view only the answers posted by him. However the questions for which he answered are displayed, and clicking on that will lead him to the next page, where he can see the question title, body, all other answers along with his. He will be able to edit his answer text from here.

**Screenshot**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/myanswers.png" width = 700><p>
  
**Associated Query**
  
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/myanswersquery.png" width = 700><p>
	
**7) View all questions**

**7.1) For any question in the system:**
	
So on the homepage all the questions of the system are added in reverse chronological order.

**Screenshot:**
	
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/homepage.png" width = 700><p>

A logged in user can view all of these questions. But certain features provided to a user are restricted to only the questions added by him. So for all questions of system the generic ability of the user will be to: 

1) Add a new answer
2) Vote for any answer
3) Edit any answer posted by him
4) Delete any answer posted by him
5) Undo any of his current votes
	
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/rahulexample.png" width = 700><p>

So this is a question not posted by ‘rahul’ but he has given 2 answers for it. So he will be able to delete all his answers using the delete key and edit his answer using the text area. Also he will able to like dislike or flag any answer from any question but cannot vote 2 different things like like and dislike or dislike and flag for each answer. For each answer there can be only one vote from a particular user. By clicking the same vote again the vote will be removed for that answer ( toggle kind of). And for each question a text area appears at the bottom which can used to add a new answer.
	
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/rahulexample2.png" width = 700><p>
	
**7.2) For each question asked by the user, the user gets to have extra features such as:**

1) Edit the question title and body
2) Delete the question
3) Mark the question as resolved
4) Choose a best answer and any number of accepted answers
	
These are additional features to what discussed in the previous section(7.1)
	
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/rahulexample3.png" width = 700><p>
	
This is one question asked by ‘rahul’ and he gets the option to edit, delete and mark the question resolved. Additionally he also get to choose the best answer and all accepted answers.
	
<p align="center"><img src = "https://github.com/Rahul-Vasan/Eureka-QNA-Application/blob/main/img/rahulexample4.png" width = 700><p>	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
  
  
  
  
  
  
  
  
  
  
  
  

  

  
  
  
  
  
  
  
  

