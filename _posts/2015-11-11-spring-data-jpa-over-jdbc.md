---
layout: post
author: Colin
title: "Spring Data JPA versus JDBC"
description: ""
category:
image:
 feature: autumn.jpg
 topPosition: 0px;
tags: [Software, Development, Team, Spring JPA, JDBC, Java, Spring Data ]
---
{% include JB/setup %}


In this short blog I'm going to very briefly show you how good Spring Data JPA is and why I think you should choose
this over raw JDBC code.

> "You don't need to write a single line of code."

Yep, you heard me say it.

We used to write raw JDBC code in our DAOs. This is what our code used to be like:

```java
DBConnection con = null;
Person person = new Person();

String sql = "select * from person p Where p.person_id = ?";

try {
      con = getDBConnection();
      con.prepareStatement(sql);
      con.setInt(1, person_id);
      con.executeQuery();

      if (con.next()) {
          person.setPersonRef(con.getString("Person_Ref"));
          person.setPersonTitle(con.getInt("Title"));
          person.setPersonFirstName(con.getString("First_Name"));
          person.setPersonLastName(con.getString("Last_Name"));
          person.setAddress1(con.getString("Address_1"));
          person.setAddress2(con.getString("Address_2"));
          person.setAddress3(con.getString("Address_3"));
          person.setAddress4(con.getString("Address_4"));
          person.setPostcode(con.getString("Postcode"));
          person.setEmail(con.getString("Email_Address"));
          person.setPhoneDay(con.getString("Phone_Day"));
          person.setPhoneEve(con.getString("Phone_Eve"));
      }

} catch (Exception ex) {
      LOGGER.error(ex);
      throw new BusinessException("DB Error", ex.getMessage());
} finally {
      try {
          con.close();
      } catch (Exception ex) {
          LOGGER.error(ex);
      }
}

return person;
```

Stuff like the above would take us a good few hours to code to make sure getting everything right.

Now with Spring Data JPA, we are using Repositories like these:

```java
@Repository
public interface PersonRepository extends JpaRepository<PersonEntity, Integer> {

}
```

WOW! Just an empty Java interface? Yes indeed it is!  

Okay, you could argue you still had to code up 3 or 4 lines of text but with the best modern IDEs, you can get them to auto-generate it for you.

Intellij IDEA, Eclipse and Netbeans all allow you to automatically generate an empty code file implementing an interface etc. just by a click of a button or a few buttons.

I'm not saying JDBC is bad. It is very good in certain situations (which I'm not going to cover here). But I feel Spring Data JPA is awesome and that not just it saves you development time but also enables you to write less error prone code. It is an abstraction layer which the Spring Framework itself has taken care of the nitty gritty data access code for you.

I admit, when I first heard of this technology, I was quite sceptical about it. My first reaction was, "What's the point of having us developers if we not writing any much code?"

But having used Spring Data JPA for over 5 months now, I can see the benefits it brings. We 'Application Developers' should be focused on writing 'Application Code' implementing business logic to solve business problems. And this is where Spring Data JPA really helps - it relieves you from having to spend so much time in writing 'Data Access' code - code that is sometimes considered as boilerplate/mondane infrastructure code surrounding you application.

Need I say more?  :)
