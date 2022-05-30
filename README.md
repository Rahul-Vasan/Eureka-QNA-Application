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
  
  
  
  
  
  

